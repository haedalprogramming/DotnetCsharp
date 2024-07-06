# ASP.NET Core fundamentals overview

## 목차
- [ASP.NET Core fundamentals overview](#aspnet-core-fundamentals-overview)
  - [목차](#목차)
- [ASP.NET Core 기본 사항 개요](#aspnet-core-기본-사항-개요)
  - [Program.cs](#programcs)
  - [의존성 주입(서비스)](#의존성-주입서비스)
  - [미들웨어](#미들웨어)
  - [호스트](#호스트)
    - [비웹 시나리오](#비웹-시나리오)
  - [서버](#서버)
  - [구성](#구성)
  - [환경](#환경)
  - [로깅](#로깅)
  - [라우팅](#라우팅)
  - [오류 처리](#오류-처리)
  - [HTTP 요청 보내기](#http-요청-보내기)
  - [콘텐츠 루트](#콘텐츠-루트)
  - [웹 루트](#웹-루트)
  - [추가 자료](#추가-자료)
  - [출처](#출처)
  - [다음](#다음)

---
# ASP.NET Core 기본 사항 개요


이 문서는 의존성 주입(DI), 구성, 미들웨어 등을 포함하여 ASP.NET Core 앱을 빌드하는 기본 사항에 대한 개요를 제공합니다.

## Program.cs

웹 템플릿으로 생성된 ASP.NET Core 앱에는 `Program.cs` 파일에 애플리케이션 시작 코드가 포함되어 있습니다. `Program.cs` 파일에서는 다음을 수행합니다:

* 앱에 필요한 서비스를 구성합니다.
* 앱의 요청 처리 파이프라인을 일련의 미들웨어 구성 요소로 정의합니다.

다음 앱 시작 코드는 다음을 지원합니다:

* Razor Pages
* 뷰가 있는 MVC 컨트롤러
* 컨트롤러가 있는 웹 API
* 최소 웹 API

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

## 의존성 주입(서비스)

ASP.NET Core는 구성된 서비스를 앱 전체에서 사용할 수 있게 하는 의존성 주입(DI)을 포함합니다. 서비스는 WebApplicationBuilder.Services, 즉 앞의 코드에서 `builder.Services`를 사용하여 DI 컨테이너에 추가됩니다. `WebApplicationBuilder`가 인스턴스화될 때, 많은 프레임워크 제공 서비스가 추가됩니다. `builder`는 다음 코드에서 `WebApplicationBuilder`입니다:

```C#
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

var app = builder.Build();
```

위의 강조된 코드에서 `builder`에는 구성, 로깅 및 다양한 다른 서비스가 DI 컨테이너에 추가됩니다.

다음 코드는 Razor Pages, 뷰가 있는 MVC 컨트롤러 및 사용자 지정 `DbContext`를 DI 컨테이너에 추가합니다:

```C#
using Microsoft.EntityFrameworkCore;
using RazorPagesMovie.Data;
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

builder.Services.AddDbContext<RazorPagesMovieContext>(options =>
   options.UseSqlServer(builder.Configuration.GetConnectionString("RPMovieContext")));

var app = builder.Build();
```

서비스는 일반적으로 생성자 주입을 통해 DI에서 해결됩니다. DI 프레임워크는 런타임에 이 서비스의 인스턴스를 제공합니다.

다음 코드는 생성자 주입을 사용하여 DI에서 데이터베이스 컨텍스트와 로거를 해결합니다:

```C#
public class IndexModel : PageModel
{
    private readonly RazorPagesMovieContext _context;
    private readonly ILogger<IndexModel> _logger;

    public IndexModel(RazorPagesMovieContext context, ILogger<IndexModel> logger)
    {
        _context = context;
        _logger = logger;
    }

    public IList<Movie> Movie { get;set; }

    public async Task OnGetAsync()
    {
        _logger.LogInformation("IndexModel OnGetAsync.");
        Movie = await _context.Movie.ToListAsync();
    }
}
```

## 미들웨어

요청 처리 파이프라인은 일련의 미들웨어 구성 요소로 구성됩니다. 각 구성 요소는 `HttpContext`에서 작업을 수행하고 파이프라인의 다음 미들웨어를 호출하거나 요청을 종료합니다.

관례에 따라 미들웨어 구성 요소는 `Use{Feature}` 확장 메서드를 호출하여 파이프라인에 추가됩니다. 다음 코드에서는 앱에 추가된 미들웨어를 강조 표시합니다:

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

## 호스트

시작 시 ASP.NET Core 앱은 *호스트*를 빌드합니다. 호스트는 다음과 같은 모든 앱 리소스를 캡슐화합니다:

* HTTP 서버 구현
* 미들웨어 구성 요소
* 로깅
* 의존성 주입(DI) 서비스
* 구성

ASP.NET Core 앱을 실행할 수 있는 세 가지 호스트가 있습니다:

* ASP.NET Core WebApplication, 최소 호스트라고도 함
* ASP.NET Core의 `ConfigureWebHostDefaults`와 결합된 .NET Generic Host
* ASP.NET Core WebHost

ASP.NET Core WebApplication 및 WebApplicationBuilder 유형은 모든 ASP.NET Core 템플릿에서 권장되고 사용됩니다. `WebApplication`은 .NET Generic Host와 유사하게 동작하며 많은 동일한 인터페이스를 노출하지만 구성에 더 적은 콜백이 필요합니다. ASP.NET Core WebHost는 하위 호환성만을 위해 사용할 수 있습니다.

다음 예제는 `WebApplication`을 인스턴스화합니다:

```C#
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

var app = builder.Build();
```

WebApplicationBuilder.Build 메서드는 다음과 같은 기본 옵션 세트로 호스트를 구성합니다:

* 웹 서버로 Kestrel 사용 및 IIS 통합 활성화.
* `appsettings.json`, 환경 변수, 명령줄 인수 및 기타 구성 소스에서 구성 로드.
* 콘솔 및 디버그 제공자에 로깅 출력 전송.

### 비웹 시나리오

Generic Host를 사용하면 로깅, 의존성 주입(DI), 구성 및 앱 수명 관리와 같은 교차 프레임워크 확장을 사용할 수 있습니다. 자세한 내용은 [.NET Generic Host in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-8.0) 및 [Background tasks with hosted services in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services?view=aspnetcore-8.0)를 참조하십시오.

## 서버

ASP.NET Core 앱은 HTTP 요청을 수신 대기하기 위해 HTTP 서버 구현을 사용합니다. 서버는 `HttpContext`로 구성된 일련의 요청 기능으로 앱에 요청을 제공합니다.

**Windows**

ASP.NET Core는 다음 서버 구현을 제공합니다:

* *Kestrel*은 크로스 플랫폼 웹 서버입니다. Kestrel은 종종 [IIS](https://www.iis.net/)를 사용하는 리버스 프록시 구성에서 실행됩니다. ASP.NET Core 2.0 이상에서는 Kestrel을 공용 엣지 서버로 직접 인터넷에 노출시켜 실행할 수 있습니다.
* *IIS HTTP 서버*는 IIS를 사용하는 Windows용 서버입니다. 이 서버를 사용하면 ASP.NET Core 앱과 IIS가 동일한 프로세스에서 실행됩니다.
* *HTTP.sys*는 IIS와 함께 사용되지 않는 Windows용 서버입니다.

**macOS**

ASP.NET Core는 *Kestrel* 크로스 플랫폼 서버 구현을 제공합니다. ASP.NET Core 2.0 이상에서는 Kestrel을 공용 엣지 서버로 직접 인터넷에 노출시켜 실행할 수 있습니다. Kestrel은 종종 [Nginx](https://nginx.org) 또는 [Apache](https://httpd.apache.org/)와 함께 리버스 프록시 구성에서 실행됩니다.

**Linux**

ASP.NET Core는 *Kestrel* 크로스 플랫폼 서버 구현을 제공합니다. ASP.NET Core 2.0 이상에서는 Kestrel을 공용 엣지 서버로 직접 인터넷에 노출시켜 실행할 수 있습니다. Kestrel은 종종 [Nginx](https://nginx.org) 또는 [Apache](https://httpd.apache.org/)와 함께 리버스 프록시 구성에서 실행됩니다.

---

## 구성

ASP.NET Core는 설정을 구성 공급자의 정렬된 집합에서 이름-값 쌍으로 가져오는 구성 프레임워크를 제공합니다. 내장된 구성 공급자는 `.json` 파일, `.xml` 파일, 환경 변수 및 명령줄 인수와 같은 다양한 소스에 대해 사용할 수 있습니다. 다른 소스를 지원하기 위해 사용자 지정 구성 공급자를 작성할 수 있습니다.

기본적으로, ASP.NET Core 앱은 `appsettings.json`, 환경 변수, 명령줄 등에서 읽도록 구성됩니다. 앱의 구성이 로드될 때, 환경 변수의 값은 `appsettings.json`의 값을 재정의합니다.

비밀번호와 같은 기밀 구성 데이터를 관리하기 위해 .NET Core는 비밀 관리자를 제공합니다. 프로덕션 비밀의 경우 Azure Key Vault를 권장합니다.

## 환경

`Development`, `Staging`, `Production`과 같은 실행 환경이 ASP.NET Core에서 제공됩니다. 앱이 실행되는 환경을 지정하려면 `ASPNETCORE_ENVIRONMENT` 환경 변수를 설정하십시오. ASP.NET Core는 앱 시작 시 이 환경 변수를 읽고 값을 `IWebHostEnvironment` 구현에 저장합니다. 이 구현은 의존성 주입(DI)을 통해 앱의 어디서나 사용할 수 있습니다.

다음 예제는 `Development` 환경이 아닐 때 예외 처리기 및 HTTP 엄격 전송 보안 프로토콜(HSTS) 미들웨어를 구성합니다:

```c#
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


## 로깅

ASP.NET Core는 다양한 내장 및 타사 로깅 제공자와 함께 작동하는 로깅 API를 지원합니다. 사용 가능한 제공자에는 다음이 포함됩니다:

* 콘솔
* 디버그
* Windows 이벤트 추적
* Windows 이벤트 로그
* TraceSource
* Azure App Service
* Azure Application Insights

로그를 생성하려면 의존성 주입(DI)에서  ILogger<TCategoryName> 서비스를 해결하고 LogInformation과 같은 로깅 메서드를 호출합니다. 예를 들어:

```C#
public class IndexModel : PageModel
{
    private readonly RazorPagesMovieContext _context;
    private readonly ILogger<IndexModel> _logger;

    public IndexModel(RazorPagesMovieContext context, ILogger<IndexModel> logger)
    {
        _context = context;
        _logger = logger;
    }

    public IList<Movie> Movie { get;set; }

    public async Task OnGetAsync()
    {
        _logger.LogInformation("IndexModel OnGetAsync.");
        Movie = await _context.Movie.ToListAsync();
    }
}
```

## 라우팅

*라우트*는 핸들러에 매핑된 URL 패턴입니다. 핸들러는 일반적으로 Razor 페이지, MVC 컨트롤러의 액션 메서드 또는 미들웨어입니다. ASP.NET Core 라우팅을 사용하면 앱에서 사용하는 URL을 제어할 수 있습니다.

ASP.NET Core 웹 애플리케이션 템플릿에서 생성된 다음 코드는 UseRouting를 호출합니다:

```
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddRazorPages();

var app = builder.Build();

// Configure the HTTP request pipeline.
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

## 오류 처리

ASP.NET Core에는 다음과 같은 오류 처리를 위한 내장 기능이 있습니다:

* 개발자 예외 페이지
* 사용자 지정 오류 페이지
* 정적 상태 코드 페이지
* 시작 예외 처리

## HTTP 요청 보내기

`HttpClient` 인스턴스를 생성하기 위한 `IHttpClientFactory` 구현이 제공됩니다. 팩토리는 다음과 같은 기능을 제공합니다:

* 논리적 `HttpClient` 인스턴스를 이름 지정하고 구성할 수 있는 중앙 위치를 제공합니다. 예를 들어, GitHub에 접근하기 위한 *github* 클라이언트를 등록하고 구성합니다. 다른 용도로 기본 클라이언트를 등록하고 구성합니다.
* 여러 위임 처리기를 등록하고 체이닝하여 아웃바운드 요청 미들웨어 파이프라인을 구축하는 것을 지원합니다. 이 패턴은 ASP.NET Core의 인바운드 미들웨어 파이프라인과 유사합니다. 이 패턴은 캐싱, 오류 처리, 직렬화 및 로깅을 포함한 HTTP 요청의 교차 문제를 관리할 수 있는 메커니즘을 제공합니다.
* 일시적인 오류 처리를 위한 인기 있는 타사 라이브러리인 *Polly*와 통합됩니다.
* `HttpClient` 수명을 수동으로 관리할 때 발생하는 일반적인 DNS 문제를 방지하기 위해 기본 `HttpClientHandler` 인스턴스의 풀링 및 수명을 관리합니다.
* 팩토리가 생성한 클라이언트를 통해 전송되는 모든 요청에 대해 구성 가능한 로깅 환경을 ILogger를 통해 추가합니다.


## 콘텐츠 루트

콘텐츠 루트는 다음의 기본 경로입니다:

* 앱을 호스팅하는 실행 파일(*.exe*).
* 앱을 구성하는 컴파일된 어셈블리(*.dll*).
* 앱에서 사용되는 콘텐츠 파일, 예:
  * Razor 파일(`.cshtml`, `.razor`)
  * 구성 파일(`.json`, `.xml`)
  * 데이터 파일(`.db`)
* 일반적으로 *wwwroot* 폴더인 [웹 루트](#web-root).

개발 중에는 콘텐츠 루트가 프로젝트의 루트 디렉토리로 기본 설정됩니다. 이 디렉토리는 또한 앱의 콘텐츠 파일과 웹 루트의 기본 경로입니다. 호스트를 빌드 할 때 경로를 설정하여 다른 콘텐츠 루트를 지정하십시오.

## 웹 루트

웹 루트는 공개된 정적 리소스 파일의 기본 경로입니다. 예를 들어:

* 스타일시트(`.css`)
* JavaScript(`.js`)
* 이미지(`.png`, `.jpg`)

기본적으로 정적 파일은 웹 루트 디렉토리와 하위 디렉토리에서만 제공됩니다. 웹 루트 경로는 기본적으로 *{content root}/wwwroot*입니다. 호스트를 빌드할 때 경로를 설정하여 다른 웹 루트를 지정하십시오.

프로젝트 파일에서 \<Content> 프로젝트 항목을 사용하여 *wwwroot*의 파일 게시를 방지하십시오. 다음 예제는 *wwwroot/local*과 그 하위 디렉토리의 콘텐츠 게시를 방지합니다:

```xml
<ItemGroup>
  <Content Update="wwwroot\local\**\*.*" CopyToPublishDirectory="Never" />
</ItemGroup>
```

Razor `.cshtml` 파일에서 `~/`는 웹 루트를 가리킵니다. `~/`로 시작하는 경로는 *가상 경로*라고 합니다.

## 추가 자료

* [WebApplicationBuilder 소스 코드](https://github.com/dotnet/aspnetcore/blob/v6.0.1/src/DefaultBuilder/src/WebApplicationBuilder.cs)

---
## 출처
[ASP.NET Core fundamentals overview](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-8.0&tabs=windows)

---
## [다음](./02_app_startup.md)
