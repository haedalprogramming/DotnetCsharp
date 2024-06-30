# Handle requests with controllers in ASP.NET Core MVC

## 목차
- [Handle requests with controllers in ASP.NET Core MVC](#handle-requests-with-controllers-in-aspnet-core-mvc)
  - [목차](#목차)
  - [컨트롤러란 무엇인가?](#컨트롤러란-무엇인가)
  - [액션 정의하기](#액션-정의하기)
    - [컨트롤러 헬퍼 메서드](#컨트롤러-헬퍼-메서드)
      - [1. 빈 응답 본문을 반환하는 메서드](#1-빈-응답-본문을-반환하는-메서드)
      - [2. 미리 정의된 콘텐츠 유형으로 비어 있지 않은 응답 본문을 반환하는 메서드](#2-미리-정의된-콘텐츠-유형으로-비어-있지-않은-응답-본문을-반환하는-메서드)
      - [3. 클라이언트와 협상된 콘텐츠 유형으로 비어 있지 않은 응답 본문을 반환하는 메서드](#3-클라이언트와-협상된-콘텐츠-유형으로-비어-있지-않은-응답-본문을-반환하는-메서드)
    - [횡단 관심사](#횡단-관심사)
  - [출처](#출처)
  - [다음](#다음)

---

컨트롤러, 액션 및 액션 결과는 개발자가 ASP.NET Core MVC를 사용하여 애플리케이션을 빌드하는 방법의 기본적인 부분입니다.

## 컨트롤러란 무엇인가?

컨트롤러는 일련의 액션을 정의하고 그룹화하는 데 사용됩니다. 액션(또는 *액션 메서드*)은 요청을 처리하는 컨트롤러의 메서드입니다. 컨트롤러는 유사한 액션들을 논리적으로 그룹화합니다. 이러한 액션의 집합을 통해 라우팅, 캐싱, 권한 부여와 같은 공통 규칙을 집합적으로 적용할 수 있습니다. 요청은 [라우팅](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-8.0)을 통해 액션에 매핑됩니다. 컨트롤러는 요청당 한 번씩 활성화되고 처분됩니다.

컨벤션에 따라, 컨트롤러 클래스는:

* 프로젝트의 루트 수준 *Controllers* 폴더에 위치합니다.
* `Microsoft.AspNetCore.Mvc.Controller`를 상속받습니다.

컨트롤러는 인스턴스화할 수 있는 클래스이며, 다음 조건 중 하나 이상이 참입니다:

* 클래스 이름이 `Controller`로 끝납니다.
* 클래스가 이름이 `Controller`로 끝나는 클래스를 상속받습니다.
* `[Controller]` 특성이 클래스에 적용됩니다.

컨트롤러 클래스는 `[NonController]` 특성이 적용되지 않아야 합니다.

컨트롤러는 [명시적 종속성 원칙](https://learn.microsoft.com/en-us/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)을 따라야 합니다. 이 원칙을 구현하는 방법에는 몇 가지가 있습니다. 여러 컨트롤러 액션이 동일한 서비스를 필요로 하는 경우, [생성자 주입](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/dependency-injection?view=aspnetcore-8.0#constructor-injection)을 사용하여 이러한 종속성을 요청하는 것을 고려하십시오. 서비스가 단일 액션 메서드에서만 필요하다면, [액션 주입](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/dependency-injection?view=aspnetcore-8.0#action-injection-with-fromservices)을 사용하여 종속성을 요청하는 것을 고려하십시오.

**M**odel-**V**iew-**C**ontroller 패턴 내에서, 컨트롤러는 요청의 초기 처리와 모델의 인스턴스화를 담당합니다. 일반적으로 비즈니스 결정은 모델 내에서 수행되어야 합니다.

컨트롤러는 모델의 처리 결과(있다면)를 가져와 적절한 뷰 및 관련 뷰 데이터를 반환하거나 API 호출의 결과를 반환합니다. 자세한 내용은 [ASP.NET Core MVC 개요](https://learn.microsoft.com/en-us/aspnet/core/mvc/overview?view=aspnetcore-8.0) 및 [ASP.NET Core MVC 및 Visual Studio 시작하기](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0)를 참조하십시오.

컨트롤러는 *UI 수준* 추상화입니다. 요청 데이터의 유효성을 검사하고 반환할 뷰(또는 API의 결과)를 선택하는 책임이 있습니다. 잘 구성된 애플리케이션에서는 데이터 액세스 또는 비즈니스 로직을 직접 포함하지 않습니다. 대신, 이러한 책임을 처리하는 서비스에 위임합니다.

## 액션 정의하기

컨트롤러의 공개 메서드는 `[NonAction]` 특성이 없는 한 액션입니다. 액션의 매개변수는 요청 데이터에 바인딩되고 [모델 바인딩](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-8.0)을 사용하여 유효성을 검사합니다. 모델 바인딩이 된 모든 항목에 대해 모델 유효성 검사가 수행됩니다. `ModelState.IsValid` 속성 값은 모델 바인딩 및 유효성 검사가 성공했는지 여부를 나타냅니다.

액션 메서드는 요청을 비즈니스 문제에 매핑하는 논리를 포함해야 합니다. 비즈니스 문제는 일반적으로 컨트롤러가 [종속성 주입](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/dependency-injection?view=aspnetcore-8.0)을 통해 액세스하는 서비스로 표현되어야 합니다. 그런 다음 액션은 비즈니스 액션의 결과를 애플리케이션 상태에 매핑합니다.

액션은 무엇이든 반환할 수 있지만, 일반적으로 응답을 생성하는 `IActionResult`(또는 비동기 메서드의 경우 `Task<IActionResult>`)의 인스턴스를 반환합니다. 액션 메서드는 *어떤 종류의 응답*을 선택하는 책임이 있습니다. 액션 결과는 *응답을 수행*합니다.

### 컨트롤러 헬퍼 메서드

컨트롤러는 일반적으로 <xref:Microsoft.AspNetCore.Mvc.Controller>를 상속받지만, 이는 필수가 아닙니다. `Controller`를 상속받으면 세 가지 카테고리의 헬퍼 메서드에 액세스할 수 있습니다:

#### 1. 빈 응답 본문을 반환하는 메서드

응답 본문에 설명할 내용이 없으므로 `Content-Type` HTTP 응답 헤더가 포함되지 않습니다.

이 카테고리에는 두 가지 결과 유형이 있습니다: 리디렉션과 HTTP 상태 코드.

* **HTTP 상태 코드**

    이 유형은 HTTP 상태 코드를 반환합니다. 이 유형의 몇 가지 헬퍼 메서드는 `BadRequest`, `NotFound`, `Ok`입니다. 예를 들어, `return BadRequest();`는 실행 시 400 상태 코드를 생성합니다. `BadRequest`, `NotFound`, `Ok`와 같은 메서드가 오버로드되면, 콘텐츠 협상이 발생하므로 더 이상 HTTP 상태 코드 응답자로 간주되지 않습니다.

* **리디렉션**

    이 유형은 액션 또는 목적지로 리디렉션을 반환합니다(예: `Redirect`, `LocalRedirect`, `RedirectToAction`, `RedirectToRoute` 사용). 예를 들어, `return RedirectToAction("Complete", new {id = 123});`는 익명 객체를 전달하여 `Complete`로 리디렉션합니다.

    리디렉션 결과 유형은 주로 `Location` HTTP 응답 헤더를 추가하는 점에서 HTTP 상태 코드 유형과 다릅니다.

#### 2. 미리 정의된 콘텐츠 유형으로 비어 있지 않은 응답 본문을 반환하는 메서드

이 카테고리의 대부분의 헬퍼 메서드는 응답 본문을 설명하기 위해 `Content-Type` 응답 헤더를 설정할 수 있는 `ContentType` 속성을 포함합니다.

이 카테고리에는 두 가지 결과 유형이 있습니다: [뷰](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/overview?view=aspnetcore-8.0)와 [형식화된 응답](https://learn.microsoft.com/en-us/aspnet/core/web-api/advanced/formatting?view=aspnetcore-8.0).

* **뷰**

    이 유형은 모델을 사용하여 HTML을 렌더링하는 뷰를 반환합니다. 예를 들어, `return View(customer);`는 모델을 뷰에 전달하여 데이터 바인딩을 수행합니다.

* **형식화된 응답**

    이 유형은 특정 방식으로 객체를 표현하기 위해 JSON 또는 유사한 데이터 교환 형식을 반환합니다. 예를 들어, `return Json(customer);`는 제공된 객체를 JSON 형식으로 직렬화합니다.

    이 유형의 다른 일반적인 메서드로는 `File`과 `PhysicalFile`이 있습니다. 예를 들어, `return PhysicalFile(customerFilePath, "text/xml");`은 `PhysicalFileResult`를 반환합니다.

#### 3. 클라이언트와 협상된 콘텐츠 유형으로 비어 있지 않은 응답 본문을 반환하는 메서드

이 카테고리는 **콘텐츠 협상**으로 더 잘 알려져 있습니다. [콘텐츠 협상](https://learn.microsoft.com/en-us/aspnet/core/web-api/advanced/formatting?view=aspnetcore-8.0#content-negotiation)은 액션이 `ObjectResult` 유형 또는 `IActionResult` 구현이 아닌 다른 것을 반환할 때마다 적용됩니다. `IActionResult` 구현이 아닌 것(예: `object`)을 반환하는 액션도 형식화된 응답을 반환합니다.

이 유형의 일부 헬퍼 메서드로는 `BadRequest`, `CreatedAtRoute`, `Ok`가 있습니다. 이러한 메서드의 예로는 각각 `return BadRequest(modelState);`, `return CreatedAtRoute("routename", values, newobject);`, `return Ok(value);`가 있습니다. `BadRequest`와 `Ok`는 값을 전달받을 때만 콘텐츠 협상을 수행하며, 값을 전달받지 않을 경우 HTTP 상태 코드 결과 유형으로 작동합니다. 반면, `CreatedAtRoute` 메서드는 모든 오버로드가 값을 요구하므로 항상 콘텐츠 협상을 수행합니다.

### 횡단 관심사

애플리케이션은 일반적으로 워크플로의 일부를 공유합니다. 예를 들어, 쇼핑 카트에 접근하려면 인증이 필요한 애플리케이션이나 일부 페이지에 데이터를 캐시하는 애플리케이션이 있습니다. 액션 메서드 전에 또는 후에 논리를 수행하려면 *필터*를 사용하십시오. 횡단 관심사에 대해 [필터](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-8.0)를 사용하면 중복을 줄일 수 있습니다.

대부분의 필터 특성은 `[Authorize]`와 같이 원하는 세분성 수준에 따라 컨트롤러 또는 액션 수준에서 적용될 수 있습니다.

오류 처리 및 응답 캐싱은 종종 횡단 관심사입니다:
* [오류 처리](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-8.0#exception-filters)
* [응답 캐싱](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/response?view=aspnetcore-8.0)

많은 횡단 관심사는 필터 또는 사용자 정의 [미들웨어](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0)를 사용하여 처리할 수 있습니다.

---
## 출처
[Handle requests with controllers in ASP.NET Core MVC](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/actions?view=aspnetcore-8.0)

---
## [다음](./05_Routing.md)
