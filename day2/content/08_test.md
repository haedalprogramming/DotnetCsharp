# Unit test controller logic in ASP.NET Core

## 목차
- [Unit test controller logic in ASP.NET Core](#unit-test-controller-logic-in-aspnet-core)
  - [목차](#목차)
  - [컨트롤러 단위 테스트](#컨트롤러-단위-테스트)
  - [Test ActionResult\<T\>](#test-actionresultt)
  - [추가 자료](#추가-자료)
  - [출처](#출처)
  - [다음](#다음)

---
[단위 테스트](https://learn.microsoft.com/en-us/dotnet/articles/core/testing/unit-testing-with-dotnet-test)는 인프라 및 종속성에서 분리된 앱의 일부를 테스트하는 것을 포함합니다. 컨트롤러 로직을 단위 테스트할 때는 단일 액션의 내용만 테스트하며, 종속성이나 프레임워크 자체의 동작은 테스트하지 않습니다.

## 컨트롤러 단위 테스트

컨트롤러 동작에 집중하기 위해 컨트롤러 액션의 단위 테스트를 설정합니다. 컨트롤러 단위 테스트는 [필터](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-8.0), [라우팅](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-8.0), [모델 바인딩](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-8.0)과 같은 시나리오를 피합니다. 요청에 응답하는 구성 요소 간의 상호 작용을 다루는 테스트는 *통합 테스트*에 의해 처리됩니다. 통합 테스트에 대한 자세한 내용은 [Integration tests in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-8.0)를 참조하십시오.

맞춤 필터와 라우트를 작성하는 경우, 특정 컨트롤러 액션의 테스트의 일부가 아닌 별도의 테스트에서 단위 테스트하십시오.

컨트롤러 단위 테스트를 시연하기 위해 샘플 앱의 다음 컨트롤러를 검토합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/mvc/controllers/testing/samples/) ([다운로드 방법](https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-8.0#how-to-download-a-sample))

Home 컨트롤러는 브레인스토밍 세션 목록을 표시하고 POST 요청으로 새로운 브레인스토밍 세션을 생성할 수 있습니다:

```C#
public class HomeController : Controller
{
    private readonly IBrainstormSessionRepository _sessionRepository;

    public HomeController(IBrainstormSessionRepository sessionRepository)
    {
        _sessionRepository = sessionRepository;
    }

    public async Task<IActionResult> Index()
    {
        var sessionList = await _sessionRepository.ListAsync();

        var model = sessionList.Select(session => new StormSessionViewModel()
        {
            Id = session.Id,
            DateCreated = session.DateCreated,
            Name = session.Name,
            IdeaCount = session.Ideas.Count
        });

        return View(model);
    }

    public class NewSessionModel
    {
        [Required]
        public string SessionName { get; set; }
    }

    [HttpPost]
    public async Task<IActionResult> Index(NewSessionModel model)
    {
        if (!ModelState.IsValid)
        {
            return BadRequest(ModelState);
        }
        else
        {
            await _sessionRepository.AddAsync(new BrainstormSession()
            {
                DateCreated = DateTimeOffset.Now,
                Name = model.SessionName
            });
        }

        return RedirectToAction(actionName: nameof(Index));
    }
}
```

앞서의 컨트롤러는:

* [명시적 종속성 원칙](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/architectural-principles#explicit-dependencies)을 따릅니다.
* [종속성 주입(DI)](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 통해 `IBrainstormSessionRepository` 인스턴스를 제공합니다.
* [Moq](https://www.nuget.org/packages/Moq/)와 같은 모의 객체 프레임워크를 사용하여 모의 `IBrainstormSessionRepository` 서비스를 통해 테스트할 수 있습니다. *모의 객체*는 테스트를 위해 미리 정의된 속성과 메서드 동작을 가진 가상의 객체입니다. 자세한 내용은 [통합 테스트 소개](https://learn.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-8.0#introduction-to-integration-tests)를 참조하십시오.

`HTTP GET Index` 메서드는 반복 또는 분기 없이 단일 메서드만 호출합니다. 이 액션에 대한 단위 테스트는:

* `GetTestSessions` 메서드를 사용하여 `IBrainstormSessionRepository` 서비스를 모의합니다. `GetTestSessions`는 날짜와 세션 이름이 있는 두 개의 모의 브레인스토밍 세션을 생성합니다.
* `Index` 메서드를 실행합니다.
* 메서드가 반환한 결과에 대해 다음을 주장합니다:
  * `ViewResult`가 반환됩니다.
  * [ViewDataDictionary.Model](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary.model)이 `StormSessionViewModel`입니다.
  * `ViewDataDictionary.Model`에 두 개의 브레인스토밍 세션이 저장됩니다.

```C#
[Fact]
public async Task Index_ReturnsAViewResult_WithAListOfBrainstormSessions()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.ListAsync())
        .ReturnsAsync(GetTestSessions());
    var controller = new HomeController(mockRepo.Object);

    // Act
    var result = await controller.Index();

    // Assert
    var viewResult = Assert.IsType<ViewResult>(result);
    var model = Assert.IsAssignableFrom<IEnumerable<StormSessionViewModel>>(
        viewResult.ViewData.Model);
    Assert.Equal(2, model.Count());
}
```

```C#
private List<BrainstormSession> GetTestSessions()
{
    var sessions = new List<BrainstormSession>();
    sessions.Add(new BrainstormSession()
    {
        DateCreated = new DateTime(2016, 7, 2),
        Id = 1,
        Name = "Test One"
    });
    sessions.Add(new BrainstormSession()
    {
        DateCreated = new DateTime(2016, 7, 1),
        Id = 2,
        Name = "Test Two"
    });
    return sessions;
}
```

Home 컨트롤러의 `HTTP POST Index` 메서드 테스트는 다음을 검증합니다:

* [ModelState.IsValid](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary.isvalid)이 `false`인 경우, 액션 메서드는 적절한 데이터를 가진 *400 Bad Request* `ViewResult`를 반환합니다.
* `ModelState.IsValid`이 `true`인 경우:
  * 저장소에서 `Add` 메서드가 호출됩니다.
  * 올바른 인수를 가진 `RedirectToActionResult`가 반환됩니다.

유효하지 않은 모델 상태는 아래 첫 번째 테스트에서 `AddModelError`를 사용하여 오류를 추가하여 테스트합니다:

```C#
[Fact]
public async Task IndexPost_ReturnsBadRequestResult_WhenModelStateIsInvalid()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.ListAsync())
        .ReturnsAsync(GetTestSessions());
    var controller = new HomeController(mockRepo.Object);
    controller.ModelState.AddModelError("SessionName", "Required");
    var newSession = new HomeController.NewSessionModel();

    // Act
    var result = await controller.Index(newSession);

    // Assert
    var badRequestResult = Assert.IsType<BadRequestObjectResult>(result);
    Assert.IsType<SerializableError>(badRequestResult.Value);
}

[Fact]
public async Task IndexPost_ReturnsARedirectAndAddsSession_WhenModelStateIsValid()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.AddAsync(It.IsAny<BrainstormSession>()))
        .Returns(Task.CompletedTask)
        .Verifiable();
    var controller = new HomeController(mockRepo.Object);
    var newSession = new HomeController.NewSessionModel()
    {
        SessionName = "Test Name"
    };

    // Act
    var result = await controller.Index(newSession);

    // Assert
    var redirectToActionResult = Assert.IsType<RedirectToActionResult>(result);
    Assert.Null(redirectToActionResult.ControllerName);
    Assert.Equal("Index", redirectToActionResult.ActionName);
    mockRepo.Verify();
}
```

[ModelState](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary)가 유효하지 않은 경우, GET 요청과 동일한 `ViewResult`가 반환됩니다. 테스트는 유효하지 않은 모델을 전달하려고 시도하지 않습니다. 모델 바인딩이 실행되지 않기 때문에 유효하지 않은 모델을 전달하는 것은 유효한 접근 방식이 아닙니다(통합 테스트에서는 모델 바인딩을 사용하지만). 이 경우, 모델 바인딩은 테스트되지 않습니다. 이 단위 테스트는 액션 메서드의 코드만 테스트합니다.

두 번째 테스트는 `ModelState`가 유효할 때를 검증합니다:

* 새로운 `BrainstormSession`이 추가됩니다(저장소를 통해).
* 메서드는 예상 속성을 가진 `RedirectToActionResult`를 반환합니다.

호출되지 않은 모의 호출은 일반적으로 무시되지만, 설정 호출 끝에서 `Verifiable`을 호출하면 테스트에서 모의 검증을 수행할 수 있습니다. 이는 `mockRepo.Verify` 호출을 통해 수행되며, 예상 메서드가 호출되지 않은 경우 테스트가 실패합니다.

> [!NOTE]
> 이 샘플에서 사용된 Moq 라이브러리는 검증 가능한 모의("엄격한" 모의)와 검증할 수 없는 모의("느슨한" 모의 또는 스텁)을 혼합하여 사용할 수 있게 합니다. [Moq를 사용한 모의 동작 사용자 정의](https://github.com/Moq/moq4/wiki/Quickstart#customizing-mock-behavior)에 대해 자세히 알아보십시오.

샘플 앱의 [SessionController](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/mvc/controllers/testing/samples/3.x/TestingControllersSample/src/TestingControllersSample/Controllers/SessionController.cs)는 특정 브레인스토밍 세션과 관련된 정보를 표시합니다. 컨트롤러에는 유효하지 않은 `id` 값 처리 로직이 포함되어 있습니다(이러한 시나리오를 다루기 위해 두 개의 `return` 시나리오가 있습니다). 최종 `return` 문은 뷰에 새로운 `StormSessionViewModel`을 반환합니다(`Controllers/SessionController.cs`):

```C#
public class SessionController : Controller
{
    private readonly IBrainstormSessionRepository _sessionRepository;

    public SessionController(IBrainstormSessionRepository sessionRepository)
    {
        _sessionRepository = sessionRepository;
    }

    public async Task<IActionResult> Index(int? id)
    {
        if (!id.HasValue)
        {
            return RedirectToAction(actionName: nameof(Index), 
                controllerName: "Home");
        }

        var session = await _sessionRepository.GetByIdAsync(id.Value);
        if (session == null)
        {
            return Content("Session not found.");
        }

        var viewModel = new StormSessionViewModel()
        {
            DateCreated = session.DateCreated,
            Name = session.Name,
            Id = session.Id
        };

        return View(viewModel);
    }
}
```

단위 테스트에는 Session 컨트롤러 `Index` 액션의 각 `return` 시나리오에 대한 테스트가 포함되어 있습니다:

```C#
[Fact]
public async Task IndexReturnsARedirectToIndexHomeWhenIdIsNull()
{
    // Arrange
    var controller = new SessionController(sessionRepository: null);

    // Act
    var result = await controller.Index(id: null);

    // Assert
    var redirectToActionResult = 
        Assert.IsType<RedirectToActionResult>(result);
    Assert.Equal("Home", redirectToActionResult.ControllerName);
    Assert.Equal("Index", redirectToActionResult.ActionName);
}

[Fact]
public async Task IndexReturnsContentWithSessionNotFoundWhenSessionNotFound()
{
    // Arrange
    int testSessionId = 1;
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync((BrainstormSession)null);
    var controller = new SessionController(mockRepo.Object);

    // Act
    var result = await controller.Index(testSessionId);

    // Assert
    var contentResult = Assert.IsType<ContentResult>(result);
    Assert.Equal("Session not found.", contentResult.Content);
}

[Fact]
public async Task IndexReturnsViewResultWithStormSessionViewModel()
{
    // Arrange
    int testSessionId = 1;
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync(GetTestSessions().FirstOrDefault(
            s => s.Id == testSessionId));
    var controller = new SessionController(mockRepo.Object);

    // Act
    var result = await controller.Index(testSessionId);

    // Assert
    var viewResult = Assert.IsType<ViewResult>(result);
    var model = Assert.IsType<StormSessionViewModel>(
        viewResult.ViewData.Model);
    Assert.Equal("Test One", model.Name);
    Assert.Equal(2, model.DateCreated.Day);
    Assert.Equal(testSessionId, model.Id);
}
```

Ideas 컨트롤러로 이동하여, 앱은 `api/ideas` 경로에서 웹 API로 기능을 노출합니다:

* 브레인스토밍 세션과 관련된 아이디어(`IdeaDTO`) 목록이 `ForSession` 메서드에 의해 반환됩니다.
* `Create` 메서드는 세션에 새로운 아이디어를 추가합니다.

```C#
[HttpGet("forsession/{sessionId}")]
public async Task<IActionResult> ForSession(int sessionId)
{
    var session = await _sessionRepository.GetByIdAsync(sessionId);
    if (session == null)
    {
        return NotFound(sessionId);
    }

    var result = session.Ideas.Select(idea => new IdeaDTO()
    {
        Id = idea.Id,
        Name = idea.Name,
        Description = idea.Description,
        DateCreated = idea.DateCreated
    }).ToList();

    return Ok(result);
}

[HttpPost("create")]
public async Task<IActionResult> Create([FromBody]NewIdeaModel model)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    var session = await _sessionRepository.GetByIdAsync(model.SessionId);
    if (session == null)
    {
        return NotFound(model.SessionId);
    }

    var idea = new Idea()
    {
        DateCreated = DateTimeOffset.Now,
        Description = model.Description,
        Name = model.Name
    };
    session.AddIdea(idea);

    await _sessionRepository.UpdateAsync(session);

    return Ok(session);
}
```

API 호출을 통해 비즈니스 도메인 엔터티를 직접 반환하지 않도록 합니다. 도메인 엔터티는:

* 클라이언트가 요구하는 것보다 더 많은 데이터를 포함할 수 있습니다.
* 앱의 내부 도메인 모델과 공개된 API를 불필요하게 결합할 수 있습니다.

도메인 엔터티와 클라이언트에 반환되는 유형 간의 매핑은 다음과 같이 수행할 수 있습니다:

* 샘플 앱에서 사용하는 것처럼 LINQ `Select`로 수동으로 수행합니다. 자세한 내용은 [LINQ (Language Integrated Query)](https://learn.microsoft.com/en-us/dotnet/standard/using-linq)를 참조하십시오.
* [AutoMapper](https://github.com/AutoMapper/AutoMapper)와 같은 라이브러리를 사용하여 자동으로 수행합니다.

다음으로, 샘플앱은 Ideas 컨트롤러의 `Create` 및 `ForSession` API 메서드에 대한 단위 테스트를 시연합니다.

샘플 앱에는 두 개의 `ForSession` 테스트가 포함되어 있습니다. 첫 번째 테스트는 유효하지 않은 세션에 대해 `ForSession`이 `NotFoundObjectResult` (HTTP Not Found)를 반환하는지 확인합니다:

```C#
[Fact]
public async Task ForSession_ReturnsHttpNotFound_ForInvalidSession()
{
    // Arrange
    int testSessionId = 123;
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync((BrainstormSession)null);
    var controller = new IdeasController(mockRepo.Object);

    // Act
    var result = await controller.ForSession(testSessionId);

    // Assert
    var notFoundObjectResult = Assert.IsType<NotFoundObjectResult>(result);
    Assert.Equal(testSessionId, notFoundObjectResult.Value);
}
```

두 번째 `ForSession` 테스트는 유효한 세션에 대해 `ForSession`이 세션 아이디어(`<List<IdeaDTO>>`) 목록을 반환하는지 확인합니다. 또한 첫 번째 아이디어의 `Name` 속성이 올바른지 확인합니다:

```C#
[Fact]
public async Task ForSession_ReturnsIdeasForSession()
{
    // Arrange
    int testSessionId = 123;
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync(GetTestSession());
    var controller = new IdeasController(mockRepo.Object);

    // Act
    var result = await controller.ForSession(testSessionId);

    // Assert
    var okResult = Assert.IsType<OkObjectResult>(result);
    var returnValue = Assert.IsType<List<IdeaDTO>>(okResult.Value);
    var idea = returnValue.FirstOrDefault();
    Assert.Equal("One", idea.Name);
}
```

`Create` 메서드의 동작을 테스트하기 위해 샘플 앱은 테스트의 일부로 컨트롤러에 모델 오류를 추가합니다. 단위 테스트에서 모델 유효성 검사나 모델 바인딩을 테스트하려고 하지 말고, 잘못된 `ModelState`와 마주쳤을 때 액션 메서드의 동작만 테스트하십시오:

```C#
[Fact]
public async Task Create_ReturnsBadRequest_GivenInvalidModel()
{
    // Arrange & Act
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    var controller = new IdeasController(mockRepo.Object);
    controller.ModelState.AddModelError("error", "some error");

    // Act
    var result = await controller.Create(model: null);

    // Assert
    Assert.IsType<BadRequestObjectResult>(result);
}
```

`Create`의 두 번째 테스트는 저장소가 `null`을 반환하는 경우에 따라 다르므로, 모의 저장소는 `null`을 반환하도록 구성됩니다. 이 결과를 반환하는 쿼리를 구성하고 메모리 내 또는 기타 방식으로 테스트 데이터베이스를 생성할 필요가 없습니다. 테스트는 샘플 코드에서 설명한 대로 단일 문장으로 완료될 수 있습니다:

```C#
[Fact]
public async Task Create_ReturnsHttpNotFound_ForInvalidSession()
{
    // Arrange
    int testSessionId = 123;
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync((BrainstormSession)null);
    var controller = new IdeasController(mockRepo.Object);

    // Act
    var result = await controller.Create(new NewIdeaModel());

    // Assert
    Assert.IsType<NotFoundObjectResult>(result);
}
```

세 번째 `Create` 테스트, `Create_ReturnsNewlyCreatedIdeaForSession`은 저장소의 `UpdateAsync` 메서드가 호출되는지 확인합니다. 모의는 `Verifiable`로 호출되며, 모의 저장소의 `Verify` 메서드를 호출하여 검증 가능한 메서드가 실행되었는지 확인합니다. 데이터가 저장되었는지 확인하는 것은 단위 테스트의 책임이 아닙니다. 이는 통합 테스트로 수행할 수 있습니다.

```C#
[Fact]
public async Task Create_ReturnsNewlyCreatedIdeaForSession()
{
    // Arrange
    int testSessionId = 123;
    string testName = "test name";
    string testDescription = "test description";
    var testSession = GetTestSession();
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync(testSession);
    var controller = new IdeasController(mockRepo.Object);

    var newIdea = new NewIdeaModel()
    {
        Description = testDescription,
        Name = testName,
        SessionId = testSessionId
    };
    mockRepo.Setup(repo => repo.UpdateAsync(testSession))
        .Returns(Task.CompletedTask)
        .Verifiable();

    // Act
    var result = await controller.Create(newIdea);

    // Assert
    var okResult = Assert.IsType<OkObjectResult>(result);
    var returnSession = Assert.IsType<BrainstormSession>(okResult.Value);
    mockRepo.Verify();
    Assert.Equal(2, returnSession.Ideas.Count());
    Assert.Equal(testName, returnSession.Ideas.LastOrDefault().Name);
    Assert.Equal(testDescription, returnSession.Ideas.LastOrDefault().Description);
}
```

## Test ActionResult\<T>

[ActionResult\<T>](https://learn.microsoft.com/en-us/aspnet/core/web-api/action-return-types?view=aspnetcore-8.0#actionresultt-type)  ([ActionResult\<TValue>](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1))는 `ActionResult`를 상속하는 유형을 반환하거나 특정 유형을 반환할 수 있습니다.

샘플 앱에는 주어진 세션 `id`에 대한 `List<IdeaDTO>`를 반환하는 메서드가 포함되어 있습니다. 세션 `id`가 존재하지 않으면, 컨트롤러는 `NotFound`를 반환합니다:

```C#
[HttpGet("forsessionactionresult/{sessionId}")]
[ProducesResponseType(200)]
[ProducesResponseType(404)]
public async Task<ActionResult<List<IdeaDTO>>> ForSessionActionResult(int sessionId)
{
    var session = await _sessionRepository.GetByIdAsync(sessionId);

    if (session == null)
    {
        return NotFound(sessionId);
    }

    var result = session.Ideas.Select(idea => new IdeaDTO()
    {
        Id = idea.Id,
        Name = idea.Name,
        Description = idea.Description,
        DateCreated = idea.DateCreated
    }).ToList();

    return result;
}
```

두 개의 `ForSessionActionResult` 컨트롤러 테스트가 `ApiIdeasControllerTests`에 포함되어 있습니다.

첫 번째 테스트는 컨트롤러가 `ActionResult`를 반환하지만 존재하지 않는 세션 `id`에 대한 아이디어 목록을 반환하지 않는지 확인합니다:

* `ActionResult` 유형은 `ActionResult<List<IdeaDTO>>`입니다.
* `Result`는 `NotFoundObjectResult`입니다.

```C#
[Fact]
public async Task ForSessionActionResult_ReturnsNotFoundObjectResultForNonexistentSession()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    var controller = new IdeasController(mockRepo.Object);
    var nonExistentSessionId = 999;

    // Act
    var result = await controller.ForSessionActionResult(nonExistentSessionId);

    // Assert
    var actionResult = Assert.IsType<ActionResult<List<IdeaDTO>>>(result);
    Assert.IsType<NotFoundObjectResult>(actionResult.Result);
}
```

유효한 세션 `id`에 대해, 두 번째 테스트는 메서드가 다음을 반환하는지 확인합니다:

* `List<IdeaDTO>` 유형의 `ActionResult`.
* [ActionResult\<T>.Value](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1.value)는 `List<IdeaDTO>` 유형입니다.
* 목록의 첫 번째 항목은 모의 세션에 저장된 아이디어와 일치하는 유효한 아이디어입니다(`GetTestSession`을 호출하여 얻음).

```C#
[Fact]
public async Task ForSessionActionResult_ReturnsIdeasForSession()
{
    // Arrange
    int testSessionId = 123;
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync(GetTestSession());
    var controller = new IdeasController(mockRepo.Object);

    // Act
    var result = await controller.ForSessionActionResult(testSessionId);

    // Assert
    var actionResult = Assert.IsType<ActionResult<List<IdeaDTO>>>(result);
    var returnValue = Assert.IsType<List<IdeaDTO>>(actionResult.Value);
    var idea = returnValue.FirstOrDefault();
    Assert.Equal("One", idea.Name);
}
```

샘플 앱에는 주어진 세션에 대해 새로운 `Idea`를 생성하는 메서드도 포함되어 있습니다. 컨트롤러는 다음을 반환합니다:

* 유효하지 않은 모델에 대해 `BadRequest`.
* 세션이 존재하지 않는 경우 `NotFound`.
* 세션이 새로운 아이디어로 업데이트되면 `CreatedAtAction`.

```C#
[HttpPost("createactionresult")]
[ProducesResponseType(201)]
[ProducesResponseType(400)]
[ProducesResponseType(404)]
public async Task<ActionResult<BrainstormSession>> CreateActionResult([FromBody]NewIdeaModel model)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    var session = await _sessionRepository.GetByIdAsync(model.SessionId);

    if (session == null)
    {
        return NotFound(model.SessionId);
    }

    var idea = new Idea()
    {
        DateCreated = DateTimeOffset.Now,
        Description = model.Description,
        Name = model.Name
    };
    session.AddIdea(idea);

    await _sessionRepository.UpdateAsync(session);

    return CreatedAtAction(nameof(CreateActionResult), new { id = session.Id }, session);
}
```

`CreateActionResult`의 세 가지 테스트가 `ApiIdeasControllerTests`에 포함되어 있습니다.

첫 번째 테스트는 유효하지 않은 모델에 대해 `BadRequest`가 반환되는지 확인합니다.

```C#
[Fact]
public async Task CreateActionResult_ReturnsBadRequest_GivenInvalidModel()
{
    // Arrange & Act
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    var controller = new IdeasController(mockRepo.Object);
    controller.ModelState.AddModelError("error", "some error");

    // Act
    var result = await controller.CreateActionResult(model: null);

    // Assert
    var actionResult = Assert.IsType<ActionResult<BrainstormSession>>(result);
    Assert.IsType<BadRequestObjectResult>(actionResult.Result);
}
```

두 번째 테스트는 세션이 존재하지 않는 경우 `NotFound`가 반환되는지 확인합니다.

```C#
[Fact]
public async Task CreateActionResult_ReturnsNotFoundObjectResultForNonexistentSession()
{
    // Arrange
    var nonExistentSessionId = 999;
    string testName = "test name";
    string testDescription = "test description";
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    var controller = new IdeasController(mockRepo.Object);

    var newIdea = new NewIdeaModel()
    {
        Description = testDescription,
        Name = testName,
        SessionId = nonExistentSessionId
    };

    // Act
    var result = await controller.CreateActionResult(newIdea);

    // Assert
    var actionResult = Assert.IsType<ActionResult<BrainstormSession>>(result);
    Assert.IsType<NotFoundObjectResult>(actionResult.Result);
}
```

유효한 세션 `id`에 대해, 최종 테스트는 다음을 확인합니다:

* 메서드는 `BrainstormSession` 유형의 `ActionResult`를 반환합니다.
* [ActionResult\<T>.Result](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1.result)는 `CreatedAtActionResult`입니다. `CreatedAtActionResult`는 `Location` 헤더가 있는 *201 Created* 응답과 유사합니다.
* [ActionResult\<T>.Value](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1.value)는 `BrainstormSession` 유형입니다.
* 세션을 업데이트하기 위한 모의 호출 `UpdateAsync(testSession)`이 호출되었습니다. 검증 가능한 메서드 호출은 주장에서 `mockRepo.Verify()`를 실행하여 확인됩니다.
* 세션에 대해 두 개의 `Idea` 객체가 반환됩니다.
* 마지막 항목(모의 호출을 통해 세션에 추가된 `Idea`)은 테스트에서 세션에 추가된 `newIdea`와 일치합니다.

```C#
[Fact]
public async Task CreateActionResult_ReturnsNewlyCreatedIdeaForSession()
{
    // Arrange
    int testSessionId = 123;
    string testName = "test name";
    string testDescription = "test description";
    var testSession = GetTestSession();
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.GetByIdAsync(testSessionId))
        .ReturnsAsync(testSession);
    var controller = new IdeasController(mockRepo.Object);

    var newIdea = new NewIdeaModel()
    {
        Description = testDescription,
        Name = testName,
        SessionId = testSessionId
    };
    mockRepo.Setup(repo => repo.UpdateAsync(testSession))
        .Returns(Task.CompletedTask)
        .Verifiable();

    // Act
    var result = await controller.CreateActionResult(newIdea);

    // Assert
    var actionResult = Assert.IsType<ActionResult<BrainstormSession>>(result);
    var createdAtActionResult = Assert.IsType<CreatedAtActionResult>(actionResult.Result);
    var returnValue = Assert.IsType<BrainstormSession>(createdAtActionResult.Value);
    mockRepo.Verify();
    Assert.Equal(2, returnValue.Ideas.Count());
    Assert.Equal(testName, returnValue.Ideas.LastOrDefault().Name);
    Assert.Equal(testDescription, returnValue.Ideas.LastOrDefault().Description);
}
```

## 추가 자료

* [Integration tests in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-8.0)
* [Visual Studio에서 단위 테스트 생성 및 실행](/visualstudio/test/unit-test-your-code)
* [MyTested.AspNetCore.Mvc - ASP.NET Core MVC를 위한 유창한 테스트 라이브러리](https://github.com/ivaylokenov/MyTested.AspNetCore.Mvc): MVC 및 웹 API 앱을 테스트하기 위한 강력한 형식의 단위 테스트 라이브러리로, 유창한 인터페이스를 제공합니다. (*Microsoft에서 유지 관리하거나 지원하지 않습니다.*)
* [JustMockLite](https://github.com/telerik/JustMockLite): .NET 개발자를 위한 모의 프레임워크입니다. (*Microsoft에서 유지 관리하거나 지원하지 않습니다.*)

---
## 출처
[Unit test controller logic in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/testing?view=aspnetcore-8.0)

---
## [다음](./09_01_get_started.md)
