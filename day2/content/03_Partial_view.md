# Partial views in ASP.NET Core

## 목차
- [Partial views in ASP.NET Core](#partial-views-in-aspnet-core)
  - [목차](#목차)
  - [부분 뷰를 사용하는 경우](#부분-뷰를-사용하는-경우)
  - [부분 뷰 선언](#부분-뷰-선언)
  - [부분 뷰 참조](#부분-뷰-참조)
    - [Razor Pages PageModel에서 부분 뷰 사용](#razor-pages-pagemodel에서-부분-뷰-사용)
    - [마크업 파일에서 부분 뷰 사용](#마크업-파일에서-부분-뷰-사용)
    - [Partial 태그 헬퍼](#partial-태그-헬퍼)
    - [비동기 HTML 헬퍼](#비동기-html-헬퍼)
    - [동기 HTML 헬퍼](#동기-html-헬퍼)
  - [부분 뷰 검색](#부분-뷰-검색)
  - [부분 뷰에서 데이터 접근](#부분-뷰에서-데이터-접근)
  - [출처](#출처)
  - [다음](#다음)

---

부분 뷰는 다른 마크업 파일의 렌더링된 출력 *내부에* HTML 출력을 렌더링하는 `@page` 지시문이 없는 Razor 마크업 파일(`.cshtml`)입니다.

*부분 뷰*라는 용어는 마크업 파일을 *뷰*라고 부르는 MVC 앱 또는 마크업 파일을 *페이지*라고 부르는 Razor Pages 앱을 개발할 때 사용됩니다. 이 주제에서는 MVC 뷰와 Razor Pages 페이지를 *마크업 파일*이라고 일반적으로 지칭합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/mvc/views/partial/sample) ([다운로드 방법](https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-8.0#how-to-download-a-sample))

## 부분 뷰를 사용하는 경우

부분 뷰는 다음과 같은 경우에 효과적입니다:

* 큰 마크업 파일을 더 작은 구성 요소로 나눕니다.

  여러 논리적 조각으로 구성된 큰 복잡한 마크업 파일에서 각 조각을 부분 뷰로 분리하여 작업하는 것이 유리합니다. 마크업 파일의 코드는 관리 가능해지며, 마크업은 전체 페이지 구조와 부분 뷰에 대한 참조만 포함합니다.
* 마크업 파일 간에 공통 마크업 콘텐츠의 중복을 줄입니다.

  동일한 마크업 요소가 여러 마크업 파일에서 사용되는 경우, 부분 뷰를 사용하면 마크업 콘텐츠의 중복을 하나의 부분 뷰 파일로 제거할 수 있습니다. 부분 뷰에서 마크업이 변경되면, 부분 뷰를 사용하는 마크업 파일의 렌더링된 출력이 업데이트됩니다.

부분 뷰는 공통 레이아웃 요소를 유지 관리하는 데 사용하지 않아야 합니다. 공통 레이아웃 요소는 _Layout.cshtml 파일에 지정해야 합니다.

마크업을 렌더링하기 위해 복잡한 렌더링 로직이나 코드 실행이 필요한 경우, 부분 뷰 대신 뷰 컴포넌트를 사용하십시오.

## 부분 뷰 선언

부분 뷰는 *Views* 폴더(MVC) 또는 *Pages* 폴더(Razor Pages) 내에 유지 관리되는 `@page` 지시문이 없는 `.cshtml` 마크업 파일입니다.

ASP.NET Core MVC에서는 컨트롤러의 `ViewResult`가 뷰나 부분 뷰를 반환할 수 있습니다. Razor Pages에서는 `PageModel`이 `PartialViewResult` 객체로 표현되는 부분 뷰를 반환할 수 있습니다. 부분 뷰 참조 및 렌더링에 대해서는 부분 뷰 참조 섹션을 참조하십시오.

MVC 뷰나 페이지 렌더링과 달리, 부분 뷰는 `_ViewStart.cshtml`을 실행하지 않습니다. `_ViewStart.cshtml`에 대한 자세한 내용은 [Layout in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/layout?view=aspnetcore-8.0)을 참조하십시오.

부분 뷰 파일 이름은 종종 밑줄(`_`)로 시작합니다. 이 명명 규칙은 필수는 아니지만, 부분 뷰를 뷰 및 페이지와 시각적으로 구분하는 데 도움이 됩니다.

## 부분 뷰 참조

:::moniker range=">= aspnetcore-2.0"

### Razor Pages PageModel에서 부분 뷰 사용

ASP.NET Core 2.0 또는 2.1에서는 다음 처리기 메서드가 *\_AuthorPartialRP.cshtml* 부분 뷰를 응답으로 렌더링합니다:

```csharp
public IActionResult OnGetPartial() =>
    new PartialViewResult
    {
        ViewName = "_AuthorPartialRP",
        ViewData = ViewData,
    };
```

ASP.NET Core 2.2 이상에서는 처리기 메서드가 `Partial` 메서드를 호출하여 `PartialViewResult` 객체를 생성할 수 있습니다:

```C#
public IActionResult OnGetPartial() =>
    Partial("_AuthorPartialRP");
```

### 마크업 파일에서 부분 뷰 사용

마크업 파일 내에서 부분 뷰를 참조하는 여러 가지 방법이 있습니다. 애플리케이션에서 다음 비동기 렌더링 접근 방식을 사용할 것을 권장합니다:

* Partial 태그 헬퍼
* 비동기 HTML 헬퍼

### Partial 태그 헬퍼

Partial 태그 헬퍼는 ASP.NET Core 2.1 이상이 필요합니다.

Partial 태그 헬퍼는 HTML과 유사한 구문을 사용하여 콘텐츠를 비동기적으로 렌더링합니다:

```cshtml
<partial name="_PartialName" />
```

파일 확장자가 있는 경우, 태그 헬퍼는 부분 뷰를 참조하며, 부분 뷰는 부분 뷰를 호출하는 마크업 파일과 동일한 폴더에 있어야 합니다:

```cshtml
<partial name="_PartialName.cshtml" />
```

다음 예제는 앱 루트에서 부분 뷰를 참조합니다. 물결표 슬래시(`~/`) 또는 슬래시(`/`)로 시작하는 경로는 앱 루트를 참조합니다:

**Razor Pages**

```cshtml
<partial name="~/Pages/Folder/_PartialName.cshtml" />
<partial name="/Pages/Folder/_PartialName.cshtml" />
```

**MVC**

```cshtml
<partial name="~/Views/Folder/_PartialName.cshtml" />
<partial name="/Views/Folder/_PartialName.cshtml" />
```

다음 예제는 상대 경로를 사용하여 부분 뷰를 참조합니다:

```cshtml
<partial name="../Account/_PartialName.cshtml" />
```

자세한 내용은 [Partial Tag Helper in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/built-in/partial-tag-helper?view=aspnetcore-8.0)을 참조하십시오.


### 비동기 HTML 헬퍼

HTML 헬퍼를 사용할 때, 모범 사례는 `PartialAsync`를 사용하는 것입니다. `PartialAsync`는 `IHtmlContent` 유형을  `Task<TResult>`로 래핑하여 반환합니다. 이 메서드는 `@` 문자로 접두사를 붙여 호출합니다:

```cshtml
@await Html.PartialAsync("_PartialName")
```

파일 확장자가 있는 경우, HTML 헬퍼는 부분 뷰를 참조하며, 부분 뷰는 부분 뷰를 호출하는 마크업 파일과 동일한 폴더에 있어야 합니다:

```cshtml
@await Html.PartialAsync("_PartialName.cshtml")
```

다음 예제는 앱 루트에서 부분 뷰를 참조합니다. 물결표 슬래시(`~/`) 또는 슬래시(`/`)로 시작하는 경로는 앱 루트를 참조합니다:


**Razor Pages**

```cshtml
@await Html.PartialAsync("~/Pages/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Pages/Folder/_PartialName.cshtml")
```

**MVC**

```cshtml
@await Html.PartialAsync("~/Views/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Views/Folder/_PartialName.cshtml")
```

다음 예제는 상대 경로를 사용하여 부분 뷰를 참조합니다:

```cshtml
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

또는 `RenderPartialAsync`를 사용하여 부분 뷰를 렌더링할 수 있습니다. 이 메서드는 `IHtmlContent`를 반환하지 않습니다. 렌더링된 출력을 직접 응답에 스트리밍합니다. 이 메서드는 결과를 반환하지 않으므로, Razor 코드 블록 내에서 호출해야 합니다:

```cshtml
@{
    await Html.RenderPartialAsync("_AuthorPartial");
}
```

`RenderPartialAsync`는 렌더링된 콘텐츠를 스트리밍하므로, 일부 시나리오에서 더 나은 성능을 제공합니다. 성능이 중요한 상황에서는 두 가지 접근 방식을 모두 벤치마크하여 더 빠른 응답을 생성하는 접근 방식을 사용하십시오.

### 동기 HTML 헬퍼

`Partial` 및 `RenderPartial`는 각각 `PartialAsync` 및 `RenderPartialAsync`의 동기 버전입니다. 동기 버전은 데드락이 발생할 수 있는 시나리오가 있기 때문에 권장되지 않습니다. 동기 메서드는 향후 릴리스에서 제거될 예정입니다.

> [!IMPORTANT]
> 코드를 실행해야 하는 경우, 부분 뷰 대신 뷰 컴포넌트를 사용하십시오.

`Partial` 또는 `RenderPartial`을 호출하면 Visual Studio 분석기 경고가 발생합니다. 예를 들어, `Partial`이 존재하면 다음과 같은 경고 메시지가 나타납니다:

> IHtmlHelper.Partial의 사용은 애플리케이션 데드락을 초래할 수 있습니다. &lt;partial&gt; 태그 헬퍼 또는 IHtmlHelper.PartialAsync 사용을 고려하십시오.

`@Html.Partial` 호출을 `@await Html.PartialAsync` 또는 Partial 태그 헬퍼로 대체하십시오. Partial 태그 헬퍼 마이그레이션에 대한 자세한 내용은 HTML 헬퍼에서 마이그레이션을 참조하십시오.


## 부분 뷰 검색

부분 뷰가 파일 확장자 없이 이름으로 참조될 때, 다음 위치가 순서대로 검색됩니다:

**Razor Pages**

1. 현재 실행 중인 페이지의 폴더
2. 페이지 폴더의 상위 디렉터리 그래프
3. `/Shared`
4. `/Pages/Shared`
5. `/Views/Shared`

**MVC**

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
2. `/Areas/<Area-Name>/Views/Shared`
3. `/Views/Shared`
4. `/Pages/Shared`


부분 뷰 검색에는 다음 규칙이 적용됩니다:

* 다른 폴더에 있는 경우, 동일한 파일 이름을 가진 다른 부분 뷰가 허용됩니다.
* 파일 확장자 없이 이름으로 부분 뷰를 참조할 때, 호출자의 폴더와 *Shared* 폴더 모두에 부분 뷰가 존재하면, 호출자의 폴더에 있는 부분 뷰가 제공됩니다. 호출자의 폴더에 부분 뷰가 없는 경우, *Shared* 폴더에서 부분 뷰가 제공됩니다. *Shared* 폴더의 부분 뷰는 *공유 부분 뷰* 또는 *기본 부분 뷰*라고 합니다.
* 부분 뷰는 *체인*이 가능하며, 부분 뷰가 순환 참조를 형성하지 않는 한 다른 부분 뷰를 호출할 수 있습니다. 상대 경로는 항상 현재 파일을 기준으로 하며, 파일의 루트 또는 부모를 기준으로 하지 않습니다.

> [!NOTE]
> 부분 뷰에 정의된 Razor `section`은 상위 마크업 파일에 보이지 않습니다. `section`은 정의된 부분 뷰에서만 보입니다.

## 부분 뷰에서 데이터 접근

부분 뷰가 인스턴스화될 때, 상위 `ViewData` 딕셔너리의 *복사본*을 받습니다. 부분 뷰 내에서 데이터에 대해 수행된 업데이트는 상위 뷰에 반영되지 않습니다. 부분 뷰에서 `ViewData`에 대한 변경 사항은 부분 뷰가 반환될 때 손실됩니다.

다음 예제는 `ViewDataDictionary`의 인스턴스를 부분 뷰에 전달하는 방법을 보여줍니다:

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

모델을 부분 뷰에 전달할 수 있습니다. 모델은 사용자 정의 객체일 수 있습니다. 모델은 `PartialAsync`(호출자에게 콘텐츠 블록을 렌더링) 또는 `RenderPartialAsync`(출력에 콘텐츠를 스트리밍)를 사용하여 전달할 수 있습니다:

```cshtml
@await Html.PartialAsync("_PartialName", model)
```


**Razor Pages**

샘플 애플리케이션의 다음 마크업은 `Pages/ArticlesRP/ReadRP.cshtml` 페이지에서 가져온 것입니다. 이 페이지에는 두 개의 부분 뷰가 포함되어 있습니다. 두 번째 부분 뷰는 모델과 `ViewData`를 부분 뷰에 전달합니다. `ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 딕셔너리를 유지하면서 새 `ViewData` 딕셔너리를 전달합니다.

```cshtml
@model ReadRPModel

<h2>@Model.Article.Title</h2>
@* Pass the author's name to Pages\Shared\_AuthorPartialRP.cshtml *@
@await Html.PartialAsync("../Shared/_AuthorPartialRP", Model.Article.AuthorName)
@Model.Article.PublicationDate

@* Loop over the Sections and pass in a section and additional ViewData to 
   the strongly typed Pages\ArticlesRP\_ArticleSectionRP.cshtml partial view. *@
@{
    var index = 0;

    foreach (var section in Model.Article.Sections)
    {
        await Html.PartialAsync("_ArticleSectionRP", 
                                section,
                                new ViewDataDictionary(ViewData)
                                {
                                    { "index", index }
                                });

        index++;
    }
}
```

`Pages/Shared/_AuthorPartialRP.cshtml`은 `ReadRP.cshtml` 마크업 파일에서 참조된 첫 번째 부분 뷰입니다:

```cshtml
@model string
<div>
    <h3>@Model</h3>
    This partial view from /Pages/Shared/_AuthorPartialRP.cshtml.
</div>
```

`Pages/ArticlesRP/_ArticleSectionRP.cshtml`은 `ReadRP.cshtml` 마크업 파일에서 참조된 두 번째 부분 뷰입니다:

```cshtml
@using PartialViewsSample.ViewModels
@model ArticleSection

<h3>@Model.Title Index: @ViewData["index"]</h3>
<div>
    @Model.Content
</div>
```

**MVC**


샘플 애플리케이션의 다음 마크업은 `Views/Articles/Read.cshtml` 뷰를 보여줍니다. 이 뷰에는 두 개의 부분 뷰가 포함되어 있습니다. 두 번째 부분 뷰는 모델과 `ViewData`를 부분 뷰에 전달합니다. `ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 딕셔너리를 유지하면서 새 `ViewData` 딕셔너리를 전달합니다.

```cshtml
@model PartialViewsSample.ViewModels.Article

<h2>@Model.Title</h2>
@* Pass the author's name to Views\Shared\_AuthorPartial.cshtml *@
@await Html.PartialAsync("_AuthorPartial", Model.AuthorName)
@Model.PublicationDate

@* Loop over the Sections and pass in a section and additional ViewData to 
   the strongly typed Views\Articles\_ArticleSection.cshtml partial view. *@
@{
    var index = 0;

    foreach (var section in Model.Sections)
    {
        @(await Html.PartialAsync("_ArticleSection", 
                                section,
                                new ViewDataDictionary(ViewData)
                                {
                                    { "index", index }
                                }))

        index++;
    }
}
```

`Views/Shared/_AuthorPartial.cshtml`은 `Read.cshtml` 마크업 파일에서 참조된 첫 번째 부분 뷰입니다:

```cshtml
@model string
<div>
    <h3>@Model</h3>
    This partial view from /Views/Shared/_AuthorPartial.cshtml.
</div>
```

`Views/Articles/_ArticleSection.cshtml`은 `Read.cshtml` 마크업 파일에서 참조된 두 번째 부분 뷰입니다:

```cshtml
@using PartialViewsSample.ViewModels
@model ArticleSection

<h3>@Model.Title Index: @ViewData["index"]</h3>
<div>
    @Model.Content
</div>
```

런타임에 부분 뷰는 상위 마크업 파일의 렌더링된 출력에 렌더링되며, 이는 공유 `_Layout.cshtml` 내에서 렌더링됩니다. 첫 번째 부분 뷰는 기사 작성자의 이름과 출판 날짜를 렌더링합니다:

> Abraham Lincoln
>
> This partial view from <shared partial view file path>. 11/19/1863 12:00:00 AM

두 번째 부분 뷰는 기사의 섹션을 렌더링합니다:

> Section One Index: 0
>
> Four score and seven years ago ...
>
> Section Two Index: 1
>
> Now we are engaged in a great civil war, testing ...
>
> Section Three Index: 2
>
> But, in a larger sense, we can not dedicate ...

---
## 출처
[Partial views in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/partial?view=aspnetcore-8.0)

---
## [다음](./04_Handle_requests_with_controllers_in_ASP.NET_Core_MVC.md)
