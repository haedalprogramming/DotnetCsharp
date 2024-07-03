# Minimal APIs overview

## 목차
- [Minimal APIs overview](#minimal-apis-overview)
  - [목차](#목차)
  - [출처](#출처)
  - [다음](#다음)

---

최소 API는 ASP.NET Core를 사용하여 빠른 HTTP API를 구축하기 위한 간소화된 접근 방식입니다.
최소한의 코드와 구성으로 완전한 기능을 갖춘 REST 엔드포인트를 구축할 수 있습니다. 전통적인 스캐폴딩을 건너뛰고 불필요한 컨트롤러를 피하며, API 경로와 동작을 유연하게 선언할 수 있습니다. 예를 들어, 다음 코드는 웹 앱의 루트에 API를 생성하여 `"Hello World!"` 텍스트를 반환합니다.

```csharp
var app = WebApplication.Create(args);

app.MapGet("/", () => "Hello World!");

app.Run();
```

대부분의 API는 경로의 일부로 매개변수를 수락합니다.

```csharp 
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.MapGet("/users/{userId}/books/{bookId}", 
    (int userId, int bookId) => $"The user id is {userId} and book id is {bookId}");

app.Run();
```

이것이 시작하는 데 필요한 전부이지만, 제공되는 모든 것은 아닙니다. 최소 API는 여러 API로 확장하고, 복잡한 경로를 처리하고, 권한 부여 규칙을 적용하며, API 응답의 내용을 제어하는 데 필요한 구성 및 맞춤화를 지원합니다.

---
## 출처
[Minimal APIs overview](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis/overview?view=aspnetcore-8.0)

---
## [다음](./02_Tutorial.md)
