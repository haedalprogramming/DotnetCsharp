# Part 7, add a new field to a Razor Page in ASP.NET Core

## 목차
- [Part 7, add a new field to a Razor Page in ASP.NET Core](#part-7-add-a-new-field-to-a-razor-page-in-aspnet-core)
  - [목차](#목차)
  - [Movie 모델에 Rating 속성 추가하기](#movie-모델에-rating-속성-추가하기)
    - [rating에 대한 마이그레이션 추가](#rating에-대한-마이그레이션-추가)
    - [선택 사항: 다른 제공자에 대해 데이터베이스 삭제 및 재생성](#선택-사항-다른-제공자에-대해-데이터베이스-삭제-및-재생성)
  - [출처](#출처)
  - [다음](#다음)

---

이 섹션에서는 [Entity Framework](https://learn.microsoft.com/en-us/ef/core/get-started/aspnetcore/new-db) Code First 마이그레이션을 사용하여 다음을 수행합니다:

* 모델에 새 필드를 추가합니다.
* 새 필드 스키마 변경 사항을 데이터베이스에 마이그레이션합니다.

EF Code First를 사용하여 데이터베이스를 자동으로 생성하고 추적할 때, Code First는 다음을 수행합니다:

* 데이터베이스에 [`__EFMigrationsHistory`](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/history-table) 테이블을 추가하여 데이터베이스 스키마가 생성된 모델 클래스와 동기화되어 있는지 추적합니다.
* 모델 클래스가 데이터베이스와 동기화되지 않으면 예외를 던집니다.

스키마와 모델이 동기화되어 있는지 자동으로 확인하면 일관성 없는 데이터베이스 코드 문제를 찾기가 더 쉬워집니다.

## Movie 모델에 Rating 속성 추가하기

1. `Models/Movie.cs` 파일을 열고 `Rating` 속성을 추가합니다:
    ```C#
    public class Movie
    {
        public int Id { get; set; }
        public string Title { get; set; } = string.Empty;

        [Display(Name = "Release Date")]
        [DataType(DataType.Date)]
        public DateTime ReleaseDate { get; set; }
        public string Genre { get; set; } = string.Empty;

        [Column(TypeName = "decimal(18, 2)")]
        public decimal Price { get; set; }
        public string Rating { get; set; } = string.Empty;
    }
    ```
2. `Pages/Movies/Index.cshtml`을 편집하고 `Rating` 필드를 추가합니다:
   <a name="addrat7"></a>
    ```C#
    @page
    @model RazorPagesMovie.Pages.Movies.IndexModel

    @{
        ViewData["Title"] = "Index";
    }

    <h1>Index</h1>

    <p>
        <a asp-page="Create">Create New</a>
    </p>

    <form>
        <p>
            <select asp-for="MovieGenre" asp-items="Model.Genres">
                <option value="">All</option>
            </select>
            Title: <input type="text" asp-for="SearchString" />
            <input type="submit" value="Filter" />
        </p>
    </form>

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
                <th>
                    @Html.DisplayNameFor(model => model.Movie[0].Rating)
                </th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            @foreach (var item in Model.Movie)
            {
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
                        @Html.DisplayFor(modelItem => item.Rating)
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

3. 다음 페이지에 `Rating` 필드를 업데이트합니다:
   * *[Pages/Movies/Create.cshtml](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie80/Pages/Movies/Create.cshtml)*.
   * *[Pages/Movies/Delete.cshtml](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie80/Pages/Movies/Delete.cshtml)*.
   * *[Pages/Movies/Details.cshtml](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie80/Pages/Movies/Details.cshtml)*.
   * *[Pages/Movies/Edit.cshtml](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie80/Pages/Movies/Edit.cshtml)*.

앱은 데이터베이스가 새 필드를 포함하도록 업데이트될 때까지 작동하지 않습니다. 데이터베이스를 업데이트하지 않고 앱을 실행하면 `SqlException`이 발생합니다:

`SqlException: Invalid column name 'Rating'.`

`SqlException` 예외는 업데이트된 Movie 모델 클래스가 데이터베이스의 Movie 테이블 스키마와 다르기 때문에 발생합니다. 데이터베이스 테이블에 `Rating` 열이 없습니다.

오류를 해결하는 몇 가지 접근 방식이 있습니다:

1. Entity Framework가 새 모델 클래스 스키마를 사용하여 데이터베이스를 자동으로 삭제하고 다시 생성하게 합니다. 이 접근 방식은 개발 초기 단계에서 편리하며, 개발자가 모델과 데이터베이스 스키마를 함께 빠르게 발전시킬 수 있게 합니다. 단점은 데이터베이스에 있는 기존 데이터가 손실된다는 것입니다. 이 접근 방식을 프로덕션 데이터베이스에서는 사용하지 마십시오! 스키마 변경 시 데이터베이스를 삭제하고 초기화기를 사용하여 테스트 데이터로 데이터베이스를 자동으로 시드하는 것은 종종 생산적인 방법입니다.
2. 기존 데이터베이스의 스키마를 모델 클래스와 일치하도록 명시적으로 수정합니다. 이 접근 방식의 장점은 데이터를 유지할 수 있다는 것입니다. 이 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 작성하여 수행할 수 있습니다.
3. Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.

이 튜토리얼에서는 Code First 마이그레이션을 사용합니다.

`SeedData` 클래스를 업데이트하여 새 열에 값을 제공합니다. 아래 예제 변경 사항을 참조하십시오. 하지만 각 `new Movie` 블록에 대해 이 변경을 적용하십시오.

```C#
context.Movie.AddRange(
    new Movie
    {
        Title = "When Harry Met Sally",
        ReleaseDate = DateTime.Parse("1989-2-12"),
        Genre = "Romantic Comedy",
        Price = 7.99M,
        Rating = "R"
    },
```

[완성된 SeedData.cs 파일](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie80/Models/SeedDataRating.cs)을 참조하십시오.

앱 빌드

*View* 메뉴에서 *Terminal*을 선택하고 다음 명령을 입력하십시오:

```dotnetcli
dotnet build
```

### rating에 대한 마이그레이션 추가
다음 명령을 사용하여 rating 필드에 대한 마이그레이션을 추가하십시오:

```dotnetcli
dotnet ef migrations add rating
dotnet ef database update
```

`dotnet ef migrations add rating` 명령은 프레임워크에 다음을 지시합니다:

* `Movie` 모델과 `Movie` 데이터베이스 스키마를 비교합니다.
* 데이터베이스 스키마를 새 모델로 마이그레이션하는 코드를 생성합니다.

`rating`이라는 이름은 임의의 것이며 마이그레이션 파일의 이름을 지정하는 데 사용됩니다. 마이그레이션 파일에 의미 있는 이름을 사용하는 것이 좋습니다.

`dotnet ef database update` 명령은 프레임워크에 스키마 변경 사항을 데이터베이스에 적용하고 기존 데이터를 보존하도록 지시합니다.

데이터베이스의 모든 레코드를 삭제하십시오. 초기화기가 데이터베이스를 시드하고 `Rating` 필드를 포함시킵니다.

### 선택 사항: 다른 제공자에 대해 데이터베이스 삭제 및 재생성

데이터베이스를 성공적으로 마이그레이션했다면 이 섹션을 건너뛰십시오.

이 튜토리얼에서는 가능한 경우 Entity Framework Core *마이그레이션* 기능을 사용합니다. 마이그레이션은 데이터 모델의 변경 사항과 일치하도록 데이터베이스 스키마를 업데이트합니다. 그러나 마이그레이션은 EF Core 제공자가 지원하는 종류의 변경만 수행할 수 있으며, 일부 제공자의 기능은 제한적입니다. 예를 들어, 열을 추가하는 것은 지원되지만, 열을 제거하거나 변경하는 것은 지원되지

 않을 수 있습니다. 열을 제거하거나 변경하는 마이그레이션을 생성하면 `ef migrations add` 명령은 성공하지만 `ef database update` 명령은 실패합니다. 이러한 제한으로 인해 데이터베이스를 삭제하고 다시 생성할 수 있습니다.

제한 사항에 대한 해결 방법은 테이블에 변경 사항이 있을 때 테이블 재구성을 수행하는 마이그레이션 코드를 수동으로 작성하는 것입니다. 테이블 재구성에는 다음이 포함됩니다:

* 새 테이블 생성
* 이전 테이블에서 새 테이블로 데이터 복사
* 이전 테이블 삭제
* 새 테이블 이름 변경

자세한 내용은 다음 리소스를 참조하십시오:

 * [SQLite EF Core Database Provider Limitations](https://learn.microsoft.com/en-us/ef/core/providers/sqlite/limitations)
 * [Customize migration code](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/#customize-migration-code)
 * [Data seeding](https://learn.microsoft.com/en-us/ef/core/modeling/data-seeding)
 * [SQLite ALTER TABLE statement](https://sqlite.org/lang_altertable.html)

1. 마이그레이션 폴더를 삭제하십시오.

2. 다음 명령을 사용하여 데이터베이스를 다시 생성하십시오.

   ```dotnetcli
   dotnet ef database drop
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```

---

앱을 실행하고 `Rating` 필드가 있는 영화를 생성, 편집 및 표시할 수 있는지 확인하십시오. 데이터베이스가 시드되지 않으면 `SeedData.Initialize` 메서드에 브레이크 포인트를 설정하십시오.

---
## 출처
[Part 7, add a new field to a Razor Page in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/new-field?view=aspnetcore-8.0&tabs=visual-studio-code)

---
## [다음](./06_10_validation.md)
