# App startup in ASP.NET Core

## 목차
- [App startup in ASP.NET Core](#app-startup-in-aspnet-core)
  - [목차](#목차)
  - [시작 필터로 시작 확장](#시작-필터로-시작-확장)
  - [외부 어셈블리에서 시작 시 구성 추가](#외부-어셈블리에서-시작-시-구성-추가)
  - [시작, ConfigureServices, 및 Configure](#시작-configureservices-및-configure)
  - [출처](#출처)
  - [다음](#다음)

---

ASP.NET Core 웹 템플릿으로 생성된 앱에는 `Program.cs` 파일에 애플리케이션 시작 코드가 포함되어 있습니다.

다음의 앱 시작 코드는 다음을 지원합니다:

* Razor Pages
* 뷰가 있는 MVC 컨트롤러
* 컨트롤러가 있는 웹 API
* 최소 API

```C#
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseAuthorization();

app.MapGet("/hi", () => "Hello!");

app.MapDefaultControllerRoute();
app.MapRazorPages();

app.Run();
```

EventSource를 사용하는 앱은 시작 시간을 측정하여 시작 성능을 이해하고 최적화할 수 있습니다. Microsoft.AspNetCore.Hosting의 `ServerReady` 이벤트는 서버가 요청에 응답할 준비가 된 시점을 나타냅니다.

## 시작 필터로 시작 확장

다음과 같은 경우 IStartupFilter를 사용하십시오:

* `Use{Middleware}`를 명시적으로 호출하지 않고 앱의 미들웨어 파이프라인의 시작 또는 끝에서 미들웨어를 구성합니다. `IStartupFilter`를 사용하여 기본 미들웨어를 명시적으로 등록하지 않고 파이프라인의 시작 부분에 기본값을 추가할 수 있습니다. `IStartupFilter`를 사용하면 다른 구성 요소가 앱 작성자를 대신하여 `Use{Middleware}`를 호출할 수 있습니다.
* `Configure` 메서드의 파이프라인을 생성합니다. IStartupFilter.Configure는 라이브러리에 의해 추가된 미들웨어 전후에 실행될 미들웨어를 설정할 수 있습니다.

`IStartupFilter`는 `Action<IApplicationBuilder>`를 수신하고 반환하는 Configure를 구현합니다. IApplicationBuilder는 앱의 요청 파이프라인을 구성하기 위한 클래스를 정의합니다.

각 `IStartupFilter`는 요청 파이프라인에서 하나 이상의 미들웨어를 추가할 수 있습니다. 필터는 서비스 컨테이너에 추가된 순서대로 호출됩니다. 필터는 다음 필터에 제어를 전달하기 전에 또는 후에 미들웨어를 추가할 수 있으므로 앱 파이프라인의 시작 또는 끝에 추가됩니다.

다음 예제는 `IStartupFilter`로 미들웨어를 등록하는 방법을 보여줍니다. `RequestSetOptionsMiddleware` 미들웨어는 쿼리 문자열 매개변수에서 옵션 값을 설정합니다:

```c#
public class RequestSetOptionsMiddleware
{
    private readonly RequestDelegate _next;

    public RequestSetOptionsMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    // Test with https://localhost:5001/Privacy/?option=Hello
    public async Task Invoke(HttpContext httpContext)
    {
        var option = httpContext.Request.Query["option"];

        if (!string.IsNullOrWhiteSpace(option))
        {
            httpContext.Items["option"] = WebUtility.HtmlEncode(option);
        }

        await _next(httpContext);
    }
}
```

`RequestSetOptionsMiddleware`는 `RequestSetOptionsStartupFilter` 클래스에서 구성됩니다:

```c#
namespace WebStartup.Middleware;
// <snippet1>
public class RequestSetOptionsStartupFilter : IStartupFilter
{
    public Action<IApplicationBuilder> Configure(Action<IApplicationBuilder> next)
    {
        return builder =>
        {
            builder.UseMiddleware<RequestSetOptionsMiddleware>();
            next(builder);
        };
    }
}
// </snippet1>
```

`IStartupFilter`는 `Program.cs`에서 등록됩니다:

```c#
using WebStartup.Middleware;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddRazorPages();
builder.Services.AddTransient<IStartupFilter,
                      RequestSetOptionsStartupFilter>();

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapRazorPages();

app.Run();
```

쿼리 문자열 매개변수로 `option`이 제공되면, 미들웨어는 ASP.NET Core 미들웨어가 응답을 렌더링하기 전에 값 할당을 처리합니다:

```CSHTML
@page
@model PrivacyModel
@{
    ViewData["Title"] = "Privacy Policy";
}
<h1>@ViewData["Title"]</h1>

<p> Append query string ?option=hello</p>
Option String: @HttpContext.Items["option"];
```

미들웨어 실행 순서는 `IStartupFilter` 등록 순서에 의해 설정됩니다:

* 여러 `IStartupFilter` 구현이 동일한 객체와 상호 작용할 수 있습니다. 순서가 중요한 경우, 미들웨어가 실행될 순서에 맞게 `IStartupFilter` 서비스 등록 순서를 정렬하십시오.
* 라이브러리는 하나 이상의 `IStartupFilter` 구현으로 미들웨어를 추가할 수 있으며, 이는 `IStartupFilter`로 등록된 다른 앱 미들웨어 전후에 실행됩니다. 라이브러리의 `IStartupFilter`가 추가한 미들웨어 전에 `IStartupFilter` 미들웨어를 호출하려면:

  * 서비스 등록을 라이브러리가 서비스 컨테이너에 추가되기 전에 위치시킵니다.
  * 이후에 호출하려면 서비스 등록을 라이브러리가 추가된 후에 위치시킵니다.

참고: `Configure`를 재정의할 때 ASP.NET Core 앱을 확장할 수 없습니다. 자세한 내용은 [이 GitHub 이슈](https://github.com/dotnet/aspnetcore/issues/45372)를 참조하십시오.

## 외부 어셈블리에서 시작 시 구성 추가

`IHostingStartup` 구현을 사용하면 앱의 `Program.cs` 파일 외부의 외부 어셈블리에서 앱을 시작할 때 개선 사항을 추가할 수 있습니다. 자세한 내용은 [Use hosting startup assemblies in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/platform-specific-configuration?view=aspnetcore-8.0)를 참조하십시오.

## 시작, ConfigureServices, 및 Configure

최소 호스팅 모델에서 ConfigureServices 및 Configure 메서드를 사용하는 방법에 대한 자세한 내용은 다음을 참조하십시오:

* [최소 호스팅 모델에서 Startup 사용]([xref:migration/50-to-60#smhm](https://learn.microsoft.com/en-us/aspnet/core/migration/50-to-60?view=aspnetcore-8.0#smhm))
* [이 문서의 ASP.NET Core 5.0 버전]([?view=aspnetcore-5.0&preserve-view=true#the-startup-class](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/startup?view=aspnetcore-5.0&preserve-view=true#the-startup-class)):
  * [ConfigureServices 메서드]([?view=aspnetcore-5.0&preserve-view=true#the-configureservices-method](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/startup?view=aspnetcore-5.0&preserve-view=true#the-configureservices-method))
  * [Configure 메서드]([?view=aspnetcore-5.0&preserve-view=true#the-configure-method](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/startup?view=aspnetcore-5.0&preserve-view=true#the-configure-method))

---
## 출처
[App startup in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/startup?view=aspnetcore-8.0)

---
## [다음](./03_Dependency_injection.md)
