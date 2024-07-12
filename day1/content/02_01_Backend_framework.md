# 백엔드 프레임워크의 기능과 ASP.NET Core 예제

## 목차
- [백엔드 프레임워크의 기능과 ASP.NET Core 예제](#백엔드-프레임워크의-기능과-aspnet-core-예제)
  - [목차](#목차)
  - [소개](#소개)
  - [1. 백엔드 프레임워크의 주요 기능](#1-백엔드-프레임워크의-주요-기능)
    - [1.1 라우팅](#11-라우팅)
    - [1.2 컨트롤러와 액션](#12-컨트롤러와-액션)
    - [1.3 모델 바인딩](#13-모델-바인딩)
    - [1.4 데이터베이스 연동](#14-데이터베이스-연동)
    - [1.5 유효성 검사](#15-유효성-검사)
    - [1.6 의존성 주입(DI)](#16-의존성-주입di)
    - [1.7 미들웨어](#17-미들웨어)
    - [1.8 인증 및 권한 부여](#18-인증-및-권한-부여)
    - [1.9 로깅](#19-로깅)
  - [2. ASP.NET Core 소개](#2-aspnet-core-소개)
    - [2.1 ASP.NET Core 개요](#21-aspnet-core-개요)
    - [2.2 ASP.NET Core의 주요 기능](#22-aspnet-core의-주요-기능)
  - [3. ASP.NET Core 예제](#3-aspnet-core-예제)
    - [3.1 프로젝트 생성](#31-프로젝트-생성)
    - [3.2 컨트롤러 작성](#32-컨트롤러-작성)
      - [`WeatherForecastController.cs`](#weatherforecastcontrollercs)
    - [3.3 모델 작성](#33-모델-작성)
      - [`WeatherForecast.cs`](#weatherforecastcs)
    - [3.4 데이터베이스 연동](#34-데이터베이스-연동)
      - [`ApplicationDbContext.cs`](#applicationdbcontextcs)
      - [`appsettings.json`](#appsettingsjson)
      - [`Startup.cs`](#startupcs)
    - [3.5 의존성 주입](#35-의존성-주입)
      - [`Startup.cs`](#startupcs-1)
      - [`IWeatherForecastService.cs`](#iweatherforecastservicecs)
      - [`WeatherForecastService.cs`](#weatherforecastservicecs)
    - [3.6 유효성 검사](#36-유효성-검사)
      - [`WeatherForecast.cs`](#weatherforecastcs-1)
    - [3.7 미들웨어](#37-미들웨어)
      - [`Startup.cs`](#startupcs-2)
    - [3.8 인증 및 권한 부여](#38-인증-및-권한-부여)
      - [`Startup.cs`](#startupcs-3)
    - [3.9 로깅](#39-로깅)
      - [`WeatherForecastController.cs`](#weatherforecastcontrollercs-1)
  - [결론](#결론)
  - [출처](#출처)
  - [다음](#다음)

---

## 소개
백엔드 프레임워크는 웹 애플리케이션의 서버 측 로직을 구현하는 데 필요한 도구와 기능을 제공합니다. 이 문서에서는 백엔드 프레임워크가 지원하는 주요 기능들을 소개하고, ASP.NET Core를 예시로 설명합니다.

## 1. 백엔드 프레임워크의 주요 기능

### 1.1 라우팅
클라이언트 요청을 적절한 컨트롤러와 액션 메서드로 라우팅합니다.
- **경로 매핑**: URL 경로를 컨트롤러 메서드와 매핑.
- **동적 라우팅**: 다양한 URL 패턴을 지원.

### 1.2 컨트롤러와 액션
웹 애플리케이션의 주요 로직을 처리하는 컨트롤러와 액션 메서드를 제공합니다.
- **컨트롤러**: 요청을 처리하고 응답을 생성하는 클래스.
- **액션 메서드**: 컨트롤러 내에서 특정 요청을 처리하는 메서드.

### 1.3 모델 바인딩
클라이언트의 요청 데이터를 자동으로 모델 객체에 바인딩합니다.
- **폼 데이터**: 폼 데이터를 모델 객체에 바인딩.
- **쿼리 스트링**: URL의 쿼리 스트링 데이터를 모델 객체에 바인딩.

### 1.4 데이터베이스 연동
데이터베이스와의 상호작용을 위한 ORM(Object-Relational Mapping)을 지원합니다.
- **Entity Framework Core**: .NET용 ORM 프레임워크.
- **LINQ**: 데이터베이스 쿼리를 작성하기 위한 언어 통합 쿼리.

### 1.5 유효성 검사
모델 데이터를 검증하는 유효성 검사 기능을 제공합니다.
- **데이터 주석**: 모델 속성에 대한 유효성 검사 특성.
- **커스텀 유효성 검사**: 사용자 정의 유효성 검사 로직.

### 1.6 의존성 주입(DI)
객체 간의 의존성을 관리하고 주입하는 기능을 제공합니다.
- **서비스 등록**: 의존성을 DI 컨테이너에 등록.
- **서비스 주입**: 생성자 또는 메서드 주입을 통해 서비스 주입.

### 1.7 미들웨어
요청 파이프라인에서 요청과 응답을 처리하는 미들웨어를 지원합니다.
- **요청 처리**: 요청을 처리하고 다음 미들웨어로 전달.
- **응답 처리**: 응답을 처리하고 클라이언트에 전달.

### 1.8 인증 및 권한 부여
사용자 인증과 권한 부여를 처리하는 기능을 제공합니다.
- **쿠키 인증**: 쿠키 기반 인증.
- **JWT 인증**: JSON Web Token을 사용한 인증.
- **역할 기반 권한 부여**: 사용자 역할에 따른 권한 부여.

### 1.9 로깅
애플리케이션의 로깅을 지원하여 문제를 진단하고 추적합니다.
- **로그 레벨**: 다양한 로그 레벨(정보, 경고, 오류 등) 지원.
- **로그 출력**: 파일, 콘솔, 데이터베이스 등 다양한 출력 대상.

## 2. ASP.NET Core 소개

### 2.1 ASP.NET Core 개요
- **ASP.NET Core**는 마이크로소프트에서 개발한 오픈 소스, 크로스 플랫폼 웹 프레임워크입니다.
- **고성능**: 높은 성능과 확장성을 제공합니다.
- **모듈화**: 필요에 따라 구성 요소를 추가하거나 제거할 수 있습니다.

### 2.2 ASP.NET Core의 주요 기능
- **컨트롤러와 라우팅**: MVC 아키텍처를 기반으로 한 라우팅 및 컨트롤러.
- **의존성 주입**: 내장된 DI 컨테이너를 통한 의존성 관리.
- **데이터베이스 연동**: Entity Framework Core를 통한 데이터베이스 연동.
- **유효성 검사**: 데이터 주석을 통한 모델 유효성 검사.
- **미들웨어**: 요청 파이프라인을 구성하는 미들웨어.
- **인증 및 권한 부여**: 다양한 인증 및 권한 부여 메커니즘.
- **로깅**: 통합된 로깅 시스템.

## 3. ASP.NET Core 예제

### 3.1 프로젝트 생성
```bash
dotnet new webapi -o MyApi
cd MyApi
dotnet run
```
- **`dotnet new webapi`**: 새로운 ASP.NET Core Web API 프로젝트 생성.
- **`dotnet run`**: 애플리케이션 실행.

### 3.2 컨트롤러 작성
ASP.NET Core에서 컨트롤러는 클라이언트 요청을 처리하는 클래스입니다.

#### `WeatherForecastController.cs`
```csharp
using Microsoft.AspNetCore.Mvc;

namespace MyApi.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        [HttpGet]
        public IEnumerable<WeatherForecast> Get()
        {
            return Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateTime.Now.AddDays(index),
                TemperatureC = Random.Shared.Next(-20, 55),
                Summary = Summaries[Random.Shared.Next(Summaries.Length)]
            })
            .ToArray();
        }
    }
}
```

### 3.3 모델 작성
ASP.NET Core에서 모델은 데이터를 정의하는 클래스입니다.

#### `WeatherForecast.cs`
```csharp
namespace MyApi
{
    public class WeatherForecast
    {
        public DateTime Date { get; set; }
        public int TemperatureC { get; set; }
        public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
        public string Summary { get; set; }
    }
}
```

### 3.4 데이터베이스 연동
Entity Framework Core를 사용하여 데이터베이스와 상호작용합니다.

#### `ApplicationDbContext.cs`
```csharp
using Microsoft.EntityFrameworkCore;

namespace MyApi
{
    public class ApplicationDbContext : DbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        public DbSet<WeatherForecast> WeatherForecasts { get; set; }
    }
}
```

#### `appsettings.json`
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=MyApiDb;Trusted_Connection=True;MultipleActiveResultSets=true"
  },
  ...
}
```

#### `Startup.cs`
```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddControllers();
}
```

### 3.5 의존성 주입
ASP.NET Core는 의존성 주입을 기본적으로 지원합니다.

#### `Startup.cs`
```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddScoped<IWeatherForecastService, WeatherForecastService>();

    services.AddControllers();
}
```

#### `IWeatherForecastService.cs`
```csharp
using System.Collections.Generic;

namespace MyApi
{
    public interface IWeatherForecastService
    {
        IEnumerable<WeatherForecast> GetForecasts();
    }
}
```

#### `WeatherForecastService.cs`
```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace MyApi
{
    public class WeatherForecastService : IWeatherForecastService
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        public IEnumerable<WeatherForecast> GetForecasts()
        {
            return Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateTime.Now.AddDays(index),
                TemperatureC = Random.Shared.Next(-20, 55),
                Summary = Summaries[Random.Shared.Next(Summaries.Length)]
            })
            .ToArray();
        }
    }
}
```

### 3.6 유효성 검사
ASP.NET Core는 데이터 주석을 사용하여 모델 유효성 검사를 지원합니다.

#### `WeatherForecast.cs`
```csharp
using System;
using System.ComponentModel.DataAnnotations;

namespace MyApi
{
    public class WeatherForecast
    {
        [Required]
        public DateTime Date { get; set; }

        [Range(-20, 55)]
        public int TemperatureC { get; set; }

        public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);

        [Required]
        [StringLength(100)]
        public string Summary { get; set; }
    }
}
```

### 3.7 미들웨어
ASP

.NET Core는 요청 파이프라인에서 요청과 응답을 처리하는 미들웨어를 지원합니다.

#### `Startup.cs`
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseHttpsRedirection();

    app.UseRouting();

    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}
```

### 3.8 인증 및 권한 부여
ASP.NET Core는 다양한 인증 및 권한 부여 메커니즘을 지원합니다.

#### `Startup.cs`
```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddJwtBearer(options =>
        {
            options.TokenValidationParameters = new TokenValidationParameters
            {
                ValidateIssuer = true,
                ValidateAudience = true,
                ValidateLifetime = true,
                ValidateIssuerSigningKey = true,
                ValidIssuer = Configuration["Jwt:Issuer"],
                ValidAudience = Configuration["Jwt:Issuer"],
                IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Configuration["Jwt:Key"]))
            };
        });

    services.AddControllers();
}
```

### 3.9 로깅
ASP.NET Core는 다양한 로깅 메커니즘을 제공합니다.

#### `WeatherForecastController.cs`
```csharp
using Microsoft.Extensions.Logging;

namespace MyApi.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        private readonly ILogger<WeatherForecastController> _logger;

        public WeatherForecastController(ILogger<WeatherForecastController> logger)
        {
            _logger = logger;
        }

        [HttpGet]
        public IEnumerable<WeatherForecast> Get()
        {
            _logger.LogInformation("Fetching weather forecasts.");
            // Other code...
        }
    }
}
```

## 결론
백엔드 프레임워크는 웹 애플리케이션의 서버 측 로직을 구현하는 데 필요한 다양한 기능을 제공합니다. ASP.NET Core는 강력한 기능을 갖춘 백엔드 프레임워크로, 라우팅, 컨트롤러, 데이터베이스 연동, 유효성 검사, 의존성 주입, 미들웨어, 인증 및 권한 부여, 로깅 등을 지원합니다. 이 문서를 통해 백엔드 프레임워크의 주요 기능과 ASP.NET Core를 사용한 웹 애플리케이션 개발의 기초를 이해할 수 있습니다.

## 출처
- [ASP.NET Core 공식 문서](https://docs.microsoft.com/en-us/aspnet/core/)
- [Entity Framework Core 공식 문서](https://docs.microsoft.com/en-us/ef/core/)

---
## [다음](./02_02_database.md)



