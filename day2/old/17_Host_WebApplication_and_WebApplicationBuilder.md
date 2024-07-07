# WebApplication and WebApplicationBuilder in Minimal API apps


## 목차
- [WebApplication and WebApplicationBuilder in Minimal API apps](#webapplication-and-webapplicationbuilder-in-minimal-api-apps)
  - [목차](#목차)
  - [`WebApplication`](#webapplication)
    - [포트 작업](#포트-작업)
      - [여러 포트](#여러-포트)
      - [명령줄에서 포트 설정](#명령줄에서-포트-설정)
      - [환경 변수에서 포트 읽기](#환경-변수에서-포트-읽기)
      - [ASPNETCORE\_URLS 환경 변수를 통해 포트 설정](#aspnetcore_urls-환경-변수를-통해-포트-설정)
    - [모든 인터페이스에서 수신 대기](#모든-인터페이스에서-수신-대기)
      - [http://\*:3000](#http3000)
      - [http://+:3000](#http3000-1)
      - [`http://0.0.0.0:3000`](#http00003000)
    - [ASPNETCORE\_URLS를 사용하여 모든 인터페이스에서 수신 대기](#aspnetcore_urls를-사용하여-모든-인터페이스에서-수신-대기)
    - [ASPNETCORE\_HTTPS\_PORTS를 사용하여 모든 인터페이스에서 수신 대기](#aspnetcore_https_ports를-사용하여-모든-인터페이스에서-수신-대기)
    - [개발 인증서를 사용하여 HTTPS 지정](#개발-인증서를-사용하여-https-지정)
    - [사용자 지정 인증서를 사용하여 HTTPS 지정](#사용자-지정-인증서를-사용하여-https-지정)
      - [`appsettings.json`을 사용하여 사용자 지정 인증서 지정](#appsettingsjson을-사용하여-사용자-지정-인증서-지정)
      - [구성을 통해 사용자 지정 인증서 지정](#구성을-통해-사용자-지정-인증서-지정)
      - [인증서 API 사용](#인증서-api-사용)
    - [환경 읽기](#환경-읽기)
    - [구성](#구성)
    - [로깅](#로깅)
    - [종속성 주입 (DI) 컨테이너에 접근](#종속성-주입-di-컨테이너에-접근)
  - [WebApplicationBuilder](#webapplicationbuilder)
    - [콘텐츠 루트, 애플리케이션 이름 및 환경 변경](#콘텐츠-루트-애플리케이션-이름-및-환경-변경)
    - [환경 변수 또는 명령줄을 사용하여 콘텐츠 루트, 앱 이름 및 환경 변경](#환경-변수-또는-명령줄을-사용하여-콘텐츠-루트-앱-이름-및-환경-변경)
    - [구성 공급자 추가](#구성-공급자-추가)
    - [구성 읽기](#구성-읽기)
    - [환경 읽기](#환경-읽기-1)
    - [로깅 공급자 추가](#로깅-공급자-추가)
    - [서비스 추가](#서비스-추가)
    - [IHostBuilder 사용자 지정](#ihostbuilder-사용자-지정)
    - [IWebHostBuilder 사용자 지정](#iwebhostbuilder-사용자-지정)
    - [웹 루트 변경](#웹-루트-변경)
    - [사용자 지정 종속성 주입 (DI) 컨테이너](#사용자-지정-종속성-주입-di-컨테이너)
    - [미들웨어 추가](#미들웨어-추가)
    - [개발자 예외 페이지](#개발자-예외-페이지)
  - [출처](#출처)
  - [다음](#다음)

---
## `WebApplication`

다음 코드는 ASP.NET Core 템플릿에 의해 생성된 것입니다:

```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```

위 코드는 명령줄에서 `dotnet new web`을 실행하거나 Visual Studio에서 빈 웹 템플릿을 선택하여 생성할 수 있습니다.

다음 코드는 `WebApplication` (`app`)을 명시적으로 `WebApplicationBuilder`를 생성하지 않고 만듭니다:

```C#
var app = WebApplication.Create(args);

app.MapGet("/", () => "Hello World!");

app.Run();
```

[`WebApplication.Create`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplication.create)는 미리 구성된 기본값으로 `WebApplication` 클래스의 새 인스턴스를 초기화합니다.

### 포트 작업

Visual Studio 또는 `dotnet new`를 사용하여 웹 앱을 만들면 앱이 응답할 포트를 지정하는 `Properties/launchSettings.json` 파일이 생성됩니다. 다음의 포트 설정 샘플에서는 Visual Studio에서 앱을 실행할 때 `Unable to connect to web server 'AppName'` 오류 대화 상자가 반환됩니다. Visual Studio는 `Properties/launchSettings.json`에 지정된 포트를 기대하고 있지만 앱은 `app.Run("http://localhost:3000")`에서 지정한 포트를 사용하고 있습니다. 다음의 포트 변경 샘플을 명령줄에서 실행하십시오.

다음 섹션에서는 앱이 응답할 포트를 설정합니다.

```C#
var app = WebApplication.Create(args);

app.MapGet("/", () => "Hello World!");

app.Run("http://localhost:3000");
```

위 코드에서는 앱이 포트 `3000`에 응답합니다.

#### 여러 포트

다음 코드에서는 앱이 포트 `3000`과 `4000`에 응답합니다.

```C#
var app = WebApplication.Create(args);

app.Urls.Add("http://localhost:3000");
app.Urls.Add("http://localhost:4000");

app.MapGet("/", () => "Hello World");

app.Run();
```

#### 명령줄에서 포트 설정

다음 명령은 앱이 포트 `7777`에 응답하도록 만듭니다:

```dotnetcli
dotnet run --urls="https://localhost:7777"
```

`appsettings.json` 파일에서 Kestrel 엔드포인트가 구성된 경우, `appsettings.json` 파일에 지정된 URL이 사용됩니다. 자세한 내용은 [Kestrel 엔드포인트 구성](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0#kestrel)을 참조하십시오.

#### 환경 변수에서 포트 읽기

다음 코드는 환경 변수에서 포트를 읽습니다:

```C#
var app = WebApplication.Create(args);

var port = Environment.GetEnvironmentVariable("PORT") ?? "3000";

app.MapGet("/", () => "Hello World");

app.Run($"http://localhost:{port}");
```

환경 변수에서 포트를 설정하는 선호 방법은 다음 섹션에 표시된 `ASPNETCORE_URLS` 환경 변수를 사용하는 것입니다.

#### ASPNETCORE_URLS 환경 변수를 통해 포트 설정

`ASPNETCORE_URLS` 환경 변수를 사용하여 포트를 설정할 수 있습니다:

```
ASPNETCORE_URLS=http://localhost:3000
```

`ASPNETCORE_URLS`는 여러 URL을 지원합니다:

```
ASPNETCORE_URLS=http://localhost:3000;https://localhost:5000
```

### 모든 인터페이스에서 수신 대기

다음 샘플은 모든 인터페이스에서 수신 대기하는 방법을 보여줍니다.

#### http://*:3000

```C#
var app = WebApplication.Create(args);

app.Urls.Add("http://*:3000");

app.MapGet("/", () => "Hello World");

app.Run();
```

#### http://+:3000

```C#
var app = WebApplication.Create(args);

app.Urls.Add("http://+:3000");

app.MapGet("/", () => "Hello World");

app.Run();
```

#### `http://0.0.0.0:3000`

```C#
var app = WebApplication.Create(args);

app.Urls.Add("http://0.0.0.0:3000");

app.MapGet("/", () => "Hello World");

app.Run();
```

### ASPNETCORE_URLS를 사용하여 모든 인터페이스에서 수신 대기

앞의 샘플은 `ASPNETCORE_URLS`를 사용할 수 있습니다:

```
ASPNETCORE_URLS=http://*:3000;https://+:5000;http://0.0.0.0:5005
```

### ASPNETCORE_HTTPS_PORTS를 사용하여 모든 인터페이스에서 수신 대기

앞의 샘플은 `ASPNETCORE_HTTPS_PORTS`와 `ASPNETCORE_HTTP_PORTS`를 사용할 수 있습니다.

```
ASPNETCORE_HTTP_PORTS=3000;5005
ASPNETCORE_HTTPS_PORTS=5000
```

자세한 내용은 [ASP.NET Core Kestrel 웹 서버의 엔드포인트 구성](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel/endpoints?view=aspnetcore-8.0)을 참조하십시오.

### 개발 인증서를 사용하여 HTTPS 지정

```C#
var app = WebApplication.Create(args);

app.Urls.Add("https://localhost:3000");

app.MapGet("/", () => "Hello World");

app.Run();
```

개발 인증서에 대한 자세한 내용은 [Windows 및 macOS에서 ASP.NET Core HTTPS 개발 인증서 신뢰](https://learn.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-8.0#trust)를 참조하십시오.

### 사용자 지정 인증서를 사용하여 HTTPS 지정

다음 섹션에서는 `appsettings.json` 파일과 구성을 통해 사용자 지정 인증서를 지정하는 방법을 보여줍니다.

#### `appsettings.json`을 사용하여 사용자 지정 인증서 지정

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "cert.pem",
        "KeyPath": "key.pem"
      }
    }
  }
}
```

#### 구성을 통해 사용자 지정 인증서 지정

```C#
var builder = WebApplication.CreateBuilder(args);

// Configure the cert and the key
builder.Configuration["Kestrel:Certificates:Default:Path"] = "cert.pem";
builder.Configuration["Kestrel:Certificates:Default:KeyPath"] = "key.pem";

var app = builder.Build();

app.Urls.Add("https://localhost:3000");

app.MapGet("/", () => "Hello World");

app.Run();
```

#### 인증서 API 사용

```C#
using System.Security.Cryptography.X509Certificates;

var builder = WebApplication.CreateBuilder(args);

builder.WebHost.ConfigureKestrel(options =>
{
    options.ConfigureHttpsDefaults(httpsOptions =>
    {
        var certPath = Path.Combine(builder.Environment.ContentRootPath, "cert.pem");
        var keyPath = Path.Combine(builder.Environment.ContentRootPath, "key.pem");

        httpsOptions.ServerCertificate = X509Certificate2.CreateFromPemFile(certPath, 
                                         keyPath);
    });
});

var app = builder.Build();

app.Urls.Add("https://localhost:3000");

app.MapGet("/", () => "Hello World");

app.Run();
```

### 환경 읽기

```C#
var app = WebApplication.Create(args);

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/oops");
}

app.MapGet("/", () => "Hello World");
app.MapGet("/oops", () => "Oops! An error happened.");

app.Run();
```

환경 사용에 대한 자세한 내용은 [Use multiple environments in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/environments?view=aspnetcore-8.0)를 참조하십시오.

### 구성

다음 코드는 구성 시스템에서 읽습니다:

```C#
var app = WebApplication.Create(args);

var message = app.Configuration["HelloKey"] ?? "Config failed!";

app.MapGet("/", () => message);

app.Run();
```

자세한 내용은 [Configuration in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0)를 참조하십시오.

### 로깅

다음 코드는 애플리케이션 시작 시 로그에 메시지를 기록합니다:

```C#
var app = WebApplication.Create(args);

app.Logger.LogInformation("The app started");

app.MapGet("/", () => "Hello World");

app.Run();
```

자세한 내용은 [Logging in .NET Core and ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-8.0)를 참조하십시오.

### 종속성 주입 (DI) 컨테이너에 접근

다음 코드는 애플리케이션 시작 시 DI 컨테이너에서 서비스를 가져오는 방법을 보여줍니다:

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddScoped<SampleService>();

var app = builder.Build();

app.MapControllers();

using (var scope = app.Services.CreateScope())
{
    var sampleService = scope.ServiceProvider.GetRequiredService<SampleService>();
    sampleService.DoSomething();
}

app.Run();
```

다음 코드는 [`[FromKeyedServices]`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.fromkeyedservicesattribute) 특성을 사용하여 DI 컨테이너에서 키를 사용하는 방법을 보여줍니다:

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddKeyedSingleton<ICache, BigCache>("big");
builder.Services.AddKeyedSingleton<ICache, SmallCache>("small");

var app = builder.Build();

app.MapGet("/big", ([FromKeyedServices("big")] ICache bigCache) => bigCache.Get("date"));

app.MapGet("/small", ([FromKeyedServices("small")] ICache smallCache) => smallCache.Get("date"));

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
```

DI에 대한 자세한 내용은 [Dependency injection in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 참조하십시오.

---
## WebApplicationBuilder

이 섹션에는 `WebApplicationBuilder`를 사용하는 샘플 코드가 포함되어 있습니다.

### 콘텐츠 루트, 애플리케이션 이름 및 환경 변경

다음 코드는 콘텐츠 루트, 애플리케이션 이름 및 환경을 설정합니다:

```C#
var builder = WebApplication.CreateBuilder(new WebApplicationOptions
{
    Args = args,
    ApplicationName = typeof(Program).Assembly.FullName,
    ContentRootPath = Directory.GetCurrentDirectory(),
    EnvironmentName = Environments.Staging,
    WebRootPath = "customwwwroot"
});

Console.WriteLine($"Application Name: {builder.Environment.ApplicationName}");
Console.WriteLine($"Environment Name: {builder.Environment.EnvironmentName}");
Console.WriteLine($"ContentRoot Path: {builder.Environment.ContentRootPath}");
Console.WriteLine($"WebRootPath: {builder.Environment.WebRootPath}");

var app = builder.Build();
```

`WebApplication.CreateBuilder`는 미리 구성된 기본값으로 `WebApplicationBuilder` 클래스의 새 인스턴스를 초기화합니다.

자세한 내용은 [ASP.NET Core fundamentals overview](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-8.0)를 참조하십시오.

### 환경 변수 또는 명령줄을 사용하여 콘텐츠 루트, 앱 이름 및 환경 변경

다음 표는 콘텐츠 루트, 앱 이름 및 환경을 변경하는 데 사용되는 환경 변수와 명령줄 인수를 보여줍니다:

| 기능   | 환경 변수 | 명령줄 인수 |
| ------------- | ------------- | -- |
| 애플리케이션 이름 | ASPNETCORE

_APPLICATIONNAME  | --applicationName |
| 환경 이름 |  ASPNETCORE_ENVIRONMENT | --environment |
| 콘텐츠 루트  | ASPNETCORE_CONTENTROOT  | --contentRoot |

### 구성 공급자 추가

다음 샘플은 INI 구성 공급자를 추가합니다:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Configuration.AddIniFile("appsettings.ini");

var app = builder.Build();
```

자세한 내용은 [Configuration in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0)의 [파일 구성 공급자](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0#file-configuration-provider)를 참조하십시오.

### 구성 읽기

기본적으로 `WebApplicationBuilder`는 다음을 포함하여 여러 소스에서 구성을 읽습니다:

* `appSettings.json` 및 `appSettings.{environment}.json`
* 환경 변수
* 명령줄

읽은 구성 소스의 전체 목록은 [Configuration in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0)의 [기본 구성](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0#default-configuration)을 참조하십시오.

다음 코드는 구성에서 `HelloKey`를 읽고 `/` 엔드포인트에서 값을 표시합니다. 구성 값이 null이면 "Hello"가 `message`에 할당됩니다:

```C#
var builder = WebApplication.CreateBuilder(args);

var message = builder.Configuration["HelloKey"] ?? "Hello";

var app = builder.Build();

app.MapGet("/", () => message);

app.Run();
```

### 환경 읽기

```C#
var builder = WebApplication.CreateBuilder(args);

if (builder.Environment.IsDevelopment())
{
    Console.WriteLine($"Running in development.");
}

var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```

### 로깅 공급자 추가

```C#
var builder = WebApplication.CreateBuilder(args);

// Configure JSON logging to the console.
builder.Logging.AddJsonConsole();

var app = builder.Build();

app.MapGet("/", () => "Hello JSON console!");

app.Run();
```

### 서비스 추가

```C#
var builder = WebApplication.CreateBuilder(args);

// Add the memory cache services.
builder.Services.AddMemoryCache();

// Add a custom scoped service.
builder.Services.AddScoped<ITodoRepository, TodoRepository>();
var app = builder.Build();
```

### IHostBuilder 사용자 지정

기존의 `IHostBuilder`에 대한 확장 메서드는 [Host 속성](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.ihostbuilder.properties#microsoft-extensions-hosting-ihostbuilder-properties)을 사용하여 접근할 수 있습니다:

```C#
var builder = WebApplication.CreateBuilder(args);

// Wait 30 seconds for graceful shutdown.
builder.Host.ConfigureHostOptions(o => o.ShutdownTimeout = TimeSpan.FromSeconds(30));

var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```

### IWebHostBuilder 사용자 지정

`IWebHostBuilder`에 대한 확장 메서드는 [WebApplicationBuilder.WebHost](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder.webhost#microsoft-aspnetcore-builder-webapplicationbuilder-webhost) 속성을 사용하여 접근할 수 있습니다.

```C#
var builder = WebApplication.CreateBuilder(args);

// Change the HTTP server implemenation to be HTTP.sys based
builder.WebHost.UseHttpSys();

var app = builder.Build();

app.MapGet("/", () => "Hello HTTP.sys");

app.Run();
```

### 웹 루트 변경

기본적으로 웹 루트는 `wwwroot` 폴더의 콘텐츠 루트를 기준으로 상대적입니다. 웹 루트는 정적 파일 미들웨어가 정적 파일을 찾는 위치입니다. 웹 루트는 `WebHostOptions`, 명령줄 또는 `UseWebRoot` 메서드를 사용하여 변경할 수 있습니다:

```C#
var builder = WebApplication.CreateBuilder(new WebApplicationOptions
{
    Args = args,
    // Look for static files in webroot
    WebRootPath = "webroot"
});

var app = builder.Build();

app.Run();
```

### 사용자 지정 종속성 주입 (DI) 컨테이너

다음 예제는 [Autofac](https://autofac.readthedocs.io/en/latest/integration/aspnetcore.html)를 사용합니다:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Host.UseServiceProviderFactory(new AutofacServiceProviderFactory());

// 여기에서 직접 Autofac에 서비스를 등록합니다. builder.Populate()를 호출하지 마십시오. 이는 AutofacServiceProviderFactory에서 처리됩니다.
builder.Host.ConfigureContainer<ContainerBuilder>(builder => builder.RegisterModule(new MyApplicationModule()));

var app = builder.Build();
```

### 미들웨어 추가

기존의 모든 ASP.NET Core 미들웨어는 `WebApplication`에 구성할 수 있습니다:

```C#
var app = WebApplication.Create(args);

// Setup the file server to serve static files.
app.UseFileServer();

app.MapGet("/", () => "Hello World!");

app.Run();
```

자세한 내용은 [ASP.NET Core Middleware](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0)를 참조하십시오.

### 개발자 예외 페이지

`WebApplication.CreateBuilder`는 미리 구성된 기본값으로 `WebApplicationBuilder` 클래스의 새 인스턴스를 초기화합니다. 개발자 예외 페이지는 미리 구성된 기본값에 포함되어 있습니다. 다음 코드가 [개발 환경](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/environments?view=aspnetcore-8.0)에서 실행될 때, `/`로 이동하면 예외를 보여주는 친절한 페이지가 렌더링됩니다.

```C#
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.MapGet("/", () =>
{
    throw new InvalidOperationException("Oops, the '/' route has thrown an exception.");
});

app.Run();
```

---
## 출처
[WebApplication and WebApplicationBuilder in Minimal API apps](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis/webapplication?view=aspnetcore-8.0)

---
## [다음](./18)
