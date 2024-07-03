# ASP.NET Core MVC 개요

## 목차
- [ASP.NET Core MVC 개요](#aspnet-core-mvc-개요)
  - [목차](#목차)
  - [MVC 패턴](#mvc-패턴)
    - [모델 책임](#모델-책임)
    - [뷰 책임](#뷰-책임)
    - [컨트롤러 책임](#컨트롤러-책임)
  - [ASP.NET Core MVC](#aspnet-core-mvc)
  - [라우팅](#라우팅)
  - [모델 바인딩](#모델-바인딩)
  - [모델 유효성 검사](#모델-유효성-검사)
  - [의존성 주입](#의존성-주입)
  - [필터](#필터)
  - [영역](#영역)
  - [웹 API](#웹-api)
  - [테스트 가능성](#테스트-가능성)
  - [Razor 뷰 엔진](#razor-뷰-엔진)
  - [강력한 형식의 뷰](#강력한-형식의-뷰)
  - [태그 헬퍼](#태그-헬퍼)
  - [뷰 컴포넌트](#뷰-컴포넌트)
  - [호환성 버전](#호환성-버전)
  - [추가 자료](#추가-자료)
  - [출처](#출처)
  - [다음](#다음)

---
ASP.NET Core MVC는 모델-뷰-컨트롤러 디자인 패턴을 사용하여 웹 앱과 API를 구축하는 데 사용되는 풍부한 프레임워크입니다.

---
## MVC 패턴

모델-뷰-컨트롤러(MVC) 아키텍처 패턴은 애플리케이션을 모델, 뷰 및 컨트롤러의 세 가지 주요 구성 요소 그룹으로 분리합니다. 이 패턴은 관심사의 분리를 달성하는 데 도움이 됩니다. 이 패턴을 사용하면 사용자 요청이 컨트롤러로 라우팅되며, 컨트롤러는 모델과 협력하여 사용자 작업을 수행하거나 쿼리 결과를 검색합니다. 컨트롤러는 사용자에게 표시할 뷰를 선택하고 필요한 모델 데이터를 제공합니다.

다음 다이어그램은 세 가지 주요 구성 요소와 이들 간의 참조 관계를 보여줍니다:

![MVC 패턴](../img/01_MVC_Overview/mvc.png)

이러한 책임의 구분은 애플리케이션의 복잡성을 확장하는 데 도움이 됩니다. 단일 작업을 수행하는 모델, 뷰 또는 컨트롤러를 코딩, 디버깅 및 테스트하는 것이 더 쉽기 때문입니다. 예를 들어, 사용자 인터페이스 로직은 비즈니스 로직보다 더 자주 변경되는 경향이 있습니다. 프레젠테이션 코드와 비즈니스 로직이 단일 객체에 결합되어 있는 경우, 사용자 인터페이스가 변경될 때마다 비즈니스 로직을 포함하는 객체를 수정해야 합니다. 이는 종종 오류를 유발하고 최소한의 사용자 인터페이스 변경 후에도 비즈니스 로직을 다시 테스트해야 합니다.

> [!NOTE]
> 뷰와 컨트롤러는 모델에 의존하지만, 모델은 뷰나 컨트롤러에 의존하지 않습니다. 이것이 분리의 주요 이점 중 하나입니다. 이 분리는 모델이 시각적 표현과 독립적으로 구축되고 테스트될 수 있도록 합니다.

### 모델 책임

MVC 애플리케이션에서 모델은 애플리케이션의 상태와 비즈니스 로직 또는 수행할 작업을 나타냅니다. 비즈니스 로직은 모델에 캡슐화되어야 하며, 애플리케이션의 상태를 지속시키기 위한 구현 로직도 포함되어야 합니다. 강력한 형식의 뷰는 일반적으로 해당 뷰에 표시할 데이터를 포함하도록 설계된 ViewModel 유형을 사용합니다. 컨트롤러는 모델에서 이러한 ViewModel 인스턴스를 생성하고 채웁니다.

### 뷰 책임

뷰는 사용자 인터페이스를 통해 콘텐츠를 표시하는 역할을 합니다. [Razor 뷰 엔진](#razor-뷰-엔진)을 사용하여 HTML 마크업에 .NET 코드를 삽입합니다. 뷰 내에는 최소한의 로직이 있어야 하며, 모든 로직은 콘텐츠를 표시하는 것과 관련이 있어야 합니다. 복잡한 모델의 데이터를 표시하기 위해 뷰 파일에서 많은 로직을 수행해야 하는 경우, 뷰 컴포넌트, ViewModel 또는 뷰 템플릿을 사용하여 뷰를 단순화하는 것을 고려하십시오.

### 컨트롤러 책임

컨트롤러는 사용자 상호 작용을 처리하고, 모델과 협력하며, 최종적으로 렌더링할 뷰를 선택하는 구성 요소입니다. MVC 애플리케이션에서 뷰는 정보만 표시하며, 컨트롤러는 사용자 입력 및 상호 작용을 처리하고 응답합니다. MVC 패턴에서 컨트롤러는 초기 진입 지점이며, 작업할 모델 유형과 렌더링할 뷰를 선택하는 책임이 있습니다(따라서 이름이 컨트롤러입니다 - 요청에 따라 앱이 어떻게 응답하는지 제어합니다).

> [!NOTE]
> 컨트롤러는 너무 많은 책임으로 인해 복잡해지지 않아야 합니다. 비즈니스 로직을 컨트롤러에서 도메인 모델로 이동시켜 컨트롤러 로직이 지나치게 복잡해지는 것을 방지하십시오.

> [!TIP]
> 컨트롤러 작업이 자주 동일한 종류의 작업을 수행하는 경우, 이러한 공통 작업을 [필터](#필터)로 이동하십시오.

## ASP.NET Core MVC

ASP.NET Core MVC 프레임워크는 ASP.NET Core와 함께 사용하기에 최적화된 경량의 오픈 소스, 높은 테스트 가능성을 가진 프레젠테이션 프레임워크입니다.

ASP.NET Core MVC는 동적 웹사이트를 구축할 수 있는 패턴 기반의 방법을 제공하여 관심사의 명확한 분리를 가능하게 합니다. 마크업에 대한 완전한 제어를 제공하며, 테스트 주도 개발(TDD) 친화적이고 최신 웹 표준을 사용합니다.

## 라우팅

ASP.NET Core MVC는 ASP.NET Core의 라우팅을 기반으로 구축된 강력한 URL 매핑 구성 요소로, 이해 가능하고 검색 가능한 URL을 갖춘 애플리케이션을 구축할 수 있습니다. 이를 통해 웹 서버의 파일 구성 방식과는 상관없이 검색 엔진 최적화(SEO) 및 링크 생성을 위해 애플리케이션의 URL 명명 패턴을 정의할 수 있습니다. 라우트 값 제약 조건, 기본값 및 선택적 값을 지원하는 편리한 라우트 템플릿 구문을 사용하여 라우트를 정의할 수 있습니다.

*규칙 기반 라우팅*은 애플리케이션이 수락하는 URL 형식을 전역적으로 정의하고 각 형식이 주어진 컨트롤러의 특정 작업 메서드에 어떻게 매핑되는지를 정의할 수 있습니다. 들어오는 요청이 수신되면 라우팅 엔진이 URL을 구문 분석하고 정의된 URL 형식 중 하나와 일치시킨 다음 관련 컨트롤러의 작업 메서드를 호출합니다.

```csharp
routes.MapRoute(name: "Default", template: "{controller=Home}/{action=Index}/{id?}");
```

*속성 라우팅*은 애플리케이션의 경로를 정의하는 속성을 사용하여 컨트롤러 및 작업에 라우팅 정보를 지정할 수 있게 합니다. 즉, 경로 정의가 관련된 컨트롤러 및 작업 옆에 배치됩니다.

```csharp
[Route("api/[controller]")]
public class ProductsController : Controller
{
    [HttpGet("{id}")]
    public IActionResult GetProduct(int id)
    {
      ...
    }
}
```

## 모델 바인딩

ASP.NET Core MVC 모델 바인딩은 클라이언트 요청 데이터(폼 값, 라우트 데이터, 쿼리 문자열 매개변수, HTTP 헤더)를 컨트롤러가 처리할 수 있는 객체로 변환합니다. 결과적으로 컨트롤러 로직은 들어오는 요청 데이터를 처리하는 작업을 할 필요가 없으며, 단순히 데이터가 작업 메서드의 매개변수로 제공됩니다.

```csharp
public async Task<IActionResult> Login(LoginViewModel model, string returnUrl = null) { ... }
```

## 모델 유효성 검사

ASP.NET Core MVC는 모델 객체를 데이터 주석 유효성 검사 속성으로 장식하여 유효성 검사를 지원합니다. 유효성 검사 속성은 값이 서버에 게시되기 전에 클라이언트 측에서, 그리고 컨트롤러 작업이 호출되기 전에 서버 측에서 확인됩니다.

```csharp
using System.ComponentModel.DataAnnotations;
public class LoginViewModel
{
    [Required]
    [EmailAddress]
    public string Email { get; set; }

    [Required]
    [DataType(DataType.Password)]
    public string Password { get; set; }

    [Display(Name = "Remember me?")]
    public bool RememberMe { get; set; }
}
```

컨트롤러 작업:

```csharp
public async Task<IActionResult> Login(LoginViewModel model, string returnUrl = null)
{
    if (ModelState.IsValid)
    {
      // 모델 작업
    }
    // 이 시점에서 무언가 실패하면 폼을 다시 표시합니다.
    return View(model);
}
```

프레임워크는 클라이언트와 서버 모두에서 요청 데이터를 유효성 검사합니다. 모델 유형에 지정된 유효성 검사 로직은 렌더링된 뷰에 비간섭적 주석으로 추가되며, jQuery 유효성 검사로 브라우저에서 강제됩니다.

## 의존성 주입

ASP.NET Core는 의존성 주입(DI)에 대한 기본 지원을 제공합니다. ASP.NET Core MVC에서 컨트롤러는 생성자를 통해 필요한 서비스를 요청할 수 있으며, 이를 통해 명시적 의존성 원칙을 따를 수 있습니다.

앱은 또한 `@inject` 지시문을 사용하여 뷰 파일에서 의존성 주입을 사용할 수 있습니다:

```cshtml
@inject SomeService ServiceName

<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ServiceName.GetTitle</title>
</head>
<body>
    <h1>@ServiceName.GetTitle</h1>
</body>
</html>
```

## 필터

필터는 예외 처리나 인증과 같은 횡단 관심사를 캡슐화하는 데 도움이 됩니다. 필터는 작업 메서드에 대한 사용자 지정 전처리 및 후처리 로직을 실행할 수 있으며, 주어진 요청에 대한 실행 파이프라인의 특정 지점에서 실행되도록 구성할 수 있습니다. 필터는 컨트롤러나 작업에 속성으로 적용될 수 있으며(또는 전역적으로 실행될 수 있음), 프레임워크에 여러 필터(예: `Authorize`)가 포함되어 있습니다. `[Authorize]`는 MVC 인증 필터를 생성하는 데 사용되는 속성입니다.

```csharp
[Authorize]
public class AccountController : Controller
```

## 영역

영역은 대규모 ASP.NET Core MVC 웹 애플리케이션을 더 작은 기능 그룹으로 분할하는 방법을 제공합니다. 영역은 애플리케이션 내에서 MVC 구조입니다. MVC 프로젝트에서는 모델, 컨트롤러 및 뷰와 같은 논리적 구성 요소가 다른 폴더에 저장되며, MVC는 이러한 구성 요소 간의 관계를 생성하기 위해 명명 규칙을 사용합니다. 대규모 애플리케이션의 경우, 애플리케이션을 별도의 상위 기능 영역으로 분할하는 것이 유리할 수 있습니다. 예를 들어, 여러 비즈니스 단위(예: 체크아웃, 청구, 검색 등)를 가진 전자 상거래 앱이 있을 수 있습니다. 이러한 각 단위는 자체 논리적 구성 요소 뷰, 컨트롤러 및 모델을 가집니다.

## 웹 API

ASP.NET Core MVC는 웹 사이트를 구축하는 데 훌륭한 플랫폼일 뿐만 아니라 웹 API를 구축하는 데에도 뛰어난 지원을 제공합니다. 브라우저 및 모바일 장치를 포함한 다양한 클라이언트에 도달할 수 있는 서비스를 구축할 수 있습니다.

프레임워크는 JSON 또는 XML로 데이터 포맷을 지원하는 HTTP 콘텐츠 협상을 지원합니다. 사용자 지정 포맷터를 작성하여 사용자 고유의 형식을 추가로 지원할 수 있습니다.

링크 생성을 사용하여 하이퍼미디어에 대한 지원을 활성화하십시오. 교차 출처 리소스 공유(CORS)를 쉽게 활성화하여 여러 웹 애플리케이션에서 웹 API를 공유할 수 있습니다.

## 테스트 가능성

프레임워크의 인터페이스 및 의존성 주입 사용은 단위 테스트에 적합하며, 프레임워크에는 통합 테스트를 빠르고 쉽게 수행할 수 있는 기능(예: TestHost 및 Entity Framework용 InMemory 제공자)이 포함되어 있습니다. 컨트롤러 로직 테스트 방법에 대해 자세히 알아보십시오.

## Razor 뷰 엔진

ASP.NET Core MVC 뷰는 Razor 뷰 엔진을 사용하여 뷰를 렌더링합니다. Razor는 임베디드 C# 코드를 사용하여 뷰를 정의하는 간결하고 표현력 있는 템플릿 마크업 언어입니다. Razor는 서버에서 웹 콘텐츠를 동적으로 생성하는 데 사용됩니다. 서버 코드와 클라이언트 측 콘텐츠 및 코드를 깔끔하게 혼합할 수 있습니다.

```cshtml
<ul>
    @for (int i = 0; i < 5; i++) {
        <li>List item @i</li>
    }
</ul>
```

Razor 뷰 엔진을 사용하여 레이아웃, 부분 뷰 및 교체 가능한 섹션을 정의할 수 있습니다.

## 강력한 형식의 뷰

MVC의 Razor 뷰는 모델을 기반으로 강력한 형식을 가질 수 있습니다. 컨트롤러는 뷰에 강력한 형식의 모델을 전달하여 뷰에 타입 검사 및 IntelliSense 지원을 가능하게 합니다.

예를 들어, 다음 뷰는 `IEnumerable<Product>` 유형의 모델을 렌더링합니다:

```cshtml
@model IEnumerable<Product>
<ul>
    @foreach (Product p in Model)
    {
        <li>@p.Name</li>
    }
</ul>
```

## 태그 헬퍼

태그 헬퍼는 서버 측 코드를 Razor 파일에서 HTML 요소를 생성하고 렌더링하는 데 참여하게 합니다. 태그 헬퍼를 사용하여 사용자 지정 태그(예: `<environment>`)를 정의하거나 기존 태그(예: `<label>`)의 동작을 수정할 수 있습니다. 태그 헬퍼는 요소 이름 및 속성을 기준으로 특정 요소에 바인딩됩니다. 서버 측 렌더링의 이점을 제공하면서도 HTML 편집 경험을 보존합니다.

일반적인 작업을 위한 많은 내장 태그 헬퍼가 있으며(예: 폼 생성, 링크, 자산 로딩 등), GitHub 리포지토리 및 NuGet 패키지에서 더 많은 태그 헬퍼를 사용할 수 있습니다. 태그 헬퍼는 C#으로 작성되며, 요소 이름, 속성 이름 또는 상위 태그를 기준으로 HTML 요소를 대상으로 합니다. 예를 들어, 내장된 LinkTagHelper는 `AccountsController`의 `Login` 작업으로의 링크를 생성하는 데 사용할 수 있습니다:

```cshtml
<p>
    이메일 확인해 주셔서 감사합니다.
    <a asp-controller="Account" asp-action="Login">여기를 클릭하여 로그인하십시오</a>.
</p>
```

`EnvironmentTagHelper`는 실행 환경(예: 개발, 스테이징 또는 프로덕션)에 따라 뷰에서 다른 스크립트를 포함하는 데 사용할 수 있습니다:

```cshtml
<environment names="Development">
    <script src="~/lib/jquery/dist/jquery.js"></script>
</environment>
<environment names="Staging,Production">
    <script src="https://ajax.aspnetcdn.com/ajax/jquery/jquery-2.1.4.js"
            asp-fallback-src="~/lib/jquery/dist/jquery.js"
            asp-fallback-test="window.jQuery">
    </script>
</environment>
```

태그 헬퍼는 HTML 및 Razor 마크업을 작성할 때 HTML 친화적인 개발 경험과 풍부한 IntelliSense 환경을 제공합니다. 대부분의 내장 태그 헬퍼는 기존 HTML 요소를 대상으로 하며, 요소에 서버 측 속성을 제공합니다.

## 뷰 컴포넌트

뷰 컴포넌트는 렌더링 로직을 패키징하여 애플리케이션 전체에서 재사용할 수 있게 합니다. 이는 부분 뷰와 유사하지만 관련된 로직이 포함되어 있습니다.

## 호환성 버전

`SetCompatibilityVersion` 메서드를 사용하여 애플리케이션이 ASP.NET Core MVC 2.1 이상에서 도입된 잠재적으로 호환성을 깨는 동작 변경 사항을 선택적으로 사용할 수 있습니다.

자세한 내용은 [Compatibility version for ASP.NET Core MVC](https://learn.microsoft.com/en-us/aspnet/core/mvc/compatibility-version?view=aspnetcore-8.0)을 참조하십시오.

## 추가 자료

* [MyTested.AspNetCore.Mvc - ASP.NET Core MVC용 Fluent Testing Library](https://github.com/ivaylokenov/MyTested.AspNetCore.Mvc): MVC 및 웹 API 애플리케이션을 테스트하기 위한 강력한 형식의 단위 테스트 라이브러리로, 유창한 인터페이스를 제공합니다. (*Microsoft에서 유지 관리하거나 지원하지 않음.*)
* [Dependency injection in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)

---
## 출처
[MVC Overview](https://learn.microsoft.com/en-us/aspnet/core/mvc/overview?view=aspnetcore-8.0)

---
## [다음](./02_View.md)
