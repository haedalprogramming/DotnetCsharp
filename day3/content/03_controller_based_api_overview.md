#  Controller Based APIs overview

## 목차
- [Controller Based APIs overview](#controller-based-apis-overview)
  - [목차](#목차)
  - [ControllerBase 클래스](#controllerbase-클래스)
  - [특성](#특성)
  - [ApiController 특성](#apicontroller-특성)
    - [특정 컨트롤러에 특성 적용](#특정-컨트롤러에-특성-적용)
    - [여러 컨트롤러에 특성 적용](#여러-컨트롤러에-특성-적용)
    - [어셈블리에 특성 적용](#어셈블리에-특성-적용)
  - [속성 라우팅 요구 사항](#속성-라우팅-요구-사항)
  - [자동 HTTP 400 응답](#자동-http-400-응답)
    - [기본 BadRequest 응답](#기본-badrequest-응답)
    - [자동 400 응답 기록](#자동-400-응답-기록)
    - [자동 400 응답 비활성화](#자동-400-응답-비활성화)
  - [바인딩 소스 매개 변수 추론](#바인딩-소스-매개-변수-추론)
    - [FromBody 추론 참고 사항](#frombody-추론-참고-사항)
    - [FromServices 추론 참고 사항](#fromservices-추론-참고-사항)
    - [추론 규칙 비활성화](#추론-규칙-비활성화)
  - [Multipart/form-data 요청 추론](#multipartform-data-요청-추론)
  - [오류 상태 코드에 대한 문제 세부 정보](#오류-상태-코드에-대한-문제-세부-정보)
    - [ProblemDetails 응답 비활성화](#problemdetails-응답-비활성화)
  - [\[Consumes\] 특성으로 지원되는 요청 콘텐츠 유형 정의](#consumes-특성으로-지원되는-요청-콘텐츠-유형-정의)
  - [출처](#출처)
  - [다음](#다음)

---

ASP.NET Core는 컨트롤러 또는 최소 API를 사용하여 웹 API를 생성하는 것을 지원합니다. 웹 API의 *컨트롤러*는 `ControllerBase`에서 파생된 클래스입니다. 컨트롤러는 요청당 한 번씩 활성화되고 삭제됩니다.

이 문서에서는 웹 API 요청을 처리하기 위해 컨트롤러를 사용하는 방법을 설명합니다.

## ControllerBase 클래스

컨트롤러 기반 웹 API는 `ControllerBase`에서 파생된 하나 이상의 컨트롤러 클래스로 구성됩니다. 웹 API 프로젝트 템플릿은 시작 컨트롤러를 제공합니다:

```C#
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
```

웹 API 컨트롤러는 일반적으로 `Controller` 대신 `ControllerBase`에서 파생되어야 합니다. `Controller`는 `ControllerBase` 에서 파생되며 뷰를 지원하므로 웹 페이지를 처리하는 데 사용되며, 웹 API 요청을 처리하는 데는 적합하지 않습니다. 동일한 컨트롤러가 뷰와 웹 API를 모두 지원해야 하는 경우에는 `Controller`에서 파생됩니다.

`ControllerBase` 클래스는 HTTP 요청을 처리하는 데 유용한 많은 속성과 메서드를 제공합니다. 예를 들어, `CreatedAtAction` 은 201 상태 코드를 반환합니다:

```C#
[HttpPost]
[ProducesResponseType(StatusCodes.Status201Created)]
[ProducesResponseType(StatusCodes.Status400BadRequest)]
public ActionResult<Pet> Create(Pet pet)
{
    pet.Id = _petsInMemoryStore.Any() ? 
             _petsInMemoryStore.Max(p => p.Id) + 1 : 1;
    _petsInMemoryStore.Add(pet);

    return CreatedAtAction(nameof(GetById), new { id = pet.Id }, pet);
}
```

다음 표에는 `ControllerBase`의 메서드 예제가 포함되어 있습니다.

|메서드   |설명    |
|---------|---------|
|BadRequest| 400 상태 코드를 반환합니다.|
|NotFound| 404 상태 코드를 반환합니다.|
|PhysicalFile| 파일을 반환합니다.|
|TryUpdateModelAsync| [모델 바인딩]을 호출합니다.|
|TryValidateModel| [모델 유효성 검사]를 호출합니다.|

사용 가능한 모든 메서드와 속성의 목록은 [<xref:Microsoft.AspNetCore.Mvc.ControllerBase>](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase)를 참조하십시오.

## 특성

`Microsoft.AspNetCore.Mvc` 네임스페이스는 웹 API 컨트롤러와 액션 메서드의 동작을 구성하는 데 사용할 수 있는 특성을 제공합니다. 다음 예제는 지원되는 HTTP 액션 동사와 반환될 수 있는 모든 알려진 HTTP 상태 코드를 지정하기 위해 특성을 사용하는 방법을 보여줍니다:

```C#
[HttpPost]
[ProducesResponseType(StatusCodes.Status201Created)]
[ProducesResponseType(StatusCodes.Status400BadRequest)]
public ActionResult<Pet> Create(Pet pet)
{
    pet.Id = _petsInMemoryStore.Any() ? 
             _petsInMemoryStore.Max(p => p.Id) + 1 : 1;
    _petsInMemoryStore.Add(pet);

    return CreatedAtAction(nameof(GetById), new { id = pet.Id }, pet);
}
```

다음은 사용할 수 있는 특성의 몇 가지 더 많은 예입니다.

| 특성 | 설명 |
|--|--|
| `[Route]` | 컨트롤러나 액션의 URL 패턴을 지정합니다. |
| `[Bind]` | 모델 바인딩을 위해 포함할 접두사와 속성을 지정합니다. |
| `[HttpGet]` | HTTP GET 액션 동사를 지원하는 액션을 식별합니다. |
| `[Consumes]` | 액션이 수락하는 데이터 유형을 지정합니다. |
| `[Produces]` | 액션이 반환하는 데이터 유형을 지정합니다. |

사용 가능한 특성을 포함한 목록은 [<xref:Microsoft.AspNetCore.Mvc>](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc) 네임스페이스를 참조하십시오.

## ApiController 특성

[`[ApiController]`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) 특성은 다음과 같은 의견이 반영된 API 전용 동작을 활성화하기 위해 컨트롤러 클래스에 적용될 수 있습니다:

* [속성 라우팅 요구 사항]
* [Multipart/form-data 요청 추론]
* [오류 상태 코드에 대한 문제 세부 정보]

### 특정 컨트롤러에 특성 적용

다음 예제에서처럼 프로젝트 템플릿의 `[ApiController]` 특성은 특정 컨트롤러에 적용될 수 있습니다:

```C#
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
```

### 여러 컨트롤러에 특성 적용

여러 컨트롤러에 특성을 적용하는 한 가지 방법은 [`[ApiController]`](<xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute>) 특성으로 주석이 달린 사용자 지정 기본 컨트롤러 클래스를 만드는 것입니다. 다음 예제는 사용자 지정 기본 클래스와 이를 상속하는 컨트롤러를 보여줍니다:

```C#
[ApiController]
public class MyControllerBase : ControllerBase
{
}
```

```C#
[Produces(MediaTypeNames.Application.Json)]
[Route("[controller]")]
public class PetsController : MyControllerBase
```

### 어셈블리에 특성 적용

`[ApiController]` 특성은 어셈블리에 적용될 수 있습니다. `[ApiController]` 특성이 어셈블리에 적용되면 어셈블리의 모든 컨트롤러에 `[ApiController]` 특성이 적용됩니다. 개별 컨트롤러에 대해서는 선택 해제할 수 없습니다. 어셈블리 수준의 특성을 `Program.cs` 파일에 적용합니다:

```C#
using Microsoft.AspNetCore.Mvc;
[assembly: ApiController]

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

## 속성 라우팅 요구 사항

`[ApiController]` 특성은 속성 라우팅을 요구합니다. 예를 들어:

```C#
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
```

액션은 [전통적인 라우팅]에 따라 `UseEndpoints`, `UseMvc`, 또는 `UseMvcWithDefaultRoute`에 의해 정의된 경로를 통해 접근할 수 없습니다.

## 자동 HTTP 400 응답

`[ApiController]` 특성은 모델 유효성 검사 오류가 자동으로 HTTP 400 응답을 트리거하도록 합니다. 따라서 다음 코드는 액션 메서드에서 불필요합니다:

```csharp
if (!ModelState.IsValid)
{
    return BadRequest(ModelState);
}
```

ASP.NET Core MVC는 `ModelStateInvalidFilter` 액션 필터를 사용하여 위의 검사를 수행합니다.

### 기본 BadRequest 응답

HTTP 400 응답의 기본 응답 유형은 `ValidationProblemDetails`입니다. 다음 응답 본문은 직렬화된 유형의 예입니다:

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "One or more validation errors occurred.",
  "status": 400,
  "traceId": "|7fb5e16a-4c8f23bbfc974667.",
  "errors": {
    "": [
      "A non-empty request body is required."
    ]
  }
}
```

`ValidationProblemDetails` 유형:

* 웹 API 응답에서 오류를 지정하는 기계 판독 형식을 제공합니다.
* [RFC 7807 사양](https://tools.ietf.org/html/rfc7807)을 준수합니다.

자동 응답과 사용자 정의 응답을 일관되게 만들려면 `BadRequest` 대신 `ValidationProblem` 메서드를 호출하십시오. `ValidationProblem`은 자동 응답과 마찬가지로 `ValidationProblemDetails` 객체를 반환합니다.

### 자동 400 응답 기록

자동 400 응답을 기록하려면 `InvalidModelStateResponseFactory` 대리자 속성을 설정하여 사용자 정의 처리를 수행합니다. 기본적으로 `InvalidModelStateResponseFactory`는 `ProblemDetailsFactory`를 사용하여 `ValidationProblemDetails`의 인스턴스를 생성합니다.

다음 예제는 자동 400 응답에 대한 정보를 기록하기 위해 `ILogger<TCategoryName>` 인스턴스를 검색하는 방법을 보여줍니다:

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(options =>
    {
      // To preserve the default behavior, capture the original delegate to call later.
        var builtInFactory = options.InvalidModelStateResponseFactory;

        options.InvalidModelStateResponseFactory = context =>
        {
            var logger = context.HttpContext.RequestServices
                                .GetRequiredService<ILogger<Program>>();

            // Perform logging here.
            // ...

            // Invoke the default behavior, which produces a ValidationProblemDetails
            // response.
            // To produce a custom response, return a different implementation of 
            // IActionResult instead.
            return builtInFactory(context);
        };
    });

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

### 자동 400 응답 비활성화

자동 400 동작을 비활성화하려면 `SuppressModelStateInvalidFilter` 속성을 `true`로 설정하십시오. 다음 강조 표시된 코드를 추가합니다:

```C#
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(options =>
    {
        options.SuppressConsumesConstraintForFormFileParameters = true;
        options.SuppressInferBindingSourcesForParameters = true;
        options.SuppressModelStateInvalidFilter = true;
        options.SuppressMapClientErrors = true;
        options.ClientErrorMapping[StatusCodes.Status404NotFound].Link =
            "https://httpstatuses.com/404";
    });

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

## 바인딩 소스 매개 변수 추론

바인딩 소스 특성은 액션 매개 변수 값이 위치한 위치를 정의합니다. 다음 바인딩 소스 특성이 존재합니다:

|특성|바인딩 소스 |
|---------|---------|
|`[FromBody]`     | 요청 본문 |
|`[FromForm]`     | 요청 본문의 폼 데이터 |
|`[FromHeader]` | 요청 헤더 |
|`[FromQuery]`   | 요청 쿼리 문자열 매개 변수 |
|`[FromRoute]`   | 현재 요청의 경로 데이터 |
|`[FromServices]` | 액션 매개 변수로 주입된 요청 서비스 |
|`[AsParameters]` | 메서드 매개 변수 |

> [!WARNING]
> 값에 `%2f`(즉 `/`)가 포함될 수 있는 경우 `[FromRoute]`를 사용하지 마십시오. `%2f`는 `/`로 변환되지 않습니다. 값에 `%2f`가 포함될 수 있는 경우 `[FromQuery]`를 사용하십시오.

`[ApiController]` 특성 또는 `[FromQuery]`와 같은 바인딩 소스 특성이 없으면 ASP.NET Core 런타임은 복합 객체 모델 바인더를 사용하려고 시도합니다. 복합 객체 모델 바인더는 정의된 순서로 값 공급자로부터 데이터를 가져옵니다.

다음 예제에서 `[FromQuery]` 특성은 `discontinuedOnly` 매개 변수 값이 요청 URL의 쿼리 문자열에 제공됨을 나타냅니다:

```C#
[HttpGet]
public ActionResult<List<Product>> Get(
    [FromQuery] bool discontinuedOnly = false)
{
    List<Product> products = null;

    if (discontinuedOnly)
    {
        products = _productsInMemoryStore.Where(p => p.IsDiscontinued).ToList();
    }
    else
    {
        products = _productsInMemoryStore;
    }

    return products;
}
```

`[ApiController]` 특성은 액션 매개 변수의 기본 데이터 소스에 대한 추론 규칙을 적용합니다. 이러한 규칙은 액션 매개 변수에 특성을 적용하여 바인딩 소스를 수동으로 식별하는 번거로움을 덜어줍니다. 바인딩 소스 추론 규칙은 다음과 같이 동작합니다:

* DI 컨테이너에 등록된 복합 유형 매개 변수에 대해 `[FromServices]`가 추론됩니다.
* DI 컨테이너에 등록되지 않은 복합 유형 매개 변수에 대해 `[FromBody]`가 추론됩니다. `[FromBody]` 추론 규칙의 예외는 `IFormCollection` 및 `CancellationToken`과 같은 특수한 의미를 가진 내장 복합 유형입니다. 바인딩 소스 추론 코드는 이러한 특수 유형을 무시합니다.
* 액션 매개 변수 유형이 `IFormFile` 및 `IFormFileCollection` 인 경우 `[FromForm]`이 추론됩니다. 간단한 유형이나 사용자 정의 유형에 대해서는 추론되지 않습니다.
* 경로 템플릿의 매개 변수와 일치하는 액션 매개 변수 이름에 대해 `[FromRoute]`가 추론됩니다. 하나 이상의 경로가 액션 매개 변수와 일치하는 경우 모든 경로 값이 `[FromRoute]`로 간주됩니다.
* 다른 모든 액션 매개 변수에 대해 `[FromQuery]`가 추론됩니다.

### FromBody 추론 참고 사항

`[FromBody]`는 `string` 또는 `int`와 같은 간단한 유형에 대해 추론되지 않습니다. 따라서 해당 기능이 필요한 경우 간단한 유형에 대해 `[FromBody]` 특성을 사용해야 합니다.

액션에 요청 본문에서 바인딩된 매개 변수가 둘 이상인 경우 예외가 발생합니다. 예를 들어, 다음과 같은 모든 액션 메서드 시그니처는 예외를 발생시킵니다:

* 둘 다 복합 유형이므로 `[FromBody]`가 추론됩니다.

  ```csharp
  [HttpPost]
  public IActionResult Action1(Product product, Order order)
  ```

* 하나에 대해 `[FromBody]` 특성이 적용되고, 다른 하나는 복합 유형이므로 추론됩니다.

  ```csharp
  [HttpPost]
  public IActionResult Action2(Product product, [FromBody] Order order)
  ```

* 둘 다 `[FromBody]` 특성이 적용됩니다.

  ```csharp
  [HttpPost]
  public IActionResult Action3([FromBody] Product product, [FromBody] Order order)
  ```

<a name="FSI7"></a>

### FromServices 추론 참고 사항

매개 변수 바인딩은 [종속성 주입](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 통해 서비스로 구성된 유형의 매개 변수를 바인딩합니다. 이는 매개 변수에 [`[FromServices]`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.fromservicesattribute) 특성을 명시적으로 적용할 필요가 없음을 의미합니다. 다음 코드에서 두 액션은 시간을 반환합니다:

```C#
[Route("[controller]")]
[ApiController]
public class MyController : ControllerBase
{
    public ActionResult GetWithAttribute([FromServices] IDateTime dateTime) 
                                                        => Ok(dateTime.Now);

    [Route("noAttribute")]
    public ActionResult Get(IDateTime dateTime) => Ok(dateTime.Now);
}
```

드물게 자동 DI는 DI에 있는 유형을 API 컨트롤러의 액션 메서드에서 인수로 받아들이는 앱을 중단시킬 수 있습니다. DI에 유형이 있고 API 컨트롤러 액션의 인수로 있는 것은 일반적이지 않습니다.

단일 액션 매개 변수에 대해 `[FromServices]` 추론을 비활성화하려면 매개 변수에 원하는 바인딩 소스 특성을 적용하십시오. 예를 들어, 요청 본문에서 바인딩된 액션 매개 변수에 `[FromBody]` 특성을 적용하십시오.

글로벌하게 `[FromServices]` 추론을 비활성화하려면 [DisableImplicitFromServicesParameters](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.disableimplicitfromservicesparameters)를 `true`로 설정하십시오:

```C#
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddSingleton<IDateTime, SystemDateTime>();

builder.Services.Configure<ApiBehaviorOptions>(options =>
{
    options.DisableImplicitFromServicesParameters = true;
});

var app = builder.Build();

app.MapControllers();

app.Run();
```

API 컨트롤러 액션의 인수가 DI에서 가져오는지 다른 소스에서 가져오는지는 앱 시작 시 `IServiceProviderIsService`로 확인됩니다.

API 컨트롤러 액션 매개 변수의 바인딩 소스를 추론하는 메커니즘은 다음 규칙을 사용합니다:

* 이전에 지정된 `BindingInfo.BindingSource`는 절대 덮어쓰지 않습니다.
* DI 컨테이너에 등록된 복합 유형 매개 변수는 `BindingSource.Services`로 할당됩니다.
* DI 컨테이너에 등록되지 않은 복합 유형 매개 변수는 `BindingSource.Body`로 할당됩니다.
* 경로 템플릿에 나타나는 이름이 있는 매개 변수는 `BindingSource.Path`로 할당됩니다.
* 나머지 모든 매개 변수는 `BindingSource.Query`로 할당됩니다.

### 추론 규칙 비활성화

바인딩 소스 추론을 비활성화하려면 `SuppressInferBindingSourcesForParameters` 를 `true`로 설정하십시오:

```C#
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(options =>
    {
        options.SuppressConsumesConstraintForFormFileParameters = true;
        options.SuppressInferBindingSourcesForParameters = true;
        options.SuppressModelStateInvalidFilter = true;
        options.SuppressMapClientErrors = true;
        options.ClientErrorMapping[StatusCodes.Status404NotFound].Link =
            "https://httpstatuses.com/404";
        options.DisableImplicitFromServicesParameters = true;
    });

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

## Multipart/form-data 요청 추론

`[ApiController]` 특성은 `IFormFile` 및 `IFormFileCollection` 유형의 액션 매개 변수에 대한 추론 규칙을 적용합니다. 이러한 유형에 대해 `multipart/form-data` 요청 콘텐츠 유형이 추론됩니다.

기본 동작을 비활성화하려면 `SuppressConsumesConstraintForFormFileParameters` 속성을 `true`로 설정하십시오:

```C#
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(options =>
    {
        options.SuppressConsumesConstraintForFormFileParameters = true;
        options.SuppressInferBindingSourcesForParameters = true;
        options.SuppressModelStateInvalidFilter = true;
        options.SuppressMapClientErrors = true;
        options.ClientErrorMapping[StatusCodes.Status404NotFound].Link =
            "https://httpstatuses.com/404";
    });

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

## 오류 상태 코드에 대한 문제 세부 정보

MVC는 오류 결과(400 이상의 상태 코드를 가진 결과)를 `ProblemDetails`가 있는 결과로 변환합니다. `ProblemDetails` 유형은 HTTP 응답에서 기계 판독 가능한 오류 세부 정보를 제공하기 위한 [RFC 7807 사양](https://tools.ietf.org/html/rfc7807)을 기반으로 합니다.

다음 코드를 컨트롤러 액션에 고려하십시오:

```C#
{
  type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
  title: "Not Found",
  status: 404,
  traceId: "0HLHLV31KRN83:00000001"
}
```

`NotFound` 메서드는 `ProblemDetails` 본문과 함께 HTTP 404 상태 코드를 생성합니다. 예를 들어:

```json
{
  type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
  title: "Not Found",
  status: 404,
  traceId: "0HLHLV31KRN83:00000001"
}
```

### ProblemDetails 응답 비활성화

오류 상태 코드에 대한 `ProblemDetails`의 자동 생성을 비활성화하려면 `SuppressMapClientErrors` 속성을 `true`로 설정합니다. 다음 코드를 추가하십시오:

```C#
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(options =>
    {
        options.SuppressConsumesConstraintForFormFileParameters = true;
        options.SuppressInferBindingSourcesForParameters = true;
        options.SuppressModelStateInvalidFilter = true;
        options.SuppressMapClientErrors = true;
        options.ClientErrorMapping[StatusCodes.Status404NotFound].Link =
            "https://httpstatuses.com/404";
    });

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

<a name="consumes"></a>

## [Consumes] 특성으로 지원되는 요청 콘텐츠 유형 정의

기본적으로 액션은 모든 사용 가능한 요청 콘텐츠 유형을 지원합니다. 예를 들어, 앱이 JSON 및 XML [입력 포매터](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-8.0#input-formatters)를 모두 지원하도록 구성된 경우, 액션은 `application/json` 및 `application/xml`을 포함한 여러 콘텐츠 유형을 지원합니다.

[[Consumes]](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.consumesattribute) 특성은 액션이 지원하는 요청 콘텐츠 유형을 제한할 수 있습니다. 액션이나 컨트롤러에 `[Consumes]` 특성을 적용하여 하나 이상의 콘텐츠 유형을 지정합니다:

```csharp
[HttpPost]
[Consumes("application/xml")]
public IActionResult CreateProduct(Product product)
```

위의 코드에서 `CreateProduct` 액션은 콘텐츠 유형 `application/xml`을 지정합니다. 이 액션으로 라우팅되는 요청은 `application/xml`의 `Content-Type` 헤더를 지정해야 합니다. `application/xml`의 `Content-Type` 헤더를 지정하지 않은 요청은 [415 Unsupported Media Type](https://developer.mozilla.org/docs/Web/HTTP/Status/415) 응답을 반환합니다.

`[Consumes]` 특성은 또한 유형 제약을 적용하여 액션이 들어오는 요청의 콘텐츠 유형에 따라 선택에 영향을 미칠 수 있습니다. 다음 예제를 고려하십시오:

```C#
[ApiController]
[Route("api/[controller]")]
public class ConsumesController : ControllerBase
{
    [HttpPost]
    [Consumes("application/json")]
    public IActionResult PostJson(IEnumerable<int> values) =>
        Ok(new { Consumes = "application/json", Values = values });

    [HttpPost]
    [Consumes("application/x-www-form-urlencoded")]
    public IActionResult PostForm([FromForm] IEnumerable<int> values) =>
        Ok(new { Consumes = "application/x-www-form-urlencoded", Values = values });
}
```

위의 코드에서 `ConsumesController`는 `https://localhost:5001/api/Consumes` URL로 전송된 요청을 처리하도록 구성됩니다. 컨트롤러의 `PostJson` 및 `PostForm` 액션은 동일한 URL로 POST 요청을 처리합니다. 유형 제약을 적용하지 않는 `[Consumes]` 특성 없이, 모호한 일치 예외가 발생합니다.

`[Consumes]` 특성은 두 액션 모두에 적용됩니다. `PostJson` 액션은 `Content-Type` 헤더가 `application/json`인 요청을 처리합니다. `PostForm` 액션은 `Content-Type` 헤더가 `application/x-www-form-urlencoded`인 요청을 처리합니다.

---
## 출처
[Controller Based APIs overview](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-8.0)

---
## [다음](./04_Tutorial.md)
