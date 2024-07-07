# Turn Map methods into request delegates with the ASP.NET Core Request Delegate Generator

## 목차
- [Turn Map methods into request delegates with the ASP.NET Core Request Delegate Generator](#turn-map-methods-into-request-delegates-with-the-aspnet-core-request-delegate-generator)
  - [목차](#목차)
  - [지원되지 않는 RDG 시나리오에 대한 진단](#지원되지-않는-rdg-시나리오에-대한-진단)
  - [출처](#출처)
  - [다음](#다음)

---

ASP.NET Core 요청 대리자 생성기(RDG)는 최소 API에 제공된 라우트 핸들러를 ASP.NET Core의 라우팅 인프라에서 처리할 수 있는 요청 대리자로 컴파일하는 컴파일 타임 소스 생성기입니다. RDG는 AoT가 활성화된 상태로 애플리케이션이 게시되거나 [트리밍이 활성화된 경우](https://learn.microsoft.com/en-us/dotnet/core/deploying/trimming/trimming-options#enable-trimming) 암묵적으로 활성화됩니다. RDG는 트림 및 네이티브 AoT 친화적인 코드를 생성합니다.

> [!NOTE]
> * Native AOT 기능은 현재 미리 보기 상태입니다.
> * .NET 8에서는 모든 ASP.NET Core 기능이 Native AOT와 호환되지 않습니다.

RDG는:

* [소스 생성기](https://learn.microsoft.com/en-us/dotnet/csharp/roslyn-sdk/source-generators-overview)입니다.
* 각 `Map` 메서드를 특정 라우트와 연결된 [RequestDelegate](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.requestdelegate)로 변환합니다. `Map` 메서드에는 `EndpointRouteBuilderExtensions`의 `MapGet`, `MapPost`, `MapPatch`, `MapPut`, `MapDelete`와 같은 메서드가 포함됩니다.

Native AOT가 ***활성화되지 않은*** 상태에서 게시할 때:

* 특정 라우트와 관련된 `Map` 메서드는 앱이 시작될 때, 빌드 시가 아닌 메모리에서 요청 대리자로 컴파일됩니다.
* 요청 대리자는 런타임에 생성됩니다.

Native AOT가 활성화된 상태에서 게시할 때:

* 특정 라우트와 관련된 `Map` 메서드는 앱이 빌드될 때 컴파일됩니다. RDG는 라우트에 대한 요청 대리자를 생성하며, 요청 대리자는 앱의 네이티브 이미지로 컴파일됩니다.
* 런타임에 요청 대리자를 생성할 필요를 제거합니다.
* 다음을 보장합니다:
  * 앱의 API에서 사용되는 타입이 네이티브 AOT 도구 체인에 의해 정적으로 분석될 수 있는 방식으로 앱 코드에 루트됩니다.
  * 필요한 코드가 트림되지 않습니다.

RDG는:

* Native AOT가 활성화된 상태로 게시할 때 또는 트리밍이 활성화된 상태로 게시할 때 프로젝트에서 자동으로 활성화됩니다.
* `<EnableRequestDelegateGenerator>true</EnableRequestDelegateGenerator>`를 프로젝트 파일에 설정하여 Native AOT를 사용하지 않을 때에도 수동으로 활성화할 수 있습니다:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <EnableRequestDelegateGenerator>true</EnableRequestDelegateGenerator>
  </PropertyGroup>
    
</Project>
```

RDG를 수동으로 활성화하는 것은 다음과 같은 경우 유용할 수 있습니다:

* 프로젝트의 Native AOT 호환성을 평가할 때.
* 요청 대리자를 미리 생성하여 앱의 시작 시간을 줄일 때.

최소 API는 System.Text.Json을 사용하는 데 최적화되어 있으며, 이는 [System.Text.Json 소스 생성기](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/source-generation)를 사용해야 합니다. 최소 API의 요청 대리자에 매개변수로 전달되거나 반환되는 모든 타입은 ASP.NET Core의 종속성 주입을 통해 등록된 `JsonSerializerContext`에서 구성되어야 합니다:

```C#
using System.Text.Json.Serialization;

var builder = WebApplication.CreateSlimBuilder(args);

builder.Services.ConfigureHttpJsonOptions(options =>
{
    options.SerializerOptions.TypeInfoResolverChain.Insert(
                         0, AppJsonSerializerContext.Default);
});

var app = builder.Build();

var sampleTodos = new Todo[] {
    new(1, "Walk the dog"),
    new(2, "Do the dishes", DateOnly.FromDateTime(DateTime.Now)),
    new(3, "Do the laundry", DateOnly.FromDateTime(DateTime.Now.AddDays(1))),
    new(4, "Clean the bathroom"),
    new(5, "Clean the car", DateOnly.FromDateTime(DateTime.Now.AddDays(2)))
};

var todosApi = app.MapGroup("/todos");
todosApi.MapGet("/", () => sampleTodos);
todosApi.MapGet("/{id}", (int id) =>
    sampleTodos.FirstOrDefault(a => a.Id == id) is { } todo
        ? Results.Ok(todo)
        : Results.NotFound());

app.Run();

public record Todo(int Id, string? Title, DateOnly? DueBy = null, bool IsComplete = false);

[JsonSerializable(typeof(Todo[]))]
internal partial class AppJsonSerializerContext : JsonSerializerContext
{

}
```

## 지원되지 않는 RDG 시나리오에 대한 진단

앱이 빌드될 때, RDG는 Native AOT에서 지원되지 않는 시나리오에 대한 진단을 경고로 내보냅니다. 이러한 진단은 앱 빌드를 방해하지 않습니다. 진단 목록은 [ASP.NET Core 요청 대리자 생성기 진단](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/aot/request-delegate-generator/rdg-ids?view=aspnetcore-8.0)을 참조하세요.

---
## 출처
[Turn Map methods into request delegates with the ASP.NET Core Request Delegate Generator](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/aot/request-delegate-generator/rdg?view=aspnetcore-8.0)

---
## [다음](./07_Middleware_overview.md)
