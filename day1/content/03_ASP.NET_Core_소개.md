# ASP.NET Core 소개

## 목차
- [ASP.NET Core 소개](#aspnet-core-소개)
  - [목차](#목차)
  - [ASP.NET Core 개요](#aspnet-core-개요)
    - [ASP.NET Core를 선택해야 하는 이유](#aspnet-core를-선택해야-하는-이유)
    - [ASP.NET Core MVC를 사용하여 웹 API 및 웹 UI 빌드](#aspnet-core-mvc를-사용하여-웹-api-및-웹-ui-빌드)
    - [클라이언트 쪽 개발](#클라이언트-쪽-개발)
    - [ASP.NET Core 대상 프레임워크](#aspnet-core-대상-프레임워크)
    - [권장되는 학습 경로](#권장되는-학습-경로)
  - [출처](#출처)
  - [다음](#다음)

---
## ASP.NET Core 개요

ASP.NET Core는 최신 클라우드 사용 인터넷 연결 앱을 빌드하기 위한 플랫폼 간 고성능 오픈 소스 프레임워크입니다.

ASP.NET Core를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

 - 웹앱 및 서비스, IoT(사물 인터넷) 앱 및 모바일 백 엔드를 빌드할 수 있습니다.
 - Windows, macOS 및 Linux에서 선호하는 개발 도구를 사용할 수 있습니다.
 - 클라우드 또는 온-프레미스에 배포할 수 있습니다.
 - .NET에서 실행합니다.

### ASP.NET Core를 선택해야 하는 이유

수백만 명의 개발자가 ASP.NET 4.x를 사용하여 웹앱을 만들었고 지금도 만들고 있습니다. ASP.NET Core는 더 간결하고 모듈화된 프레임워크를 만드는 아키텍처 변경 내용이 포함된 ASP.NET 4.x의 재설계입니다.

ASP.NET Core는 다음과 같은 이점을 제공합니다.

 - 웹 UI 및 웹 API를 동일한 과정으로 빌드합니다.
 - 테스트 가능성을 고려하여 설계되었습니다.
 - Razor Pages는 더 쉽고 더 생산적으로 코딩 페이지에 초점을 맞춘 시나리오를 만듭니다.
 - Blazor를 사용하면 JavaScript와 함께 브라우저에서 C#을 사용할 수 있습니다. 모두 .NET으로 작성된 서버 쪽 및 클라이언트 쪽 앱을 공유합니다.
 - Windows, macOS 및 Linux에서 개발하고 실행할 수 있습니다.
 - 오픈 소스이며 커뮤니티에 중점을 둡니다.
 - 최신 클라이언트 쪽 프레임워크 및 워크플로 개발을 통합합니다.
 - gRPC를 사용하여 RPC(원격 프로시저 호출) 서비스 호스팅을 지원합니다.
 - 클라우드를 갖춘 환경 기반 구성 시스템입니다.
 - 종속성 주입이 기본 제공됩니다.
 - 간단한 고성능 모듈식 HTTP 요청 파이프라인을 포함합니다.
 - 다음에 호스트하는 기능:
    - Kestrel
    - IIS
    - HTTP.sys
    - Nginx
    - Docker
 - Side-by-side 버전 관리.
 - 최신 웹 개발을 간소화하는 도구를 포함합니다.

### ASP.NET Core MVC를 사용하여 웹 API 및 웹 UI 빌드

ASP.NET Core MVC는 Web API 및 웹앱을 만들기 위한 기능을 제공합니다.

 - MVC(모델-뷰-컨트롤러) 패턴을 통해 웹 API 및 웹앱을 테스트 가능하게 합니다.
 - Razor Pages는 웹 UI를 쉽게 빌드하고 생산성을 높일 수 있는 페이지 기반 프로그래밍 모델입니다.
 - Razor 태그는 Razor Pages 및 MVC 뷰를 위한 생산적인 구문을 제공합니다.
 - 태그 도우미를 사용하면 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 서버 쪽 코드를 사용할 수 있습니다.
 - 다양한 데이터 형식 및 콘텐츠 협상에 대한 기본 제공 지원을 통해 웹 API를 브라우저 및 모바일 디바이스를 포함한 다양한 클라이언트에 연결할 수 있습니다.
 - 모델 바인딩은 HTTP 요청의 데이터를 작업 메서드 매개 변수에 자동으로 매핑합니다.
 - 모델 유효성 검사는 클라이언트 쪽 및 서버 쪽 유효성 검사를 자동으로 수행합니다.

### 클라이언트 쪽 개발

ASP.NET Core는 풍부한 대화형 웹 UI 빌드를 포함 Blazor 하며 Angular, React, Vue 및 부트스트랩과 같은 다른 인기 있는 프런트 엔드 JavaScript 프레임워크와도 통합됩니다. 자세한 내용은 ASP.NET CoreBlazor및 클라이언트 쪽 개발 관련 항목을 참조하세요.

### ASP.NET Core 대상 프레임워크

ASP.NET Core 3.x 이상에서는 .NET만 대상으로 지정할 수 있습니다.

.NET을 대상으로 하는 데는 몇 가지 이점이 있으며, 이러한 장점은 각 릴리스에 따라 증가합니다. .NET Framework보다 .NET의 몇 가지 이점은 다음과 같습니다.

 - 플랫폼 간 사용 가능. Windows, macOS 및 Linux에서 실행됩니다.
 - 성능 향상
 - Side-by-side 버전 관리
 - 새 API
 - 오픈 소스

### 권장되는 학습 경로

ASP.NET Core 앱 개발을 소개하는 자습서는 다음의 순서대로 살펴보는 것이 좋습니다.

1. 개발하거나 유지 관리하려는 앱 형식에 대한 자습서를 살펴보세요.

| 앱 유형         | 시나리오                     | 자습서             |
|--------------|--------------------------|-----------------|
| 웹 앱          | 새로운 서버 쪽 웹 UI 개발         | [Razor Pages 시작](https://learn.microsoft.com/ko-kr/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-8.0)  |
| 웹 앱          | MVC 앱 유지 관리              | [MVC 시작](https://learn.microsoft.com/ko-kr/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-8.0)          |
| 웹 앱          | 클라이언트 쪽 웹 UI 개발          | [Blazor 시작하기](https://dotnet.microsoft.com/learn/aspnet/blazor-tutorial/intro)     |
| 웹 API        | RESTful HTTP 서비스         | [Web API 만들기](https://learn.microsoft.com/ko-kr/aspnet/core/tutorials/first-web-api?view=aspnetcore-8.0)    |
| 원격 프로시저 호출 앱 | 프로토콜 버퍼를 사용하는 계약 중심 서비스  | [gRPC 서비스 시작](https://learn.microsoft.com/ko-kr/aspnet/core/tutorials/grpc/grpc-start?view=aspnetcore-8.0)     |
| 실시간 앱        | 서버 및 연결된 클라이언트 간의 양방향 통신 | [SignalR 시작하기](https://learn.microsoft.com/ko-kr/aspnet/core/tutorials/signalr?view=aspnetcore-8.0)    |


2. 기본 데이터 액세스를 수행하는 방법을 보여 주는 자습서를 살펴보세요.

| 시나리오        | 자습서                                     |
|-------------|-----------------------------------------|
| 새로운 개발      | [Entity Framework Core를 사용한 Razor Pages](https://learn.microsoft.com/ko-kr/aspnet/core/data/ef-rp/intro?view=aspnetcore-8.0)  |
| MVC 앱 유지 관리 | [Entity Framework Core를 사용한 MVC](https://learn.microsoft.com/ko-kr/aspnet/core/data/ef-mvc/intro?view=aspnetcore-8.0)          |

3. 모든 앱 형식에 적용되는 ASP.NET Core [기본 사항](https://learn.microsoft.com/ko-kr/aspnet/core/fundamentals/?view=aspnetcore-8.0)의 개요를 참고하세요.

4. 관심 있는 다른 항목은 목차를 찾아보세요.

†[대화형 Web API 자습서](https://learn.microsoft.com/ko-kr/training/modules/build-web-api-net-core)도 있습니다. 개발 도구를 로컬에 설치할 필요가 없습니다. 해당 코드는 브라우저로 Azure Cloud Shell에서 실행되고, 테스트에는 curl이 사용됩니다.



---
## 출처
 - [ASP.NET Core docs>개요>ASP.NET Core 개요](https://learn.microsoft.com/ko-kr/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-8.0)

---
## [다음](./04_CSharp_기초.md)



