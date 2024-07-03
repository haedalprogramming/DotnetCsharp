# Dependency injection into controllers in ASP.NET Core

## 목차
- [Dependency injection into controllers in ASP.NET Core](#dependency-injection-into-controllers-in-aspnet-core)
  - [목차](#목차)
  - [생성자 주입](#생성자-주입)
  - [`FromServices`를 사용한 액션 주입](#fromservices를-사용한-액션-주입)
  - [`FromKeyedServices`를 사용한 액션 주입](#fromkeyedservices를-사용한-액션-주입)
  - [컨트롤러에서 설정 액세스](#컨트롤러에서-설정-액세스)
  - [추가 자료](#추가-자료)
  - [출처](#출처)
  - [다음](#다음)

---
ASP.NET Core MVC 컨트롤러는 생성자를 통해 명시적으로 종속성을 요청합니다. ASP.NET Core는 [종속성 주입(DI)](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 기본적으로 지원합니다. DI는 앱을 테스트하고 유지 관리하기 쉽게 만듭니다.

[샘플 코드 보기 또는 다운로드](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/mvc/controllers/dependency-injection/sample) ([다운로드 방법](https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-8.0#how-to-download-a-sample))

## 생성자 주입

서비스는 생성자 매개변수로 추가되며 런타임은 서비스 컨테이너에서 서비스를 해결합니다. 서비스는 일반적으로 인터페이스를 사용하여 정의됩니다. 예를 들어 현재 시간이 필요한 앱을 고려해 보십시오. 다음 인터페이스는 `IDateTime` 서비스를 노출합니다:

```C#
public interface IDateTime
{
    DateTime Now { get; }
}
```

다음 코드는 `IDateTime` 인터페이스를 구현합니다:

```C#
public class SystemDateTime : IDateTime
{
    public DateTime Now
    {
        get { return DateTime.Now; }
    }
}
```

서비스 컨테이너에 서비스를 추가합니다:

```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDateTime, SystemDateTime>();

    services.AddControllersWithViews();
}
```

`AddSingleton` 에 대한 자세한 내용은 [DI 서비스 수명 주기](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0#service-lifetimes)를 참조하십시오.

다음 코드는 시간대에 따라 사용자에게 인사를 표시합니다:

```C#
public class HomeController : Controller
{
    private readonly IDateTime _dateTime;

    public HomeController(IDateTime dateTime)
    {
        _dateTime = dateTime;
    }

    public IActionResult Index()
    {
        var serverTime = _dateTime.Now;
        if (serverTime.Hour < 12)
        {
            ViewData["Message"] = "It's morning here - Good Morning!";
        }
        else if (serverTime.Hour < 17)
        {
            ViewData["Message"] = "It's afternoon here - Good Afternoon!";
        }
        else
        {
            ViewData["Message"] = "It's evening here - Good Evening!";
        }
        return View();
    }
```

앱을 실행하면 시간에 따라 메시지가 표시됩니다.

## `FromServices`를 사용한 액션 주입

`FromServicesAttribute`는 생성자 주입을 사용하지 않고도 액션 메서드에 서비스를 직접 주입할 수 있게 합니다:

```C#
public IActionResult About([FromServices] IDateTime dateTime)
{
    return Content( $"Current server time: {dateTime.Now}");
}
```

## `FromKeyedServices`를 사용한 액션 주입

다음 코드는 [`[FromKeyedServices]`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.fromkeyedservicesattribute) 속성을 사용하여 DI 컨테이너에서 키드 서비스를 액세스하는 방법을 보여줍니다:

```C#
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddKeyedSingleton<ICache, BigCache>("big");
builder.Services.AddKeyedSingleton<ICache, SmallCache>("small");
builder.Services.AddControllers();

var app = builder.Build();

app.MapControllers();

app.Run();

public interface ICache
{
    object Get(string key);
}
public class BigCache : ICache
{
    public object Get(string key) => $"Resolving {key} from big cache.";
}

public class SmallCache : ICache
{
    public object Get(string key) => $"Resolving {key} from small cache.";
}

[ApiController]
[Route("/cache")]
public class CustomServicesApiController : Controller
{
    [HttpGet("big")]
    public ActionResult<object> GetBigCache([FromKeyedServices("big")] ICache cache)
    {
        return cache.Get("data-mvc");
    }

    [HttpGet("small")]
    public ActionResult<object> GetSmallCache([FromKeyedServices("small")] ICache cache)
    {
        return cache.Get("data-mvc");
    }
}
```

## 컨트롤러에서 설정 액세스

컨트롤러 내에서 앱 또는 구성 설정에 액세스하는 것은 일반적인 패턴입니다. [Options pattern in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-8.0)에서 설명하는 *옵션 패턴*은 설정을 관리하는 선호되는 방법입니다. 일반적으로 `IConfiguration`를 컨트롤러에 직접 주입하지 마십시오.

옵션을 나타내는 클래스를 생성합니다. 예를 들어:

```C#
public class SampleWebSettings
{
    public string Title { get; set; }
    public int Updates { get; set; }
}
```

서비스 컬렉션에 구성 클래스를 추가합니다:

```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDateTime, SystemDateTime>();
    services.Configure<SampleWebSettings>(Configuration);

    services.AddControllersWithViews();
}
```

앱이 JSON 형식의 파일에서 설정을 읽도록 구성합니다:

```C#
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddJsonFile("samplewebsettings.json",
                    optional: false,
                    reloadOnChange: true);
            })
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

다음 코드는 서비스 컨테이너에서 `IOptions<SampleWebSettings>` 설정을 요청하고 이를 `Index` 메서드에서 사용합니다:

```C#
public class SettingsController : Controller
{
    private readonly SampleWebSettings _settings;

    public SettingsController(IOptions<SampleWebSettings> settingsOptions)
    {
        _settings = settingsOptions.Value;
    }

    public IActionResult Index()
    {
        ViewData["Title"] = _settings.Title;
        ViewData["Updates"] = _settings.Updates;
        return View();
    }
}
```

## 추가 자료

* 컨트롤러에서 명시적으로 종속성을 요청하여 코드를 더 쉽게 테스트할 수 있는 방법에 대해 알아보려면 [Test controller logic in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/testing?view=aspnetcore-8.0)을 참조하십시오.
* [키드 서비스 종속성 주입 컨테이너 지원](https://andrewlock.net/exploring-the-dotnet-8-preview-keyed-services-dependency-injection-support/)
* [기본 종속성 주입 컨테이너를 타사 구현으로 교체](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0#default-service-container-replacement).

---
## 출처
[Dependency injection into controllers in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/dependency-injection?view=aspnetcore-8.0)

---
## [다음](./07_DI_View.md)
