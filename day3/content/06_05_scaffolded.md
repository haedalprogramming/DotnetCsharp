# Part 3, scaffolded Razor Pages in ASP.NET Core


## 목차
- [Part 3, scaffolded Razor Pages in ASP.NET Core](#part-3-scaffolded-razor-pages-in-aspnet-core)
  - [목차](#목차)
  - [생성(Create), 삭제(Delete), 세부 사항(Details) 및 편집(Edit) 페이지](#생성create-삭제delete-세부-사항details-및-편집edit-페이지)
    - [@page 지시문](#page-지시문)
    - [@model 지시문](#model-지시문)
    - [레이아웃 페이지](#레이아웃-페이지)
    - [ViewData와 레이아웃](#viewdata와-레이아웃)
    - [레이아웃 업데이트](#레이아웃-업데이트)
    - [생성 페이지 모델](#생성-페이지-모델)
    - [생성 Razor 페이지](#생성-razor-페이지)
  - [출처](#출처)
  - [다음](#다음)

---

## 생성(Create), 삭제(Delete), 세부 사항(Details) 및 편집(Edit) 페이지

`Pages/Movies/Index.cshtml.cs` 페이지 모델을 확인해 보세요:

```C#
using Microsoft.AspNetCore.Mvc.RazorPages;
using Microsoft.EntityFrameworkCore;
using RazorPagesMovie.Models;

namespace RazorPagesMovie.Pages.Movies;

public class IndexModel : PageModel
{
    private readonly RazorPagesMovie.Data.RazorPagesMovieContext _context;

    public IndexModel(RazorPagesMovie.Data.RazorPagesMovieContext context)
    {
        _context = context;
    }

    public IList<Movie> Movie { get;set; }  = default!;

    public async Task OnGetAsync()
    {
        if (_context.Movie != null)
        {
            Movie = await _context.Movie.ToListAsync();
        }
    }
}
```

Razor Pages는 `PageModel`에서 파생됩니다. 관례상, `PageModel` 파생 클래스는 `PageNameModel`로 명명됩니다. 예를 들어, 인덱스 페이지는 `IndexModel`로 명명됩니다.

생성자는 [의존성 주입](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 사용하여 `RazorPagesMovieContext`를 페이지에 추가합니다:

```C#
public class IndexModel : PageModel
{
    private readonly RazorPagesMovie.Data.RazorPagesMovieContext _context;

    public IndexModel(RazorPagesMovie.Data.RazorPagesMovieContext context)
    {
        _context = context;
    }
```

비동기 프로그래밍에 대한 자세한 내용은 [비동기 코드](https://learn.microsoft.com/en-us/aspnet/core/data/ef-rp/intro?view=aspnetcore-8.0#asynchronous-code)를 참조하십시오.

페이지에 대한 `GET` 요청이 있을 때, `OnGetAsync` 메서드는 Razor 페이지에 영화 목록을 반환합니다. Razor 페이지에서 `OnGetAsync` 또는 `OnGet`이 호출되어 페이지의 상태를 초기화합니다. 이 경우, `OnGetAsync`는 영화 목록을 가져와서 표시합니다.

`OnGet`이 `void`를 반환하거나 `OnGetAsync`가 `Task`를 반환할 때는 반환문을 사용하지 않습니다. 예를 들어, 개인정보 보호 페이지를 확인해 보세요:

```C#
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;

namespace RazorPagesMovie.Pages
{
    public class PrivacyModel : PageModel
    {
        private readonly ILogger<PrivacyModel> _logger;

        public PrivacyModel(ILogger<PrivacyModel> logger)
        {
            _logger = logger;
        }

        public void OnGet()
        {
        }
    }
}
```

반환 타입이 `IActionResult` 또는 `Task<IActionResult>`일 때는 반환문을 제공해야 합니다. 예를 들어, `Pages/Movies/Create.cshtml.cs`의 `OnPostAsync` 메서드를 확인해 보세요:

```C#
public async Task<IActionResult> OnPostAsync()
{
  if (!ModelState.IsValid)
    {
        return Page();
    }

    _context.Movie.Add(Movie);
    await _context.SaveChangesAsync();

    return RedirectToPage("./Index");
}
```

<a name="index6"></a>
`Pages/Movies/Index.cshtml` Razor 페이지를 확인해 보세요:

```cshtml
@page
@model RazorPagesMovie.Pages.Movies.IndexModel

@{
    ViewData["Title"] = "Index";
}

<h1>Index</h1>

<p>
    <a asp-page="Create">Create New</a>
</p>
<table class="table">
    <thead>
        <tr>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].Title)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].ReleaseDate)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].Genre)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Movie[0].Price)
            </th>
            <th></th>
        </tr>
    </thead>
    <tbody>
@foreach (var item in Model.Movie) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Title)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.ReleaseDate)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Genre)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Price)
            </td>
            <td>
                <a asp-page="./Edit" asp-route-id="@item.Id">Edit</a> |
                <a asp-page="./Details" asp-route-id="@item.Id">Details</a> |
                <a asp-page="./Delete" asp-route-id="@item.Id">Delete</a>
            </td>
        </tr>
}
    </tbody>
</table>
```


Razor는 HTML에서 C# 또는 Razor 전용 마크업으로 전환할 수 있습니다. `@` 기호 뒤에 [Razor 예약 키워드](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-8.0#razor-reserved-keywords)가 오면 Razor 전용 마크업으로 전환되고, 그렇지 않으면 C#으로 전환됩니다.

### @page 지시문

`@page` Razor 지시문은 파일을 MVC 액션으로 만들어 요청을 처리할 수 있게 합니다. `@page`는 페이지의 첫 번째 Razor 지시문이어야 합니다. `@page`와 `@model`은 Razor 전용 마크업으로 전환하는 예입니다. 자세한 내용은 [Razor 구문](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-8.0#razor-syntax)을 참조하십시오.

<a name="md"></a>

### @model 지시문

```cshtml
@page
@model RazorPagesMovie.Pages.Movies.IndexModel
```

`@model` 지시문은 Razor 페이지에 전달된 모델의 타입을 지정합니다. 위의 예에서 `@model` 라인은 Razor 페이지에 `PageModel` 파생 클래스를 사용할 수 있게 합니다. 모델은 페이지에서 `@Html.DisplayNameFor`와 `@Html.DisplayFor` [HTML 도우미](https://learn.microsoft.com/en-us/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers)에서 사용됩니다.

다음 HTML 도우미에서 사용된 람다 표현식을 확인해 보세요:

```cshtml
@Html.DisplayNameFor(model => model.Movie[0].Title)
```

`DisplayNameFor` HTML 도우미는 람다 표현식에서 참조된 `Title` 속성을 검사하여 표시 이름을 결정합니다. 람다 표현식은 평가되지 않고 검사됩니다. 이는 `model`, `model.Movie` 또는 `model.Movie[0]`이 `null`이거나 비어 있어도 접근 위반이 발생하지 않음을 의미합니다. 예를 들어, `@Html.DisplayFor(modelItem => item.Title)`과 같이 람다 표현식이 평가되면 모델의 속성 값이 평가됩니다.

### 레이아웃 페이지

메뉴 링크 **RazorPagesMovie**, **Home**, **Privacy**를 선택합니다. 각 페이지는 동일한 메뉴 레이아웃을 보여줍니다. 메뉴 레이아웃은 `Pages/Shared/_Layout.cshtml` 파일에 구현됩니다.

`Pages/Shared/_Layout.cshtml` 파일을 열고 확인해 보세요.

[레이아웃](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/layout?view=aspnetcore-8.0) 템플릿을 사용하면 HTML 컨테이너 레이아웃을 다음과 같이 할 수 있습니다:

* 한 곳에 지정할 수 있습니다.
* 사이트의 여러 페이지에 적용할 수 있습니다.

`@RenderBody()` 라인을 찾습니다. `RenderBody`는 모든 페이지별 뷰가 레이아웃 페이지에 *포함*되어 나타나는 자리 표시자입니다. 예를 들어, **Privacy** 링크를 선택하면 `Pages/Privacy.cshtml` 뷰가 `RenderBody` 메서드 내에 렌더링됩니다.

<a name="vd"></a>

### ViewData와 레이아웃

`Pages/Movies/Index.cshtml` 파일의 다음 마크업을 확인해 보세요:

```C#
@page
@model RazorPagesMovie.Pages.Movies.IndexModel

@{
    ViewData["Title"] = "Index";
}
```

위의 강조된 마크업은 Razor가 C#으로 전환되는 예입니다. `{`와 `}` 문자는 C# 코드 블록을 감쌉니다.

`PageModel` 기본 클래스에는 `ViewData` 사전 속성이 포함되어 있으며 이를 사용하여 View에 데이터를 전달할 수 있습니다. `ViewData` 사전에 객체를 추가할 때 ***키 값*** 패턴을 사용합니다. 위의 샘플에서는 `Title` 속성이 `ViewData` 사전에 추가되었습니다.

`Title` 속성은 `Pages/Shared/_Layout.cshtml` 파일에서 사용됩니다. 다음 마크업은 `_Layout.cshtml` 파일의 첫 몇 줄을 보여줍니다.

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - RazorPagesMovie</title>
    <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.min.css" />
    <link rel="stylesheet" href="~/css/site.css" asp-append-version="true" />
    <link rel="stylesheet" href="~/RazorPagesMovie.styles.css" asp-append-version="true" />
```

### 레이아웃 업데이트

1. `Pages/Shared/_Layout.cshtml` 파일에서 `<title>` 요소를 **RazorPagesMovie** 대신 **Movie**로 변경합니다.
  ```CSHTML
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>@ViewData["Title"] - Movie</title>
  ```

2. `Pages/Shared/_Layout.cshtml` 파일에서 다음 앵커 요소를 찾습니다.

   ```cshtml
   <a class="navbar-brand" asp-area="" asp-page="/Index">RazorPagesMovie</a>
   ```

3. 위의 요소를 다음 마크업으로 교체합니다:

   ```cshtml
   <a class="navbar-brand" asp-page="/Movies/Index">RpMovie</a>
   ```

   위의 앵커 요소는 [태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-8.0)입니다. 이 경우, [앵커 태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/built-in/anchor-tag-helper?view=aspnetcore-8.0)입니다. `asp-page="/Movies/Index"` 태그 도우미 속성과 값은 `/Movies/Index` Razor 페이지로의 링크를 만듭니다. `asp-area` 속성 값은 비어 있으므로 영역은 링크에 사용되지 않습니다. 자세한 내용은 [영역](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/areas?view=aspnetcore-8.0)을 참조하십시오.

4. 변경 사항을 저장하고 **RpMovie** 링크를 선택하여 앱을 테스트합니다. 문제가 있는 경우 GitHub의 [_Layout.cshtml](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie80/Pages/Shared/_Layout.cshtml) 파일을 참조하십시오.

5. **Home**, **RpMovie**, **Create**, **Edit**, **Delete** 링크를 테스트합니다. 각 페이지는 제목을 설정하며, 이는 브라우저 탭에서 확인할 수 있습니다. 페이지를 북마크하면 제목이 북마크에 사용됩니다.

> [!NOTE]
> `Price` 필드에 소수점 쉼표를 입력할 수 없을 수도 있습니다. 소수점으로 쉼표(",")를 사용하는 비영어권 로캘과 미국식이 아닌 날짜 형식을 지원하려면 앱을 글로벌화해야 합니다. [이 GitHub 문제 4076](https://github.com/dotnet/AspNetCore.Docs/issues/4076#issuecomment-326590420)을 참조하여 소수점 쉼표를 추가하는 방법을 확인하십시오.

`Layout` 속성은 `Pages/_ViewStart.cshtml` 파일에서 설정됩니다:

```CSHTML
@{
    Layout = "_Layout";
}
```

위의 마크업은 *Pages* 폴더 아래의 모든 Razor 파일에 대해 레이아웃 파일을 `Pages/Shared/_Layout.cshtml`로 설정합니다. 자세한 내용은 [레이아웃](https://learn.microsoft.com/en-us/aspnet/core/razor-pages/?view=aspnetcore-8.0#layout)을 참조하십시오.

### 생성 페이지 모델

`Pages/Movies/Create.cshtml.cs` 페이지 모델을 확인해 보세요:

```C#
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;
using RazorPagesMovie.Models;

namespace RazorPagesMovie.Pages.Movies
{
    public class CreateModel : PageModel
    {
        private readonly RazorPagesMovie.Data.RazorPagesMovieContext _context;

        public CreateModel(RazorPagesMovie.Data.RazorPagesMovieContext context)
        {
            _context = context;
        }

        public IActionResult OnGet()
        {
            return Page();
        }

        [BindProperty]
        public Movie Movie { get; set; } = default!;
        

        // To protect from overposting attacks, see https://aka.ms/RazorPagesCRUD
        public async Task<IActionResult> OnPostAsync()
        {
          if (!ModelState.IsValid || _context.Movie == null || Movie == null)
            {
                return Page();
            }

            _context.Movie.Add(Movie);
            await _context.SaveChangesAsync();

            return RedirectToPage("./Index");
        }
    }
}
```

`OnGet` 메서드는 페이지에 필요한 상태를 초기화합니다. 생성 페이지는 초기화할 상태가 없으므로 `Page`를 반환합니다. 나중에 튜토리얼에서 `OnGet`이 상태를 초기화하는 예가 나옵니다. `Page` 메서드는 `Create.cshtml` 페이지를 렌더링하는 `PageResult` 객체를 생성합니다.

`Movie` 속성은 [[BindProperty]](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) 속성을 사용하여 [모델 바인딩](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-8.0)에 참여합니다. 생성 폼이 폼 값을 게시하면, ASP.NET Core 런타임은 게시된 값을 `Movie` 모델에 바인딩합니다.

`OnPostAsync` 메서드는 페이지가 폼 데이터를 게시할 때 실행됩니다:

```C#
public async Task<IActionResult> OnPostAsync()
{
  if (!ModelState.IsValid)
    {
        return Page();
    }

    _context.Movie.Add(Movie);
    await _context.SaveChangesAsync();

    return RedirectToPage("./Index");
}
```

모델 오류가 있는 경우, 폼이 다시 표시되고 게시된 폼 데이터가 함께 표시됩니다. 대부분의 모델 오류는 폼이 게시되기 전에 클라이언트 측에서 잡을 수 있습니다. 모델 오류의 예는 날짜 필드에 날짜로 변환할 수 없는 값을 게시하는 것입니다. 클라이언트 측 유효성 검사와 모델 유효성 검사는 나중에 튜토리얼에서 다룹니다.

모델 오류가 없는 경우:

* 데이터가 저장됩니다.
* 브라우저가 인덱스 페이지로 리디렉션됩니다.

### 생성 Razor 페이지

`Pages/Movies/Create.cshtml` Razor 페이지 파일을 확인해 보세요:

```C#
@page
@model RazorPagesMovie.Pages.Movies.CreateModel

@{
    ViewData["Title"] = "Create";
}

<h1>Create</h1>

<h4>Movie</h4>
<hr />
<div class="row">
    <div class="col-md-4">
        <form method="post">
            <div asp-validation-summary="ModelOnly" class="text-danger"></div>
            <div class="form-group">
                <label asp-for="Movie.Title" class="control-label"></label>
                <input asp-for="Movie.Title" class="form-control" />
                <span asp-validation-for="Movie.Title" class="text-danger"></span>
            </div>
            <div class="form-group">
                <label asp-for="Movie.ReleaseDate" class="control-label"></label>
                <input asp-for="Movie.ReleaseDate" class="form-control" />
                <span asp-validation-for="Movie.ReleaseDate" class="text-danger"></span>
            </div>
            <div class="form-group">
                <label asp-for="Movie.Genre" class="control-label"></label>
                <input asp-for="Movie.Genre" class="form-control" />
                <span asp-validation-for="Movie.Genre" class="text-danger"></span>
            </div>
            <div class="form-group">
                <label asp-for="Movie.Price" class="control-label"></label>
                <input asp-for="Movie.Price" class="form-control" />
                <span asp-validation-for="Movie.Price" class="text-danger"></span>
            </div>
            <div class="form-group">
                <input type="submit" value="Create" class="btn btn-primary" />
            </div>
        </form>
    </div>
</div>

<div>
    <a asp-page="Index">Back to List</a>
</div>

@section Scripts {
    @{await Html.RenderPartialAsync("_ValidationScriptsPartial");}
}
```

다음 태그 도우미가 위의 마크업에서 표시됩니다:

* `<form method="post">`
* `<div asp-validation-summary="ModelOnly" class="text-danger"></div>`
* `<label asp-for="Movie.Title" class="control-label"></label>`
* `<input asp-for="Movie.Title" class="form-control" />`
* `<span asp-validation-for="Movie.Title" class="text-danger"></span>`

---

`<form method="post">` 요소는 [폼 태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-8.0#the-form-tag-helper)입니다. 폼 태그 도우미는 자동으로 [위조 방지 토큰](https://learn.microsoft.com/en-us/aspnet/core/security/anti-request-forgery?view=aspnetcore-8.0)을 포함합니다.

스캐폴딩 엔진은 모델의 각 필드에 대해 ID를 제외하고 다음과 유사한 Razor 마크업을 생성합니다:

```CSHTML
<div asp-validation-summary="ModelOnly" class="text-danger"></div>
<div class="form-group">
    <label asp-for="Movie.Title" class="control-label"></label>
    <input asp-for="Movie.Title" class="form-control" />
    <span asp-validation-for="Movie.Title" class="text-danger"></span>
</div>
```

[유효성 검사 태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-8.0#the-validation-tag-helpers) (`<div asp-validation-summary`와 `<span asp-validation-for`)는 유효성 검사 오류를 표시합니다. 유효성 검사는 이 시리즈의 후반부에서 더 자세히 다룹니다.

[레이블 태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-8.0#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`)는 `Title` 속성에 대한 레이블 캡션과 `[for]` 속성을 생성합니다.

[입력 태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-8.0) (`<input asp-for="Movie.Title" class="form-control">`)는 [데이터 주석](https://learn.microsoft.com/en-us/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 속성을 사용하여 클라이언트 측의 jQuery 유효성 검사를 위해 필요한 HTML 속성을 생성합니다.

`<form method="post">`와 같은 태그 도우미에 대한 자세한 내용은 [ASP.NET Core의 태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-8.0)를 참조하십시오.

---
## 출처
[Part 3, scaffolded Razor Pages in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/page?view=aspnetcore-8.0&tabs=visual-studio-code%2Cvisual-studio)

---
## [다음](./06_06_db.md)
