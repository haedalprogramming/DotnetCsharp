# Routing to controller actions in ASP.NET Core

## 목차
- [Routing to controller actions in ASP.NET Core](#routing-to-controller-actions-in-aspnet-core)
  - [목차](#목차)
  - [전통적인 라우트 설정](#전통적인-라우트-설정)
  - [전통적인 라우팅](#전통적인-라우팅)
    - [다중 전통적인 라우트](#다중-전통적인-라우트)
    - [전통적인 라우팅 순서](#전통적인-라우팅-순서)
    - [모호한 액션 해결](#모호한-액션-해결)
    - [전통적인 라우트 이름](#전통적인-라우트-이름)
  - [REST API를 위한 속성 라우팅](#rest-api를-위한-속성-라우팅)
  - [예약된 라우팅 이름](#예약된-라우팅-이름)
  - [HTTP 메서드 템플릿](#http-메서드-템플릿)
    - [라우트 템플릿](#라우트-템플릿)
    - [HTTP 메서드 속성을 사용한 속성 라우팅](#http-메서드-속성을-사용한-속성-라우팅)
  - [라우트 이름](#라우트-이름)
  - [속성 라우트 결합](#속성-라우트-결합)
    - [속성 라우트 순서](#속성-라우트-순서)
  - [라우트 템플릿에서의 토큰 대체 \[controller\], \[action\], \[area\]](#라우트-템플릿에서의-토큰-대체-controller-action-area)
    - [매개변수 변환기를 사용하여 토큰 대체 사용자 지정](#매개변수-변환기를-사용하여-토큰-대체-사용자-지정)
    - [다중 속성 라우트](#다중-속성-라우트)
    - [속성 라우트 선택적 매개변수, 기본값 및 제약 조건 지정](#속성-라우트-선택적-매개변수-기본값-및-제약-조건-지정)
    - [IRouteTemplateProvider를 사용하여 사용자 지정 라우트 속성](#iroutetemplateprovider를-사용하여-사용자-지정-라우트-속성)
    - [애플리케이션 모델을 사용하여 속성 라우트 사용자 지정](#애플리케이션-모델을-사용하여-속성-라우트-사용자-지정)
  - [혼합 라우팅: 속성 라우팅 대 전통적인 라우팅](#혼합-라우팅-속성-라우팅-대-전통적인-라우팅)
  - [특수 문자와 라우팅](#특수-문자와-라우팅)
  - [URL 생성 및 상위 값](#url-생성-및-상위-값)
    - [액션 이름으로 URL 생성](#액션-이름으로-url-생성)
    - [라우트로 URL 생성](#라우트로-url-생성)
    - [HTML 및 Razor에서 URL 생성](#html-및-razor에서-url-생성)
    - [액션 결과에서 URL 생성](#액션-결과에서-url-생성)
    - [전용 전통적인 라우트의 특별 사례](#전용-전통적인-라우트의-특별-사례)
  - [영역](#영역)
  - [액션 정의](#액션-정의)
  - [샘플 코드](#샘플-코드)
  - [디버그 진단](#디버그-진단)
  - [출처](#출처)
  - [다음](#다음)

---
ASP.NET Core 컨트롤러는 라우팅 [미들웨어](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0)를 사용하여 들어오는 요청의 URL을 매칭하고 이를 [액션](#액션-정의)에 매핑합니다. 라우트 템플릿:

* `Program.cs` 또는 속성에서 시작 시 정의됩니다.
* URL 경로가 [액션](#액션-정의)에 매핑되는 방법을 설명합니다.
* 링크의 URL을 생성하는 데 사용됩니다. 생성된 링크는 일반적으로 응답에 반환됩니다.

액션은 [전통적인 라우팅](#전통적인-라우트-설정) 또는 [속성 라우팅](#rest-api를-위한-속성-라우팅)을 통해 이루어집니다. 컨트롤러나 [액션](#액션-정의)에 라우트를 배치하면 속성 라우팅이 됩니다. 자세한 내용은 [혼합 라우팅](#혼합-라우팅-속성-라우팅-대-전통적인-라우팅)을 참조하십시오.

이 문서에서는:

* MVC와 라우팅 간의 상호 작용을 설명합니다:
  * 일반적인 MVC 앱이 라우팅 기능을 사용하는 방법.
  * [컨벤션 라우팅](#전통적인-라우트-설정)과 REST API에 사용되는 *속성 라우팅*을 모두 다룹니다. REST API의 라우팅에 주로 관심이 있다면 [REST API를 위한 속성 라우팅](#rest-api를-위한-속성-라우팅) 섹션으로 이동하십시오.
  * 고급 라우팅 세부 사항은 [라우팅](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0)을 참조하십시오.
* 기본 라우팅 시스템인 엔드포인트 라우팅에 대해 설명합니다. 이전 버전의 라우팅을 호환성 목적으로 사용하여 컨트롤러를 사용할 수 있습니다. 지침은 [2.2-3.0 마이그레이션 가이드](https://learn.microsoft.com/en-us/aspnet/core/migration/22-to-30?view=aspnetcore-8.0)를 참조하십시오.

<a name="cr6"></a>

## 전통적인 라우트 설정

ASP.NET Core MVC 템플릿은 다음과 유사한 [전통적인 라우팅](#전통적인-라우팅) 코드를 생성합니다:

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllersWithViews();

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
```

`MapControllerRoute`는 단일 라우트를 생성하는 데 사용됩니다. 이 단일 라우트는 `default` 라우트로 명명됩니다. 컨트롤러와 뷰를 사용하는 대부분의 앱은 `default` 라우트와 유사한 라우트 템플릿을 사용합니다. REST API는 [속성 라우팅](#rest-api를-위한-속성-라우팅)을 사용해야 합니다.

```C#
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

라우트 템플릿 `"{controller=Home}/{action=Index}/{id?}"`:

* `/Products/Details/5`와 같은 URL 경로에 매핑됩니다.
* 경로를 토큰화하여 `{ controller = Products, action = Details, id = 5 }`와 같은 경로 값을 추출합니다. 경로 값의 추출은 앱에 `ProductsController`라는 컨트롤러와 `Details` 액션이 있는 경우 매칭됩니다:
    ```C#
    public class ProductsController : Controller
    {
        public IActionResult Details(int id)
        {
            return ControllerContext.MyDisplayRouteInfo(id);
        }
    }
    ```
    [MyDisplayRouteInfo](https://github.com/Rick-Anderson/RouteInfo/blob/master/Microsoft.Docs.Samples.RouteInfo/ControllerContextExtensions.cs)는 [Rick.Docs.Samples.RouteInfo](https://www.nuget.org/packages/Rick.Docs.Samples.RouteInfo) NuGet 패키지에 의해 제공되며 라우트 정보를 표시합니다.

* `/Products/Details/5`는 `id` 값을 모델 바인딩하여 `id` 매개변수를 `5`로 설정합니다. 자세한 내용은 [모델 바인딩](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-8.0)을 참조하십시오.
* `{controller=Home}`는 `Home`을 기본 `controller`로 정의합니다.
* `{action=Index}`는 `Index`를 기본 `action`으로 정의합니다.
* `{id?}`의 `?` 문자는 `id`를 선택 사항으로 정의합니다.
  * 기본 및 선택적 라우트 매개변수는 매칭을 위해 URL 경로에 존재할 필요가 없습니다. 라우트 템플릿 구문에 대한 자세한 설명은 [라우트 템플릿 참조](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#route-template-reference)를 참조하십시오.
* URL 경로 `/`와 매칭됩니다.
* `{ controller = Home, action = Index }`라는 라우트 값을 생성합니다.

`controller`와 `action`의 값은 기본값을 사용합니다. `id`는 URL 경로에 해당 세그먼트가 없으므로 값을 생성하지 않습니다. `/`는 `HomeController`와 `Index` 액션이 있는 경우에만 매칭됩니다:

```csharp
public class HomeController : Controller
{
    public IActionResult Index() { ... }
}
```

위의 컨트롤러 정의와 라우트 템플릿을 사용하면, `HomeController.Index` 액션은 다음 URL 경로에 대해 실행됩니다:

* `/Home/Index/17`
* `/Home/Index`
* `/Home`
* `/`

URL 경로 `/`는 기본 `Home` 컨트롤러와 `Index` 액션을 사용합니다. URL 경로 `/Home`은 기본 `Index` 액션을 사용합니다.

편의 메서드 `MapDefaultControllerRoute`는:
```C#
app.MapDefaultControllerRoute();
```
다음을 대체합니다:
```C#
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

> [!IMPORTANT]
> 라우팅은 `UseRouting` 및 `UseEndpoints` 미들웨어를 사용하여 구성됩니다. 컨트롤러를 사용하려면:
>
> * [속성 라우팅된](#rest-api를-위한-속성-라우팅) 컨트롤러를 매핑하려면 `MapControllers`를 호출하십시오.
> * [전통적인 라우팅된](#전통적인-라우트-설정) 컨트롤러와 [속성 라우팅된](#rest-api를-위한-속성-라우팅) 컨트롤러를 모두 매핑하려면 `MapControllerRoute` 또는 `MapAreaControllerRoute`를 호출하십시오.
>
> 앱은 일반적으로 `UseRouting` 또는 `UseEndpoints`를 호출할 필요가 없습니다. `WebApplicationBuilder`는 `Program.cs`에서 추가된 미들웨어를 `UseRouting` 및 `UseEndpoints`로 래핑하는 미들웨어 파이프라인을 구성합니다. 자세한 내용은 [Routing in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0)을 참조하십시오.

## 전통적인 라우팅

전통적인 라우팅은 컨트롤러와 뷰와 함께 사용됩니다. `default` 라우트:

```C#
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

위의 예는 *전통적인 라우트*의 예입니다. 이를 *전통적인 라우팅*이라고 하는 이유는 URL 경로에 대한 *컨벤션*을 설정하기 때문입니다:

* 첫 번째 경로 세그먼트 `{controller=Home}`는 컨트롤러 이름에 매핑됩니다.
* 두 번째 세그먼트 `{action=Index}`는 [액션](#액션-정의) 이름에 매핑됩니다.
* 세 번째 세그먼트 `{id?}`는 선택적 `id`에 사용됩니다. `{id?}`의 `?`는 선택 사항을 나타냅니다. `id`는 모델 엔티티에 매핑하는 데 사용됩니다.

이 `default` 라우트를 사용하면 URL 경로:

* `/Products/List`는 `ProductsController.List` 액션에 매핑됩니다.
* `/Blog/Article/17`는 `BlogController.Article`에 매핑되며 일반적으로 `id` 매개변수를 17로 모델 바인딩합니다.

이 매핑은:

* 컨트롤러와 [액션](#액션-정의) 이름 **만**을 기반으로 합니다.
* 네임스페이스, 소스 파일 위치 또는 메서드 매개변수를 기반으로 하지 않습니다.

기본 라우트를 사용하여 전통적인 라우팅을 사용하면 각 액션에 대해 새로운 URL 패턴을 만들어야 하는 부담 없이 앱을 만들 수 있습니다. [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 스타일 액션이 있는 앱에서는 컨트롤러 전반에 걸쳐 URL의 일관성을 유지하는 것이:

* 코드를 단순화하는 데 도움이 됩니다.
* UI를 더 예측 가능하게 만듭니다.

> [!WARNING]


> 위의 코드에서 `id`는 라우트 템플릿에 의해 선택적으로 정의됩니다. 액션은 URL에서 선택적 ID가 제공되지 않은 경우에도 실행될 수 있습니다. 일반적으로 URL에서 `id`가 생략되면:
>
> * 모델 바인딩에 의해 `id`가 `0`으로 설정됩니다.
> * 데이터베이스에서 `id == 0`과 일치하는 엔티티가 없습니다.
>
> [속성 라우팅](#rest-api를-위한-속성-라우팅)은 ID를 특정 액션에 대해 필수로 만들고 다른 액션에는 선택적으로 만드는 세밀한 제어를 제공합니다. 문서에서는 `id`가 올바르게 사용될 가능성이 높은 경우 선택적 매개변수를 포함합니다.

대부분의 앱은 URL이 읽기 쉽고 의미가 있도록 기본적이고 설명적인 라우팅 방식을 선택해야 합니다. 기본 전통적인 라우트 `{controller=Home}/{action=Index}/{id?}`:

* 기본적이고 설명적인 라우팅 방식을 지원합니다.
* UI 기반 앱의 유용한 출발점입니다.
* 많은 웹 UI 앱에 필요한 유일한 라우트 템플릿입니다. 더 큰 웹 UI 앱의 경우, [영역](#영역)을 사용하는 또 다른 라우트가 자주 필요한 모든 것입니다.

`MapControllerRoute` 및 `MapAreaRoute` :

* 자동으로 호출 순서에 따라 엔드포인트에 **순서** 값을 할당합니다.

ASP.NET Core의 엔드포인트 라우팅:

* 라우트 개념을 가지고 있지 않습니다.
* 모든 엔드포인트가 한 번에 처리되므로 확장성 실행 순서에 대한 보장을 제공하지 않습니다.

내장된 라우팅 구현(예: `Route`)이 요청과 일치하는 방법을 보려면 [로그](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-8.0)를 활성화하십시오.

[속성 라우팅](#rest-api를-위한-속성-라우팅)은 이 문서 후반부에서 설명합니다.

<a name="mr6"></a>

### 다중 전통적인 라우트

여러 [전통적인 라우트](#전통적인-라우트-설정)를 <xref:Microsoft.AspNetCore.Builder.ControllerEndpointRouteBuilderExtensions.MapControllerRoute%2A> 및 <xref:Microsoft.AspNetCore.Builder.ControllerEndpointRouteBuilderExtensions.MapAreaControllerRoute%2A>를 추가하여 구성할 수 있습니다. 이를 통해 여러 규칙을 정의하거나 특정 [액션](#액션-정의)에 전용 전통적인 라우트를 추가할 수 있습니다:

[!code-csharp[](routing/samples/6.x/main/Program.cs?name=snippet_mcr)]

<a name="dcr"></a>

위의 코드에서 `blog` 라우트는 **전용 전통적인 라우트**입니다. 이를 전용 전통적인 라우트라고 하는 이유는:

* [전통적인 라우팅](#전통적인-라우트-설정)을 사용합니다.
* 특정 [액션](#액션-정의)에 전용입니다.

`controller`와 `action`이 경로 템플릿 `"blog/{*article}"`에 매개변수로 나타나지 않으므로:

* 기본값 `{ controller = "Blog", action = "Article" }`만 가질 수 있습니다.
* 이 라우트는 항상 `BlogController.Article` 액션에 매핑됩니다.

`/Blog`, `/Blog/Article` 및 `/Blog/{any-string}`은 blog 라우트와 일치하는 유일한 URL 경로입니다.

위의 예:

* `blog` 라우트는 먼저 추가되었기 때문에 `default` 라우트보다 매칭 우선 순위가 높습니다.
* URL에 기사 이름을 포함하는 것이 일반적인 [슬러그](https://developer.mozilla.org/docs/Glossary/Slug) 스타일 라우팅의 예입니다.

> [!WARNING]
> ASP.NET Core에서 라우팅은 다음을 정의하지 않습니다:
> * *라우트*라는 개념. `UseRouting`은 미들웨어 파이프라인에 라우트 매칭을 추가합니다. `UseRouting` 미들웨어는 앱에 정의된 엔드포인트 집합을 보고 요청에 따라 가장 적합한 엔드포인트 매칭을 선택합니다.
> * `IRouteConstraint` 또는 `IActionConstraint`와 같은 확장성의 실행 순서에 대한 보장을 제공하지 않습니다.
>
> 라우팅에 대한 참고 자료는 [라우팅](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0)을 참조하십시오.

<a name="cro6"></a>

### 전통적인 라우팅 순서

전통적인 라우팅은 앱에서 정의된 액션과 컨트롤러의 조합만 매칭합니다. 이는 전통적인 라우트가 겹치는 경우를 단순화하기 위해 설계되었습니다.
`MapControllerRoute`, `MapDefaultControllerRoute` 및 `MapAreaControllerRoute`를 사용하여 라우트를 추가하면 호출 순서에 따라 엔드포인트에 자동으로 순서 값이 할당됩니다. 앞서 나타나는 라우트의 매칭 우선 순위가 높습니다. 전통적인 라우팅은 순서에 의존합니다. 일반적으로 영역이 있는 라우트는 영역이 없는 라우트보다 더 구체적이므로 더 일찍 배치해야 합니다. `{*article}`와 같은 캐치올 라우트 매개변수가 있는 [전용 전통적인 라우트](#다중-전통적인-라우트)는 너무 [탐욕적](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#greedy)일 수 있으며, 다른 라우트와 매칭되는 URL을 매칭합니다. 탐욕적인 매칭을 방지하기 위해 탐욕적인 라우트를 라우트 테이블의 나중에 배치하십시오.

<a name="best"></a>

### 모호한 액션 해결

두 개의 엔드포인트가 라우팅을 통해 매칭될 때, 라우팅은 다음 중 하나를 수행해야 합니다:

* 가장 적합한 후보를 선택합니다.
* 예외를 던집니다.

예를 들어:

```C#
public class Products33Controller : Controller
{
    public IActionResult Edit(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }

    [HttpPost]
    public IActionResult Edit(int id, Product product)
    {
        return ControllerContext.MyDisplayRouteInfo(id, product.name);
    }
}
```

위의 컨트롤러는 다음과 일치하는 두 개의 액션을 정의합니다:

* URL 경로 `/Products33/Edit/17`
* 라우트 데이터 `{ controller = Products33, action = Edit, id = 17 }`.

이것은 MVC 컨트롤러의 일반적인 패턴입니다:

* `Edit(int)`는 제품을 편집하는 양식을 표시합니다.
* `Edit(int, Product)`는 제출된 양식을 처리합니다.

올바른 라우트를 해결하려면:

* 요청이 HTTP `POST`일 때 `Edit(int, Product)`가 선택됩니다.
* [HTTP 메서드](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-8.0#verb)가 다른 경우 `Edit(int)`가 선택됩니다. `Edit(int)`는 일반적으로 `GET`을 통해 호출됩니다.

`HttpPostAttribute`인 `[HttpPost]`는 라우팅에 제공되어 요청의 HTTP 메서드를 기준으로 선택할 수 있습니다. `HttpPostAttribute`는 `Edit(int, Product)`를 `Edit(int)`보다 더 나은 매칭으로 만듭니다.

`HttpPostAttribute`와 같은 속성의 역할을 이해하는 것이 중요합니다. 다른 [HTTP 메서드](#verb)에 대해 유사한 속성이 정의되어 있습니다. [전통적인 라우팅](#전통적인-라우트-설정)에서는 액션이 양식 표시와 양식 제출 워크플로의 일부일 때 동일한 액션 이름을 사용하는 것이 일반적입니다. 예를 들어, [두 Edit 액션 메서드 검사](xref:tutorials/first-mvc-app/controller-methods-views#get-post)를 참조하십시오.

라우팅이 가장 적합한 후보를 선택할 수 없는 경우, 여러 매칭된 엔드포인트를 나열하는 `AmbiguousMatchException`이 발생합니다.

<a name="routing-route-name-ref-label"></a>

### 전통적인 라우트 이름

다음 예제에서 `"blog"`와 `"default"` 문자열은 전통적인 라우트 이름입니다:

```C#
app.MapControllerRoute(name: "blog",
                pattern: "blog/{*article}",
                defaults: new { controller = "Blog", action = "Article" });
app.MapControllerRoute(name: "default",
               pattern: "{controller=Home}/{action=Index}/{id?}");
```

라우트 이름은 라우트에 논리적 이름을 부여합니다. 명명된 라우트는 URL 생성을 위해 사용할 수 있습니다. 라우트의 순서가 URL 생성에 복잡한 영향을 미칠 수 있는 경우 명명된 라우트를 사용하면 URL 생성을 단순화할 수 있습니다. 라우트 이름은 앱 전역에서 고유해야 합니다.

라우트 이름:

* URL 매칭 또는 요청 처리에 영향을 미치지 않습니다.
* URL 생성에만 사용됩니다.

라우트 이름 개념은 [IEndpointNameMetadata](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.routing.iendpointnamemetadata)로 라우팅에서 표현됩니다. 

용어 **라우트 이름**과 **엔드포인트 이름**:

* 상호 교환 가능합니다.
* 설명 중인 API에 따라 문서와 코드에서 사용되는 용어가 다릅니다.

<a name="attribute-routing-ref-label"></a>
<a name="ar6"></a>

## REST API를 위한 속성 라우팅

REST API는 속성 라우팅을 사용하여 앱의 기능을 HTTP 메서드로 표현된 리소스 집합으로 모델링해야 합니다.

속성 라우팅은 속성 집합을 사용하여 액션을 직접 라우트 템플릿에 매핑합니다. 다음 코드는 REST API에 일반적으로 사용되며 다음 샘플에서 사용됩니다:

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

위의 코드에서는 `MapControllers`를 호출하여 속성 라우팅된 컨트롤러를 매핑합니다.

다음 예제에서:

* `HomeController`는 기본 전통적인 라우트 `{controller=Home}/{action=Index}/{id?}`와 유사한 URL 집합과 일치합니다.

```C#
public class HomeController : Controller
{
    [Route("")]
    [Route("Home")]
    [Route("Home/Index")]
    [Route("Home/Index/{id?}")]
    public IActionResult Index(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }

    [Route("Home/About")]
    [Route("Home/About/{id?}")]
    public IActionResult About(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

`HomeController.Index` 액션은 `/`, `/Home`, `/Home/Index` 또는 `/Home/Index/3`의 URL 경로에 대해 실행됩니다.

이 예제는 속성 라우팅과 [전통적인 라우팅](#전통적인-라우트-설정) 간의 주요 프로그래밍 차이를 강조합니다. 속성 라우팅은 라우트를 지정하기 위해 더 많은 입력을 필요로 합니다. 기본 전통적인 라우트는 라우트를 더 간결하게 처리합니다. 그러나 속성 라우팅은 각 [액션](#액션-정의)에 적용되는 라우트 템플릿을 정확하게 제어할 수 있습니다.

속성 라우팅에서는 컨트롤러와 액션 이름이 매칭되는 데 역할을 하지 않습니다(단, [토큰 대체](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-8.0#routing-token-replacement-templates-ref-label)를 사용하는 경우 제외). 다음 예제는 이전 예제와 동일한 URL을 매칭합니다:

```C#
public class MyDemoController : Controller
{
    [Route("")]
    [Route("Home")]
    [Route("Home/Index")]
    [Route("Home/Index/{id?}")]
    public IActionResult MyIndex(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }

    [Route("Home/About")]
    [Route("Home/About/{id?}")]
    public IActionResult MyAbout(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

다음 코드는 `action` 및 `controller`에 대한 토큰 대체를 사용합니다:

```C#
public class HomeController : Controller
{
    [Route("")]
    [Route("Home")]
    [Route("[controller]/[action]")]
    public IActionResult Index()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [Route("[controller]/[action]")]
    public IActionResult About()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

다음 코드는 컨트롤러에 `[Route("[controller]/[action]")]`를 적용합니다:

```C#
[Route("[controller]/[action]")]
public class HomeController : Controller
{
    [Route("~/")]
    [Route("/Home")]
    [Route("~/Home/Index")]
    public IActionResult Index()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    public IActionResult About()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

위의 코드에서, `Index` 메서드 템플릿은 라우트 템플릿에 `/` 또는 `~/`를 앞에 붙여야 합니다. 컨트롤러에 적용된 라우트 템플릿과 결합되지 않습니다.

라우트 템플릿 선택에 대한 자세한 내용은 [라우트 템플릿 우선순위](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#rtp)를 참조하십시오.

## 예약된 라우팅 이름

컨트롤러 또는 Razor Pages를 사용할 때 다음 키워드는 예약된 라우트 매개변수 이름입니다:

* `action`
* `area`
* `controller`
* `handler`
* `page`

속성 라우팅에서 `page`를 라우트 매개변수로 사용하는 것은 일반적인 오류입니다. 이렇게 하면 URL 생성 시 일관되지 않고 혼란스러운 동작이 발생합니다.

```C#
public class MyDemo2Controller : Controller
{
    [Route("/articles/{page}")]
    public IActionResult ListArticles(int page)
    {
        return ControllerContext.MyDisplayRouteInfo(page);
    }
}
```

특별 매개변수 이름은 URL 생성 시 Razor Page 또는 Controller를 참조하는지 여부를 결정하는 데 사용됩니다.

다음 키워드는 Razor 뷰 또는 Razor Page 컨텍스트에서 예약되었습니다:

* `page`
* `using`
* `namespace`
* `inject`
* `section`
* `inherits`
* `model`
* `addTagHelper`
* `removeTagHelper`

이러한 키워드는 링크 생성, 모델 바인딩된 매개변수 또는 최상위 속성에 사용하지 않아야 합니다.

<a name="verb6"></a>

## HTTP 메서드 템플릿

ASP.NET Core에는 다음과 같은 HTTP 메서드 템플릿이 있습니다:

* `[HttpGet]`
* `[HttpPost]`
* `[HttpPut]`
* `[HttpDelete]`
* `[HttpHead]`
* `[HttpPatch]`

<a name="rt6"></a>

### 라우트 템플릿

ASP.NET Core에는 다음과 같은 라우트 템플릿이 있습니다:

* 모든 [HTTP 메서드 템플릿](#http-메서드-템플릿)은 라우트 템플릿입니다.
* [[Route]](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.routeattribute)

<a name="arx"></a>

### HTTP 메서드 속성을 사용한 속성 라우팅

다음 컨트롤러를 고려하십시오:

```C#
[Route("api/[controller]")]
[ApiController]
public class Test2Controller : ControllerBase
{
    [HttpGet]   // GET /api/test2
    public IActionResult ListProducts()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [HttpGet("{id}")]   // GET /api/test2/xyz
    public IActionResult GetProduct(string id)
    {
       return ControllerContext.MyDisplayRouteInfo(id);
    }

    [HttpGet("int/{id:int}")] // GET /api/test2/int/3
    public IActionResult GetIntProduct(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }

    [HttpGet("int2/{id}")]  // GET /api/test2/int2/3
    public IActionResult GetInt2Product(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

위의 코드에서:

* 각 액션에는 `[HttpGet]` 속성이 포함되어 있으며, 이는 HTTP GET 요청에 대해서만 매칭됩니다.
* `GetProduct` 액션은 `"{id}"` 템플릿을 포함하고 있으므로 `id`는 컨트롤러의 `"api/[controller]"` 템플릿에 추가됩니다. 메서드 템플릿은 `"api/[controller]/{id}"`입니다. 따라서 이 액션은 `/api/test2/xyz`, `/api/test2/123`, `/api/test2/{any string}` 등의 형식의 GET 요청에만 매칭됩니다.
    ```C#
    [HttpGet("{id}")]   // GET /api/test2/xyz
    public IActionResult GetProduct(string id)
    {
    return ControllerContext.MyDisplayRouteInfo(id);
    }
    ```
* `GetIntProduct` 액션은 `"int/{id:int}"` 템플릿을 포함하고 있습니다. 템플릿의 `:int` 부분은 `id` 경로 값을 정수로 변환할 수 있는 문자열로 제한합니다. `/api/test2/int/abc`에 대한 GET 요청은:
  * 이 액션과 매칭되지 않습니다.
  * [404 Not Found](https://developer.mozilla.org/docs/Web/HTTP/Status/404) 오류를 반환합니다.
    ```C#
    [HttpGet("int/{id:int}")] // GET /api/test2/int/3
    public IActionResult GetIntProduct(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
    ```
* `GetInt2Product` 액션은 템플릿에 `{id}`를 포함하지만, `id`를 정수로 변환할 수 있는 값으로 제한하지 않습니다. `/api/test2/int2/abc`에 대한 GET 요청은:
  * 이 경로와 일치합니다.
  * 모델 바인딩이 `abc`를 정수로 변환하지 못합니다. 메서드의 `id` 매개변수는 정수입니다.
  * 모델 바인딩이 `abc`를 정수로 변환하지 못했기 때문에 [400 Bad Request](https://developer.mozilla.org/docs/Web/HTTP/Status/400)를 반환합니다.
    ```C#
    [HttpGet("int2/{id}")]  // GET /api/test2/int2/3
    public IActionResult GetInt2Product(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
    ```

속성 라우팅은 `HttpMethodAttribute` 속성을 사용할 수 있습니다. 예를 들어 `HttpPostAttribute`, `HttpPutAttribute` 및 `HttpDeleteAttribute` 등이 있습니다. 모든 [HTTP 메서드](#http-메서드-템플릿) 속성은 라우트 템플릿을 허용합니다. 다음 예제는 동일한 라우트 템플릿과 일치하는 두 개의 액션을 보여줍니다:

```C#
[ApiController]
public class MyProductsController : ControllerBase
{
    [HttpGet("/products3")]
    public IActionResult ListProducts()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [HttpPost("/products3")]
    public IActionResult CreateProduct(MyProduct myProduct)
    {
        return ControllerContext.MyDisplayRouteInfo(myProduct.Name);
    }
}
```

URL 경로 `/products3`를 사용하면:

* [HTTP 메서드](#http-메서드-템플릿)가 `GET`일 때 `MyProductsController.ListProducts` 액션이 실행됩니다.
* [HTTP 메서드](#http-메서드-템플릿)가 `POST`일 때 `MyProductsController.CreateProduct` 액션이 실행됩니다.

REST API를 빌드할 때, 액션이 모든 HTTP 메서드를 허용하기 때문에 `[Route(...)]`를 액션 메서드에 사용하는 경우는 드뭅니다. API가 지원하는 내용을 명확하게 하기 위해 더 구체적인 [HTTP 메서드 속성](#http-메서드-템플릿)을 사용하는 것이 좋습니다. REST API의 클라이언트는 특정 논리적 작업에 어떤 경로와 HTTP 메서드가 매핑되는지 알고 있어야 합니다.

REST API는 속성 라우팅을 사용하여 앱의 기능을 HTTP 메서드로 표현된 리소스 집합으로 모델링해야 합니다. 이는 GET과 POST와 같은 많은 작업이 동일한 논리적 리소스에서 동일한 URL을 사용하는 것을 의미합니다. 속성 라우팅은 API의 공개 엔드 포인트 레이아웃을 신중하게 설계할 수 있도록 필요한 제어 수준을 제공합니다.

속성 라우트는 특정 액션에 적용되므로, 라우트 템플릿 정의의 일부로 매개변수를 필수로 만들기가 쉽습니다. 다음 예제에서 `id`는 URL 경로의 일부로 필수입니다:

```C#
[ApiController]
public class Products2ApiController : ControllerBase
{
    [HttpGet("/products2/{id}", Name = "Products_List")]
    public IActionResult GetProduct(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

`Products2ApiController.GetProduct(int)` 액션:

* `/products2/3`와 같은 URL 경로로 실행됩니다.
* URL 경로 `/products2`로 실행되지 않습니다.

[[Consumes]](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.consumesattribute) 속성은 액션이 지원하는 요청 콘텐츠 유형을 제한할 수 있습니다. 자세한 내용은 [Consumes 속성을 사용하여 지원되는 요청 콘텐츠 유형 정의](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-8.0#consumes)를 참조하십시오.

 [라우팅](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0)에서 라우트 템플릿 및 관련 옵션에 대한 전체 설명을 참조하십시오.

`[ApiController]`에 대한 자세한 내용은 [ApiController 속성](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-8.0##apicontroller-attribute)을 참조하십시오.

## 라우트 이름

다음 코드는 `Products_List` 라우트 이름을 정의합니다:

```C#
[ApiController]
public class Products2ApiController : ControllerBase
{
    [HttpGet("/products2/{id}", Name = "Products_List")]
    public IActionResult GetProduct(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

라우트 이름은 특정 라우트를 기반으로 URL을 생성하는 데 사용할 수 있습니다. 라우트 이름:

* 라우팅의 URL 매칭 동작에 영향을 미치지 않습니다.
* URL 생성에만 사용됩니다.

라우트 이름은 앱 전역에서 고유해야 합니다.

위의 코드를 기본 전통적인 라우트와 비교하면, 기본 전통적인 라우트는 `id` 매개변수를 선택 사항으로 정의합니다(`{id?}`). API를 정확히 지정할 수 있는 능력은 `/products`와 `/products/5`를 서로 다른 액션으로 전달할 수 있다는 장점이 있습니다.

<a name="routing-combining-ref-label"></a>

## 속성 라우트 결합

속성 라우팅을 덜 반복적으로 만들기 위해, 컨트롤러의 라우트 속성과 개별 액션의 라우트 속성이 결합됩니다. 컨트롤러에 정의된 라우트 템플릿은 액션에 정의된 라우트 템플릿 앞에 추가됩니다. 컨트롤러에 라우트 속성을 배치하면 컨트롤러의 **모든** 액션이 속성 라우팅을 사용합니다.

```C#
[ApiController]
[Route("products")]
public class ProductsApiController : ControllerBase
{
    [HttpGet]
    public IActionResult ListProducts()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [HttpGet("{id}")]
    public IActionResult GetProduct(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

위의 예제에서:

* URL 경로 `/products`는 `ProductsApi.ListProducts`와 일치할 수 있습니다.
* URL 경로 `/products/5`는 `ProductsApi.GetProduct(int)`와 일치할 수 있습니다.

이 두 액션은 `[HttpGet]` 속성으로 표시되어 있으므로 HTTP `GET`에만 매칭됩니다.

액션에 적용된 라우트 템플릿이 `/` 또는 `~/`로 시작하면 컨트롤러에 적용된 라우트 템플릿과 결합되지 않습니다. 다음 예제는 기본 라우트와 유사한 URL 경로 집합과 일치합니다.

```C#
[Route("Home")]
public class HomeController : Controller
{
    [Route("")]
    [Route("Index")]
    [Route("/")]
    public IActionResult Index()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [Route("About")]
    public IActionResult About()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

위의 코드에서 `[Route]` 속성을 설명하는 표는 다음과 같습니다:

| 속성               | `[Route("Home")]`와 결합됨 | 라우트 템플릿 정의 |
| ----------------- | ------------ | --------- |
| `[Route("")]` | 예 | `"Home"` |
| `[Route("Index")]` | 예 | `"Home/Index"` |
| `[Route("/")]` | **아니요** | `""` |
| `[Route("About")]` | 예 | `"Home/About"` |

<a name="routing-ordering-ref-label"></a>
<a name="oar"></a>

### 속성 라우트 순서

라우팅은 트리를 구축하고 모든 엔드포인트를 동시에 매칭합니다:

* 라우트 항목은 이상적인 순서에 배치된 것처럼 작동합니다.
* 가장 구체적인 라우트가 더 일반적인 라우트보다 먼저 실행될 수 있습니다.

예를 들어, `blog/search/{topic}`과 같은 속성 라우트는 `blog/{*article}`과 같은 속성 라우트보다 구체적입니다. `blog/search/{topic}` 라우트는 기본적으로 더 구체적이기 때문에 우선 순위가 높습니다. [전통적인 라우팅](#전통적인-라우트-설정)을 사용할 때, 개발자는 원하는 순서대로 라우트를 배치할 책임이 있습니다.

속성 라우트는 `Order` 속성을 사용하여 순서를 구성할 수 있습니다. 모든 프레임워크 제공 [라우트 속성](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.routeattribute)은 `Order`를 포함합니다. 라우트는 `Order` 속성의 오름차순으로 처리됩니다. 기본 순서는 `0`입니다. `Order = -1`로 설정된 라우트는 순서가 설정되지 않은 라우트보다 먼저 실행됩니다. `Order = 1`로 설정된 라우트는 기본 라우트 순서 이후에 실행됩니다.

**Order에 의존하는 것은 피하십시오**. 앱의 URL 공간이 올바르게 라우팅되기 위해 명시적인 순서 값을 필요로 한다면, 클라이언트에게도 혼란을 줄 가능성이 큽니다. 일반적으로 속성 라우팅은 URL 매칭으로 올바른 라우트를 선택합니다. URL 생성의 기본 순서가 작동하지 않는 경우, `Order` 속성을 적용하는 것보다 라우트 이름을 사용하는 것이 일반적으로 더 간단합니다.

다음 두 컨트롤러는 모두 `/home`을 매칭하는 라우트를 정의합니다:

```C#
public class HomeController : Controller
{
    [Route("")]
    [Route("Home")]
    [Route("Home/Index")]
    [Route("Home/Index/{id?}")]
    public IActionResult Index(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }

    [Route("Home/About")]
    [Route("Home/About/{id?}")]
    public IActionResult About(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

```C#
public class HomeController : Controller
{
    [Route("")]
    [Route("Home")]
    [Route("Home/Index")]
    [Route("Home/Index/{id?}")]
    public IActionResult Index(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }

    [Route("Home/About")]
    [Route("Home/About/{id?}")]
    public IActionResult About(int? id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

위의 코드를 사용하면 `/home`을 요청하면 다음과 유사한 예외가 발생합니다:

```text
AmbiguousMatchException: The request matched multiple endpoints. Matches:

 WebMvcRouting.Controllers.HomeController.Index
 WebMvcRouting.Controllers.MyDemoController.MyIndex
```

라우트 속성 중 하나에 `Order`를 추가하면 모호성이 해결됩니다:

```C#
[Route("")]
[Route("Home", Order = 2)]
[Route("Home/MyIndex")]
public IActionResult MyIndex()
{
    return ControllerContext.MyDisplayRouteInfo();
}
```

위의 코드를 사용하면 `/home`이 `HomeController.Index` 엔드포인트를 실행합니다. `MyDemoController.MyIndex`에 도달하려면 `/home/MyIndex`를 요청해야 합니다. **참고**:

* 위의 코드는 잘못된 라우팅 설계의 예입니다. `Order` 속성을 설명하기 위해 사용되었습니다.
* `Order` 속성은 모호성을 해결할 뿐이며, 템플릿은 매칭될 수 없습니다. `[Route("Home")]` 템플릿을 제거하는 것이 좋습니다.

Razor Pages에서 라우트 순서에 대한 정보는 [Razor Pages 라우트 및 앱 규칙: 라우트 순서](https://learn.microsoft.com/en-us/aspnet/core/razor-pages/razor-pages-conventions?view=aspnetcore-8.0#route-order)를 참조하십시오.

일부 경우에는 모호한 라우트로 인해 HTTP 500 오류가 반환됩니다. `AmbiguousMatchException`을 발생시킨 엔드포인트를 확인하려면 [로그](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-8.0)를 사용하십시오.

## 라우트 템플릿에서의 토큰 대체 [controller], [action], [area]

편의를 위해 속성 라우트는 토큰을 대괄호(`[` 및 `]`)로 둘러싸서 *토큰 대체*를 지원합니다. `[action]`, `[area]`, `[controller]` 토큰은 라우트가 정의된 액션에서 액션 이름, 영역 이름, 컨트롤러 이름의 값으로 대체됩니다:

```C#
[Route("[controller]/[action]")]
public class Products0Controller : Controller
{
    [HttpGet]
    public IActionResult List()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }


    [HttpGet("{id}")]
    public IActionResult Edit(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

위의 코드에서:

```C#
[HttpGet]
public IActionResult List()
{
    return ControllerContext.MyDisplayRouteInfo();
}
```

* `/Products0/List`와 일치

```C#
[HttpGet("{id}")]
public IActionResult Edit(int id)
{
    return ControllerContext.MyDisplayRouteInfo(id);
}
```

* `/Products0/Edit/{id}`와 일치

토큰 대체는 속성 라우트를 구축하는 마지막 단계에서 발생합니다. 위의 예제는 다음 코드와 동일하게 동작합니다:

```C#
public class Products20Controller : Controller
{
    [HttpGet("[controller]/[action]")]  // Matches '/Products20/List'
    public IActionResult List()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [HttpGet("[controller]/[action]/{id}")]   // Matches '/Products20/Edit/{id}'
    public IActionResult Edit(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

속성 라우트는 상속과 결합될 수도 있습니다. 이는 토큰 대체와 결합될 때 강력한 기능을 제공합니다. 토큰 대체는 속성 라우트에 의해 정의된 라우트 이름에도 적용됩니다. `[Route("[controller]/[action]", Name="[controller]_[action]")]`는 각 액션에 대한 고유한 라우트 이름을 생성합니다:

```C#
[ApiController]
[Route("api/[controller]/[action]", Name = "[controller]_[action]")]
public abstract class MyBase2Controller : ControllerBase
{
}

public class Products11Controller : MyBase2Controller
{
    [HttpGet]                      // /api/products11/list
    public IActionResult List()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }

    [HttpGet("{id}")]             //    /api/products11/edit/3
    public IActionResult Edit(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

리터럴 토큰 대체 구분자 `[` 또는 `]`와 일치하려면 문자를 반복하여 이스케이프 처리합니다(`[[` 또는 `]]`).

<a name="routing-token-replacement-transformers-ref-label"></a>

### 매개변수 변환기를 사용하여 토큰 대체 사용자 지정

토큰 대체는 매개변수 변환기를 사용하여 사용자 지정할 수 있습니다. 매개변수 변환기는 `IOutboundParameterTransformer`을 구현하여 매개변수 값을 변환합니다. 예를 들어, 사용자 지정 `SlugifyParameterTransformer` 매개변수 변환기는 `SubscriptionManagement` 라우트 값을 `subscription-management`로 변경합니다:

```C#
using System.Text.RegularExpressions;

public class SlugifyParameterTransformer : IOutboundParameterTransformer
{
    public string? TransformOutbound(object? value)
    {
        if (value == null) { return null; }

        return Regex.Replace(value.ToString()!,
                             "([a-z])([A-Z])",
                             "$1-$2",
                             RegexOptions.CultureInvariant,
                             TimeSpan.FromMilliseconds(100)).ToLowerInvariant();
    }
}
```

`RouteTokenTransformerConvention`은 다음과 같은 응용 프로그램 모델 규칙입니다:

* 애플리케이션의 모든 속성 라우트에 매개변수 변환기를 적용합니다.
* 속성 라우트 토큰 값이 대체될 때 이를 사용자 지정합니다.

```C#
public class SubscriptionManagementController : Controller
{
    [HttpGet("[controller]/[action]")]
    public IActionResult ListAll()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

위의 `ListAll` 메서드는 `/subscription-management/list-all`와 일치합니다.

`RouteTokenTransformerConvention`은 옵션으로 등록됩니다:

```C#
using Microsoft.AspNetCore.Mvc.ApplicationModels;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllersWithViews(options =>
{
    options.Conventions.Add(new RouteTokenTransformerConvention(
                                 new SlugifyParameterTransformer()));
});

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapControllerRoute(name: "default",
               pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
```

[Slug에 대한 MDN 웹 문서](https://developer.mozilla.org/docs/Glossary/Slug)에서 Slug의 정의를 참조하십시오.

> [!WARNING]
> `RegularExpressions`를 사용하여 신뢰할 수 없는 입력을 처리할 때는 타임아웃을 전달하십시오. 악의적인 사용자가 `RegularExpressions`에 입력을 제공하여 [서비스 거부 공격](https://www.cisa.gov/news-events/news/understanding-denial-service-attacks)을 유발할 수 있습니다. ASP.NET Core 프레임워크 API는 `RegularExpressions`를 사용할 때 타임아웃을 전달합니다.

<a name="routing-multiple-routes-ref-label"></a>

### 다중 속성 라우트

속성 라우팅은 동일한 액션에 도달하는 여러 라우트를 정의하는 것을 지원합니다. 가장 일반적인 사용법은 기본 전통적인 라우트의 동작을 모방하는 것입니다. 다음 예제를 참조하십시오:

```C#
[Route("[controller]")]
public class Products13Controller : Controller
{
    [Route("")]     // Matches 'Products13'
    [Route("Index")] // Matches 'Products13/Index'
    public IActionResult Index()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
```

컨트롤러에 여러 라우트 속성을 두면 각 라우트 속성이 액션 메서드의 라우트 속성과 결합됩니다:

```C#
[Route("Store")]
[Route("[controller]")]
public class Products6Controller : Controller
{
    [HttpPost("Buy")]       // Matches 'Products6/Buy' and 'Store/Buy'
    [HttpPost("Checkout")]  // Matches 'Products6/Checkout' and 'Store/Checkout'
    public IActionResult Buy()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

모든 [HTTP 메서드](#http-메서드-템플릿) 라우트 제약 조건은 `IActionConstraint`를 구현합니다.

`IActionConstraint`를 구현하는 여러 라우트 속성이 액션에 배치된 경우:

* 각 액션 제약 조건은 컨트롤러에 적용된 라우트 템플릿과 결합됩니다.

```C#
[Route("api/[controller]")]
public class Products7Controller : ControllerBase
{
    [HttpPut("Buy")]        // Matches PUT 'api/Products7/Buy'
    [HttpPost("Checkout")]  // Matches POST 'api/Products7/Checkout'
    public IActionResult Buy()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

액션에 여러 라우트를 사용하는 것은 유용하고 강력해 보일 수 있지만, 앱의 URL 공간을 단순하고 잘 정의된 상태로 유지하는 것이 좋습니다. 액션에 여러 라우트를 사용하는 것은 필요할 때만 사용하십시오. 예를 들어, 기존 클라이언트를 지원하기 위해서입니다.

<a name="routing-attr-options"></a>

### 속성 라우트 선택적 매개변수, 기본값 및 제약 조건 지정

속성 라우트는 선택적 매개변수, 기본값 및 제약 조건을 지정하기 위해 전통적인 라우트와 동일한 인라인 구문을 지원합니다.

```C#
public class Products14Controller : Controller
{
    [HttpPost("product14/{id:int}")]
    public IActionResult ShowProduct(int id)
    {
        return ControllerContext.MyDisplayRouteInfo(id);
    }
}
```

위의 코드에서 `[HttpPost("product14/{id:int}")]`는 라우트 제약 조건을 적용합니다. `Products14Controller.ShowProduct` 액션은 `/product14/3`과 같은 URL 경로에만 일치합니다. 라우트 템플릿의 `{id:int}` 부분은 해당 세그먼트를 정수로만 제한합니다.

자세한 라우트 템플릿 구문 설명은 [라우트 템플릿 참조](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#route-template-reference)를 참조하십시오.

<a name="routing-cust-rt-attr-irt-ref-label"></a>

### IRouteTemplateProvider를 사용하여 사용자 지정 라우트 속성

모든 [라우트 속성](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-8.0#rt6)은 `IRouteTemplateProvider`을 구현합니다. ASP.NET Core 런타임은:

* 앱 시작 시 컨트롤러 클래스와 액션 메서드에서 속성을 찾습니다.
* `IRouteTemplateProvider`를 구현하는 속성을 사용하여 초기 라우트 집합을 구축합니다.

`IRouteTemplateProvider`를 구현하여 사용자 지정 라우트 속성을 정의합니다. 각 `IRouteTemplateProvider`는 사용자 지정 라우트 템플릿, 순서 및 이름을 사용하여 단일 라우트를 정의할 수 있습니다:

```C#
public class MyApiControllerAttribute : Attribute, IRouteTemplateProvider
{
    public string Template => "api/[controller]";
    public int? Order => 2;
    public string Name { get; set; } = string.Empty;
}

[MyApiController]
[ApiController]
public class MyTestApiController : ControllerBase
{
    // GET /api/MyTestApi
    [HttpGet]
    public IActionResult Get()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

위의 `Get` 메서드는 `Order = 2, Template = api/MyTestApi`를 반환합니다.

<a name="routing-app-model-ref-label"></a>

### 애플리케이션 모델을 사용하여 속성 라우트 사용자 지정

애플리케이션 모델:

* `Program.cs`에서 시작 시 생성되는 객체 모델입니다.
* 앱의 액션을 라우팅하고 실행하는 데 사용되는 모든 메타데이터를 포함합니다.

애플리케이션 모델은 라우트 속성에서 수집된 모든 데이터를 포함합니다. 라우트 속성에서 수집된 데이터는 `IRouteTemplateProvider` 구현에 의해 제공됩니다. 규칙은:

* 애플리케이션 모델을 수정하여 라우팅 동작을 사용자 지정할 수 있도록 작성될 수 있습니다.
* 앱 시작 시 읽습니다.

이 섹션에서는 애플리케이션 모델을 사용하여 라우팅을 사용자 지정하는 기본 예제를 보여줍니다. 다음 코드는 라우트가 프로젝트의 폴더 구조와 대략 일치하도록 만듭니다.

```C#
public class NamespaceRoutingConvention : Attribute, IControllerModelConvention
{
    private readonly string _baseNamespace;

    public NamespaceRoutingConvention(string baseNamespace)
    {
        _baseNamespace = baseNamespace;
    }

    public void Apply(ControllerModel controller)
    {
        var hasRouteAttributes = controller.Selectors.Any(selector =>
                                                selector.AttributeRouteModel != null);
        if (hasRouteAttributes)
        {
            return;
        }

        var namespc = controller.ControllerType.Namespace;
        if (namespc == null)
            return;
        var template = new StringBuilder();
        template.Append(namespc, _baseNamespace.Length + 1,
                        namespc.Length - _baseNamespace.Length - 1);
        template.Replace('.', '/');
        template.Append("/[controller]/[action]/{id?}");

        foreach (var selector in controller.Selectors)
        {
            selector.AttributeRouteModel = new AttributeRouteModel()
            {
                Template = template.ToString()
            };
        }
    }
}
```

다음 코드는 속성 라우트된 컨트롤러에 네임스페이스 규칙을 적용하지 않도록 합니다:

```C#
public void Apply(ControllerModel controller)
{
    var hasRouteAttributes = controller.Selectors.Any(selector =>
                                            selector.AttributeRouteModel != null);
    if (hasRouteAttributes)
    {
        return;
    }
```

예를 들어, 다음 컨트롤러는 `NamespaceRoutingConvention`을 사용하지 않습니다:

```C#
[Route("[controller]/[action]/{id?}")]
public class ManagersController : Controller
{
    // /managers/index
    public IActionResult Index()
    {
        var template = ControllerContext.ActionDescriptor.AttributeRouteInfo?.Template;
        return Content($"Index- template:{template}");
    }

    public IActionResult List(int? id)
    {
        var path = Request.Path.Value;
        return Content($"List- Path:{path}");
    }
}
```

`NamespaceRoutingConvention.Apply` 메서드:

* 컨트롤러가 속성 라우트된 경우 아무 것도 하지 않습니다.
* 기본 `namespace`가 제거된 `namespace`를 기반으로 컨트롤러 템플릿을 설정합니다.

`NamespaceRoutingConvention`은 `Program.cs`에서 적용될 수 있습니다:

```C#
using My.Application.Controllers;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllersWithViews(options =>
{
    options.Conventions.Add(
     new NamespaceRoutingConvention(typeof(HomeController).Namespace!));
});

var app = builder.Build();
```

예를 들어, 다음 컨트롤러를 고려하십시오:

```C#
using Microsoft.AspNetCore.Mvc;

namespace My.Application.Admin.Controllers
{
    public class UsersController : Controller
    {
        // GET /admin/controllers/users/index
        public IActionResult Index()
        {
            var fullname = typeof(UsersController).FullName;
            var template = 
                ControllerContext.ActionDescriptor.AttributeRouteInfo?.Template;
            var path = Request.Path.Value;

            return Content($"Path: {path} fullname: {fullname}  template:{template}");
        }

        public IActionResult List(int? id)
        {
            var path = Request.Path.Value;
            return Content($"Path: {path} ID:{id}");
        }
    }
}
```

위의 코드에서:

* 기본 `namespace`는 `My.Application`입니다.
* 이전 컨트롤러의 전체 이름은 `My.Application.Admin.Controllers.UsersController`입니다.
* `NamespaceRoutingConvention`은 컨트롤러의 템플릿을 `Admin/Controllers/Users/[action]/{id?}`로 설정합니다.

`NamespaceRoutingConvention`은 컨트롤러에 속성으로도 적용될 수 있습니다:

```C#
[NamespaceRoutingConvention("My.Application")]
public class TestController : Controller
{
    // /admin/controllers/test/index
    public IActionResult Index()
    {
        var template = ControllerContext.ActionDescriptor.AttributeRouteInfo?.Template;
        var actionname = ControllerContext.ActionDescriptor.ActionName;
        return Content($"Action- {actionname} template:{template}");
    }

    public IActionResult List(int? id)
    {
        var path = Request.Path.Value;
        return Content($"List- Path:{path}");
    }
}
```

<a name="routing-mixed-ref-label"></a>

## 혼합 라우팅: 속성 라우팅 대 전통적인 라우팅

ASP.NET Core 앱은 전통적인 라우팅과 속성 라우팅을 혼합하여 사용할 수 있습니다. 브라우저에 HTML 페이지를 제공하는 컨트롤러에는 전통적인 라우트를, REST API를 제공하는 컨트롤러에는 속성 라우트를 사용하는 것이 일반적입니다.

액션은 전통적으로 라우트되거나 속성으로 라우트됩니다. 컨트롤러나 액션에 라우트를 지정하면 속성으로 라우트됩니다. 속성 라우트를 정의하는 액션은 전통적인 라우트를 통해 도달할 수 없으며 그 반대도 마찬가지입니다. 컨트롤러에 있는 ***모든*** 라우트 속성은 컨트롤러의 ***모든*** 액션을 속성 라우트로 만듭니다.

속성 라우팅과 전통적인 라우팅은 동일한 라우팅 엔진을 사용합니다.

## 특수 문자와 라우팅

특수 문자와 라우팅을 사용하면 예상치 못한 결과가 발생할 수 있습니다. 예를 들어, 다음과 같은 액션 메서드를 가진 컨트롤러를 고려해 보십시오:

```csharp
[HttpGet("{id?}/name")]
public async Task<ActionResult<string>> GetName(string id)
{
    var todoItem = await _context.TodoItems.FindAsync(id);

    if (todoItem == null || todoItem.Name == null)
    {
        return NotFound();
    }

    return todoItem.Name;
}
```

`string id`에 다음과 같은 인코딩된 값이 포함될 때 예상치 못한 결과가 발생할 수 있습니다:

| ASCII  | 인코딩된 값 |
| ----| ---------- |
| `/` | `%2F`  |
| ` ` | `+`  |

라우트 매개변수가 항상 URL 디코딩되는 것은 아닙니다. 이 문제는 미래에 해결될 수 있습니다. 자세한 내용은 [이 GitHub 이슈](https://github.com/dotnet/aspnetcore/issues/11544)를 참조하십시오.

<a name="routing-url-gen-ref-label"></a>
<a name="ambient"></a>

## URL 생성 및 상위 값

앱은 라우팅 URL 생성 기능을 사용하여 액션에 대한 URL 링크를 생성할 수 있습니다. URL을 생성하면 [하드 코딩](https://wikipedia.org/wiki/Hard_coding)된 URL을 제거하여 코드가 더욱 강력하고 유지 보수 가능하게 됩니다. 이 섹션은 MVC에서 제공하는 URL 생성 기능에 중점을 두며 URL 생성 방식의 기본 사항만 다룹니다. URL 생성에 대한 자세한 설명은 [라우팅](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0)을 참조하십시오.

`IUrlHelper` 인터페이스는 MVC와 라우팅 간의 URL 생성에 대한 기본 요소입니다. `IUrlHelper`의 인스턴스는 컨트롤러, 뷰 및 뷰 구성 요소에서 `Url` 속성을 통해 사용할 수 있습니다.

다음 예제에서는 `IUrlHelper` 인터페이스를 `Controller.Url` 속성을 통해 사용하여 다른 액션에 대한 URL을 생성합니다.

```C#
public class UrlGenerationController : Controller
{
    public IActionResult Source()
    {
        // Generates /UrlGeneration/Destination
        var url = Url.Action("Destination");
        return ControllerContext.MyDisplayRouteInfo("", $" URL = {url}");
    }

    public IActionResult Destination()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
}
```

앱이 기본 전통적인 라우트를 사용하는 경우 `url` 변수의 값은 URL 경로 문자열 `/UrlGeneration/Destination`입니다. 이 URL 경로는 라우팅이 현재 요청의 라우트 값인 **상위 값**과 `Url.Action`에 전달된 값을 결합하여 생성됩니다:

``` text
상위 값: { controller = "UrlGeneration", action = "Source" }
Url.Action에 전달된 값: { controller = "UrlGeneration", action = "Destination" }
라우트 템플릿: {controller}/{action}/{id?}

결과: /UrlGeneration/Destination
```

라우트 템플릿의 각 라우트 매개변수는 값 및 상위 값과 이름을 일치시켜 대체됩니다. 값이 없는 라우트 매개변수는:

* 기본값이 있는 경우 기본값을 사용합니다.
* 선택적인 경우 건너뜁니다. 예를 들어, 라우트 템플릿 `{controller}/{action}/{id?}`의 `id`와 같습니다.

필수 라우트 매개변수에 해당하는 값이 없는 경우 URL 생성이 실패합니다. URL 생성이 라우트에 대해 실패하면 다음 라우트를 시도하며, 모든 라우트를 시도하거나 일치하는 항목을 찾을 때까지 계속됩니다.

`Url.Action`의 이전 예제는 [전통적인 라우팅](#전통적인-라우트-설정)을 가정합니다. URL 생성은 [속성 라우팅](#rest-api를-위한-속성-라우팅)과 유사하게 작동하지만 개념은 다릅니다. 전통적인 라우팅에서는:

* 라우트 값이 템플릿을 확장하는 데 사용됩니다.
* `controller`와 `action`의 라우트 값이 일반적으로 해당 템플릿에 나타납니다. 이는 라우팅이 규칙에 맞는 URL을 사용하기 때문에 작동합니다.

다음 예제는 속성 라우팅을 사용합니다:

```C#
public class UrlGenerationAttrController : Controller
{
    [HttpGet("custom")]
    public IActionResult Source()
    {
        var url = Url.Action("Destination");
        return ControllerContext.MyDisplayRouteInfo("", $" URL = {url}");
    }

    [HttpGet("custom/url/to/destination")]
    public IActionResult Destination()
    {
       return ControllerContext.MyDisplayRouteInfo();
    }
}
```

위의 코드에서 `Source` 액션은 `custom/url/to/destination`을 생성합니다.

`LinkGenerator`는 `IUrlHelper`의 대안으로 ASP.NET Core 3.0에 추가되었습니다. `LinkGenerator`는 유사하지만 더 유연한 기능을 제공합니다. `IUrlHelper`의 각 메서드에는 `LinkGenerator`의 해당 메서드군이 있습니다.

### 액션 이름으로 URL 생성

[Url.Action](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.iurlhelper.action), [LinkGenerator.GetPathByAction](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.routing.controllerlinkgeneratorextensions.getpathbyaction), 및 관련 모든 오버로드는 컨트롤러 이름과 액션 이름을 지정하여 대상 엔드포인트를 생성하도록 설계되었습니다.

`Url.Action`을 사용할 때 현재 라우트 값인 `controller`와 `action` 값은 런타임에 제공됩니다:

* `controller`와 `action` 값은 [상위 값](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-8.0#ambient) 및 값의 일부입니다. `Url.Action` 메서드는 항상 현재 `action` 및 `controller` 값을 사용하여 현재 액션으로 라우팅되는 URL 경로를 생성합니다.

라우팅은 URL을 생성할 때 제공되지 않은 정보를 채우기 위해 상위 값의 값을 사용하려고 시도합니다. `{a}/{b}/{c}/{d}`와 같은 라우트와 상위 값 `{ a = Alice, b = Bob, c = Carol, d = David }`를 고려하십시오:

* 라우팅은 추가 값 없이 URL을 생성할 충분한 정보를 가지고 있습니다.
* 라우팅은 모든 라우트 매개변수에 값이 있기 때문에 충분한 정보를 가지고 있습니다.

값 `{ d = Donovan }`가 추가되면:

* 값 `{ d = David }`는 무시됩니다.
* 생성된 URL 경로는 `Alice/Bob/Carol/Donovan`입니다.

**경고**: URL 경로는 계층적입니다. 위의 예에서 값 `{ c = Cheryl }`가 추가되면:

* 값 `{ c = Carol, d = David }`는 무시됩니다.
* 더 이상 `d`에 대한 값이 없으므로 URL 생성이 실패합니다.
* URL을 생성하려면 원하는 `c` 및 `d` 값을 지정해야 합니다.

기본 라우트 `{controller}/{action}/{id?}`에서 이 문제에 직면할 것으로 예상할 수 있습니다. 실제로 `Url.Action`이 항상 `controller`와 `action` 값을 명시적으로 지정하기 때문에 이 문제는 드뭅니다.

여러 오버로드된 [Url.Action](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.iurlhelper.action) 메서드는 라우트 값 객체를 사용하여 `controller`와 `action` 외의 라우트 매개변수에 대한 값을 제공합니다. 라우트 값 객체는 종종 `id`와 함께 사용됩니다. 예를 들어, `Url.Action("Buy", "Products", new { id = 17 })`. 라우트 값 객체는:

* 관례적으로 익명 타입의 객체입니다.
* `IDictionary<>` 또는 [POCO](https://wikipedia.org/wiki/Plain_old_CLR_object)일 수 있습니다.

라우트 매개변수와 일치하지 않는 추가 라우트 값은 쿼리 문자열에 추가됩니다.

```C#
public IActionResult Index()
{
    var url = Url.Action("Buy", "Products", new { id = 17, color = "red" });
    return Content(url!);
}
```

위의 코드는 `/Products/Buy/17?color=red`를 생성합니다.

다음 코드는 절대 URL을 생성합니다:

```C#
public IActionResult Index2()
{
    var url = Url.Action("Buy", "Products", new { id = 17 }, protocol: Request.Scheme);
    // Returns https://localhost:5001/Products/Buy/17
    return Content(url!);
}
```

절대 URL을 생성하려면 다음 중 하나를 사용하십시오:

* `protocol`을 수락하는 오버로드. 예를 들어, 위의 코드.
* 기본적으로 절대 URI를 생성하는 [LinkGenerator.GetUriByAction](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.routing.controllerlinkgeneratorextensions.geturibyaction).

<a name="routing-gen-urls-route-ref-label"></a>

### 라우트로 URL 생성

위의 코드는 컨트롤러와 액션 이름을 전달하여 URL을 생성하는 것을 보여주었습니다. `IUrlHelper`는 [Url.RouteUrl](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.iurlhelper.routeurl) 메서드 군도 제공합니다. 이 메서드는 [Url.Action](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.iurlhelper.action)과 유사하지만, 현재 `action`과 `controller` 값을 라우트 값에 복사하지 않습니다. `Url.RouteUrl`의 가장 일반적인 사용법:

* URL을 생성하기 위해 라우트 이름을 지정합니다.
* 일반적으로 컨트롤러나 액션 이름을 지정하지 않습니다.

```C#
public class UrlGeneration2Controller : Controller
{
    [HttpGet("")]
    public IActionResult Source()
    {
        var url = Url.RouteUrl("Destination_Route");
        return ControllerContext.MyDisplayRouteInfo("", $" URL = {url}");
    }

    [HttpGet("custom/url/to/destination2", Name = "Destination_Route")]
    public IActionResult Destination()
    {
        return ControllerContext.MyDisplayRouteInfo();
    }
```

다음 Razor 파일은 `Destination_Route`로 HTML 링크를 생성합니다:

```cshtml
<h1>Test Links</h1>

<ul>
    <li><a href="@Url.RouteUrl("Destination_Route")">Test Destination_Route</a></li>
</ul>
```

<a name="routing-gen-urls-html-ref-label"></a>

### HTML 및 Razor에서 URL 생성

`IHtmlHelper`는 각각 `<form>` 및 `<a>` 요소를 생성하기 위해 `Html.BeginForm` 및 `Html.ActionLink` 메서드를 제공합니다. 이 메서드는 `Url.Action` 메서드를 사용하여 URL을 생성하며 유사한 인수를 수락합니다. `HtmlHelper`의 `Url.RouteUrl` 동반자는 `Html.BeginRouteForm` 및 `Html.RouteLink`로, 유사한 기능을 제공합니다.

TagHelper는 `form` TagHelper 및 `<a>` TagHelper를 통해 URL을 생성합니다. 이 두 TagHelper는 `IUrlHelper`를 구현에 사용합니다. 자세한 내용은 [폼에서의 Tag Helper](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-8.0)를 참조하십시오.

뷰 내에서는 `IUrlHelper`가 위의 사항들로 커버되지 않는 모든 즉석 URL 생성을 위해 `Url` 속성을 통해 사용할 수 있습니다.

<a name="routing-gen-urls-action-ref-label"></a>

### 액션 결과에서 URL 생성

앞서 예제에서는 컨트롤러에서 `IUrlHelper`를 사용하는 방법을 보여주었습니다. 컨트롤러에서 가장 일반적인 사용법은 액션 결과의 일부로 URL을 생성하는 것입니다.

`ControllerBase` 및 `Controller` 기본 클래스는 다른 액션을 참조하는 액션 결과에 대한 편의 메서드를 제공합니다. 사용자 입력을 수락한 후 리디렉션하는 것이 일반적인 사용법입니다:

```C#
[HttpPost]
[ValidateAntiForgeryToken]
public IActionResult Edit(int id, Customer customer)
{
    if (ModelState.IsValid)
    {
        // Update DB with new details.
        ViewData["Message"] = $"Successful edit of customer {id}";
        return RedirectToAction("Index");
    }
    return View(customer);
}
```

`RedirectToAction` 및 `CreatedAtAction`과 같은 액션 결과 팩토리 메서드는 `IUrlHelper`의 메서드와 유사한 패턴을 따릅니다.

<a name="routing-dedicated-ref-label"></a>

### 전용 전통적인 라우트의 특별 사례

[전통적인 라우팅](#전통적인-라우트-설정)은 [전용 전통적인 라우트](#다중-전통적인-라우트)라는 특수한 종류의 라우트 정의를 사용할 수 있습니다. 다음 예제에서 `blog`라는 라우트는 전용 전통적인 라우트입니다:

```C#
app.MapControllerRoute(name: "blog",
                pattern: "blog/{*article}",
                defaults: new { controller = "Blog", action = "Article" });
app.MapControllerRoute(name: "default",
               pattern: "{controller=Home}/{action=Index}/{id?}");
```

위의 라우트 정의를 사용하면 `Url.Action("Index", "Home")`이 URL 경로 `/`를 생성합니다. 이유는 무엇일까요? `{ controller = Home, action = Index }`의 라우트 값으로 `blog`를 사용하여 URL을 생성하면 `/blog?action=Index&controller=Home`이 결과가 될 것이라고 추측할 수 있습니다.

[전용 전통적인 라우트](#다중-전통적인-라우트)는 URL 생성을 위해 너무 [탐욕스럽게](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#greedy) 되지 않도록 기본값에 해당하는 라우트 매개변수가 없는 특수 동작에 의존합니다. 이 경우 기본값은 `{ controller = Blog, action = Article }`이며, `controller`나 `action`이 라우트 매개변수로 나타나지 않습니다. 라우팅이 URL 생성을 수행할 때 제공된 값은 기본값과 일치해야 합니다. `blog`를 사용한 URL 생성이 `{ controller = Home, action = Index }` 값이 `{ controller = Blog, action = Article }`와 일치하지 않기 때문에 실패합니다. 그런 다음 라우팅은 `default`를 시도하여 성공합니다.

<a name="routing-areas-ref-label"></a>

## 영역

[영역](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/areas?view=aspnetcore-8.0)은 관련 기능을 그룹으로 조직하기 위해 사용되는 MVC 기능입니다:

* 컨트롤러 액션을 위한 라우팅 네임스페이스.
* 뷰를 위한 폴더 구조.

영역을 사용하면 앱에 이름이 같은 여러 컨트롤러가 있을 수 있으며, 각 컨트롤러는 다른 영역을 가집니다. 영역을 사용하면 `controller`와 `action` 외에 `area` 라우트 매개변수를 추가하여 라우팅에 계층 구조를 생성합니다. 이 섹션에서는 라우팅과 영역의 상호 작용을 설명합니다. 영역이 뷰와 함께 사용되는 방법에 대한 자세한 내용은 [영역](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/areas?view=aspnetcore-8.0)을 참조하십시오.

다음 예제는 기본 전통적인 라우트와 `Blog`라는 영역 라우트를 사용하도록 MVC를 구성합니다:

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllersWithViews();

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{    
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapAreaControllerRoute("blog_route", "Blog",
        "Manage/{controller}/{action}/{id?}");
app.MapControllerRoute("default_route", "{controller}/{action}/{id?}");

app.Run();
```

위의 코드에서 `MapAreaControllerRoute`가 호출되어 `"blog_route"`를 생성합니다. 두 번째 매개변수인 `"Blog"`는 영역 이름입니다.

`/Manage/Users/AddUser`와 같은 URL 경로를 일치시킬 때, `"blog_route"` 라우트는 `{ area = Blog, controller = Users, action = AddUser }` 라우트 값을 생성합니다. `area` 라우트 값은 `area`에 대한 기본값에 의해 생성됩니다. `MapAreaControllerRoute`에 의해 생성된 라우트는 다음과 같습니다:

```C#
app.MapControllerRoute("blog_route", "Manage/{controller}/{action}/{id?}",
        defaults: new { area = "Blog" }, constraints: new { area = "Blog" });
app.MapControllerRoute("default_route", "{controller}/{action}/{id?}");
```

`MapAreaControllerRoute`는 제공된 영역 이름인 이 경우 `Blog`를 사용하여 `area`에 대한 기본값과 제약 조건을 모두 사용하는 라우트를 생성합니다. 기본값은 라우트가 항상 `{ area = Blog, ... }`을 생성하도록 보장하며, 제약 조건은 URL 생성을 위해 `{ area = Blog, ... }` 값을 요구합니다.

전통적인 라우팅은 순서에 의존합니다. 일반적으로 영역이 있는 라우트는 영역이 없는 라우트보다 더 구체적이므로 더 먼저 배치해야 합니다.

위의 예를 사용하여 `{ area = Blog, controller = Users, action = AddUser }` 라우트 값은 다음 액션과 일치합니다:

```C#
using Microsoft.AspNetCore.Mvc;

namespace MyApp.Namespace1
{
    [Area("Blog")]
    public class UsersController : Controller
    {
        // GET /manage/users/adduser
        public IActionResult AddUser()
        {
            var area = ControllerContext.ActionDescriptor.RouteValues["area"];
            var actionName = ControllerContext.ActionDescriptor.ActionName;
            var controllerName = ControllerContext.ActionDescriptor.ControllerName;

            return Content($"area name:{area}" +
                $" controller:{controllerName}  action name: {actionName}");
        }        
    }
}
```

[[Area]](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.areaattribute) 속성이 컨트롤러를 영역의 일부로 표시하는 것입니다. 이 컨트롤러는 `Blog` 영역에 있습니다. `[Area]` 속성이 없는 컨트롤러는 어떤 영역의 구성원도 아니며, 라우팅에 의해 `area` 라우트 값이 제공될 때 일치하지 **않습니다**. 다음 예제에서는 첫 번째로 나열된 컨트롤러만 `{ area = Blog, controller = Users, action = AddUser }` 라우트 값과 일치할 수 있습니다.

```C#
using Microsoft.AspNetCore.Mvc;

namespace MyApp.Namespace1
{
    [Area("Blog")]
    public class UsersController : Controller
    {
        // GET /manage/users/adduser
        public IActionResult AddUser()
        {
            var area = ControllerContext.ActionDescriptor.RouteValues["area"];
            var actionName = ControllerContext.ActionDescriptor.ActionName;
            var controllerName = ControllerContext.ActionDescriptor.ControllerName;

            return Content($"area name:{area}" +
                $" controller:{controllerName}  action name: {actionName}");
        }        
    }
}
```

```C#
using Microsoft.AspNetCore.Mvc;

namespace MyApp.Namespace2
{
    // Matches { area = Zebra, controller = Users, action = AddUser }
    [Area("Zebra")]
    public class UsersController : Controller
    {
        // GET /zebra/users/adduser
        public IActionResult AddUser()
        {
            var area = ControllerContext.ActionDescriptor.RouteValues["area"];
            var actionName = ControllerContext.ActionDescriptor.ActionName;
            var controllerName = ControllerContext.ActionDescriptor.ControllerName;

            return Content($"area name:{area}" +
                $" controller:{controllerName}  action name: {actionName}");
        }        
    }
}
```

```C#
using Microsoft.AspNetCore.Mvc;

namespace MyApp.Namespace3
{
    // Matches { area = string.Empty, controller = Users, action = AddUser }
    // Matches { area = null, controller = Users, action = AddUser }
    // Matches { controller = Users, action = AddUser }
    public class UsersController : Controller
    {
        // GET /users/adduser
        public IActionResult AddUser()
        {
            var area = ControllerContext.ActionDescriptor.RouteValues["area"];
            var actionName = ControllerContext.ActionDescriptor.ActionName;
            var controllerName = ControllerContext.ActionDescriptor.ControllerName;

            return Content($"area name:{area}" +
                $" controller:{controllerName}  action name: {actionName}");
        }
    }
}
```

여기에 각 컨트롤러의 네임스페이스를 완성하기 위해 보여줍니다. 위의 컨트롤러가 동일한 네임스페이스를 사용하면 컴파일러 오류가 발생합니다. 클래스 네임스페이스는 MVC의 라우팅에 영향을 미치지 않습니다.

첫 번째와 두 번째 컨트롤러는 영역의 구성원이며, 해당 영역 이름이 라우팅에 의해 제공될 때만 일치합니다. 세 번째 컨트롤러는 어떤 영역의 구성원이 아니며, 라우팅에 의해 `area` 값이 제공되지 않을 때만 일치할 수 있습니다.

<a name="aa"></a>

값이 *없는* 일치 관점에서, `area` 값이 없다는 것은 `area` 값이 null 또는 빈 문자열인 것과 같습니다.

영역 내에서 액션을 실행할 때, 라우트 값 `area`는 URL 생성을 위해 라우팅에 사용할 수 있는 [상위 값](#ambient)으로 사용할 수 있습니다. 기본적으로 영역은 다음 샘플에 의해 입증된 대로 URL 생성을 위해 *끈적거리는* 동작을 합니다.

```C#
app.MapAreaControllerRoute(name: "duck_route",
                                     areaName: "Duck",
                                     pattern: "Manage/{controller}/{action}/{id?}");
app.MapControllerRoute(name: "default",
                             pattern: "Manage/{controller=Home}/{action=Index}/{id?}");
```

```C#
using Microsoft.AspNetCore.Mvc;

namespace MyApp.Namespace4
{
    [Area("Duck")]
    public class UsersController : Controller
    {
        // GET /Manage/users/GenerateURLInArea
        public IActionResult GenerateURLInArea()
        {
            // Uses the 'ambient' value of area.
            var url = Url.Action("Index", "Home");
            // Returns /Manage/Home/Index
            return Content(url);
        }

        // GET /Manage/users/GenerateURLOutsideOfArea
        public IActionResult GenerateURLOutsideOfArea()
        {
            // Uses the empty value for area.
            var url = Url.Action("Index", "Home", new { area = "" });
            // Returns /Manage
            return Content(url);
        }
    }
}
```

다음 코드는 `/Zebra/Users/AddUser`에 대한 URL을 생성합니다:

```C#
public class HomeController : Controller
{
    public IActionResult About()
    {
        var url = Url.Action("AddUser", "Users", new { Area = "Zebra" });
        return Content($"URL: {url}");
    }
```

<a name="action"></a>

## 액션 정의

[NonAction](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.nonactionattribute) 속성이 있는 공용 메서드를 제외한 컨트롤러의 공용 메서드는 액션입니다.

## 샘플 코드

* [MyDisplayRouteInfo](https://github.com/Rick-Anderson/RouteInfo/blob/master/Microsoft.Docs.Samples.RouteInfo/ControllerContextExtensions.cs) is provided by the [Rick.Docs.Samples.RouteInfo](https://www.nuget.org/packages/Rick.Docs.Samples.RouteInfo) NuGet package and displays route information.
* [샘플 코드 보기 또는 다운로드](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/mvc/controllers/routing/samples/3.x) ([샘플 다운로드 방법](xref:index#how-to-download-a-sample))

## 디버그 진단

자세한 라우팅 진단 출력을 위해 `Logging:LogLevel:Microsoft`를 `Debug`로 설정하십시오. 개발 환경에서는 `appsettings.Development.json`에서 로그 레벨을 설정하십시오:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Debug",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  }
}
```

---
## 출처
[Routing to controller actions in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-8.0)

---
## [다음](./06_DI_Controller.md)
