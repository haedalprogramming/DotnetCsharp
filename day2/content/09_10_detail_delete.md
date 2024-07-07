# Part 10, examine the Details and Delete methods of an ASP.NET Core app

## 목차
- [Part 10, examine the Details and Delete methods of an ASP.NET Core app](#part-10-examine-the-details-and-delete-methods-of-an-aspnet-core-app)
  - [목차](#목차)
    - [Azure에 게시하기](#azure에-게시하기)
  - [신뢰할 수 있는 웹 앱 패턴](#신뢰할-수-있는-웹-앱-패턴)
  - [출처](#출처)

---
Movie 컨트롤러를 열고 `Details` 메서드를 확인하세요:

```C#
// GET: Movies/Details/5
public async Task<IActionResult> Details(int? id)
{
    if (id == null)
    {
        return NotFound();
    }

    var movie = await _context.Movie
        .FirstOrDefaultAsync(m => m.Id == id);
    if (movie == null)
    {
        return NotFound();
    }

    return View(movie);
}
```

이 액션 메서드를 생성한 MVC 스캐폴딩 엔진은 메서드를 호출하는 HTTP 요청을 보여주는 주석을 추가합니다. 이 경우, `Movies` 컨트롤러, `Details` 메서드 및 `id` 값을 포함하는 세 개의 URL 세그먼트가 있는 GET 요청입니다. 이러한 세그먼트는 `Program.cs`에 정의되어 있습니다.

```C#
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

EF는 `FirstOrDefaultAsync` 메서드를 사용하여 데이터를 쉽게 검색할 수 있게 합니다. 이 메서드에 내장된 중요한 보안 기능은 검색 메서드가 영화를 찾았는지 확인한 후에만 해당 영화와 관련된 작업을 시도하도록 하는 것입니다. 예를 들어, 해커가 링크에서 생성된 URL을 `http://localhost:{PORT}/Movies/Details/1`에서 `http://localhost:{PORT}/Movies/Details/12345`와 같이 실제 영화를 나타내지 않는 값으로 변경하여 사이트에 오류를 도입할 수 있습니다. 영화를 찾지 못한 경우를 확인하지 않으면, 앱은 예외를 던질 것입니다.

`Delete` 및 `DeleteConfirmed` 메서드를 확인하세요.

```C#
// GET: Movies/Delete/5
public async Task<IActionResult> Delete(int? id)
{

    if (id == null)
    {
        return NotFound();
    }

    var movie = await _context.Movie
        .FirstOrDefaultAsync(m => m.Id == id);
    if (movie == null)
    {
        return NotFound();
    }

    return View(movie);
}

// POST: Movies/Delete/5
[HttpPost, ActionName("Delete")]
[ValidateAntiForgeryToken]
public async Task<IActionResult> DeleteConfirmed(int id)
{
    var movie = await _context.Movie.FindAsync(id);
    if (movie != null)
    {
        _context.Movie.Remove(movie);
    }

    await _context.SaveChangesAsync();
    return RedirectToAction(nameof(Index));
}
```

`HTTP GET Delete` 메서드는 지정된 영화를 삭제하지 않고, 삭제를 제출할 수 있는(HTTP POST) 영화 뷰를 반환한다는 점에 유의하세요. GET 요청에 대한 응답으로 삭제 작업을 수행하는 것(또는 데이터 변경 작업을 수행하는 편집 작업, 생성 작업 등)은 보안 취약점을 열 수 있습니다.

데이터를 삭제하는 `[HttpPost]` 메서드는 고유한 서명 또는 이름을 부여하기 위해 `DeleteConfirmed`라고 명명됩니다. 두 메서드 서명은 아래와 같습니다:

```C#
// GET: Movies/Delete/5
public async Task<IActionResult> Delete(int? id)
{
```

```C#
// POST: Movies/Delete/5
[HttpPost, ActionName("Delete")]
[ValidateAntiForgeryToken]
public async Task<IActionResult> DeleteConfirmed(int id)
{
```

공용 언어 런타임(CLR)은 오버로드된 메서드가 고유한 매개변수 서명을 가지도록 요구합니다(같은 메서드 이름이지만 다른 매개변수 목록). 그러나 여기서는 동일한 매개변수 서명을 가진 두 개의 `Delete` 메서드(하나는 GET, 하나는 POST)가 필요합니다. (둘 다 단일 정수를 매개변수로 받아야 합니다.)

이 문제에 대한 두 가지 접근 방식이 있으며, 하나는 메서드에 다른 이름을 부여하는 것입니다. 이는 앞선 예제에서 스캐폴딩 메커니즘이 한 것입니다. 그러나 이는 작은 문제를 도입합니다. ASP.NET은 URL의 세그먼트를 이름으로 액션 메서드에 매핑하고, 메서드 이름을 변경하면 라우팅이 해당 메서드를 찾을 수 없습니다. 해결책은 `DeleteConfirmed` 메서드에 `ActionName("Delete")` 속성을 추가하는 것입니다. 이 속성은 라우팅 시스템이 POST 요청을 위한 /Delete/를 포함하는 URL을 `DeleteConfirmed` 메서드로 매핑하도록 합니다.

동일한 이름과 서명을 가진 메서드에 대한 또 다른 일반적인 해결 방법은 POST 메서드의 서명에 추가(사용되지 않는) 매개변수를 인위적으로 추가하는 것입니다. 이전 게시물에서 `notUsed` 매개변수를 추가할 때 그렇게 했습니다. 여기에서도 `[HttpPost] Delete` 메서드에 동일한 작업을 수행할 수 있습니다:

```csharp
// POST: Movies/Delete/6
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> Delete(int id, bool notUsed)
```

### Azure에 게시하기

Azure에 배포하는 정보는 [자습서: Azure App Service에서 ASP.NET Core 및 SQL 데이터베이스 앱 빌드](https://learn.microsoft.com/en-us/azure/app-service/tutorial-dotnetcore-sqldb-app)를 참조하세요.

## 신뢰할 수 있는 웹 앱 패턴

.NET용 신뢰할 수 있는 웹 앱 패턴에 대한 [YouTube 동영상](https://www.youtube.com/watch?v=hNoUT9NRzDM)과 [기사](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/reliable-web-app/dotnet/pattern-overview)를 참조하여 현대적이고 신뢰할 수 있으며, 성능이 우수하고, 테스트 가능하며, 비용 효율적이고, 확장 가능한 ASP.NET Core 앱을 처음부터 만들거나 기존 앱을 리팩토링하는 방법에 대한 지침을 확인하세요.

---
## 출처
[Part 10, examine the Details and Delete methods of an ASP.NET Core app](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/details?view=aspnetcore-8.0)

