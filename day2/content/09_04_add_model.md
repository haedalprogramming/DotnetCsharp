# Part 4, add a model to an ASP.NET Core MVC app

## 목차
- [Part 4, add a model to an ASP.NET Core MVC app](#part-4-add-a-model-to-an-aspnet-core-mvc-app)
  - [목차](#목차)
  - [데이터 모델 클래스 추가](#데이터-모델-클래스-추가)
  - [NuGet 패키지 추가](#nuget-패키지-추가)
  - [영화 페이지 스캐폴딩](#영화-페이지-스캐폴딩)
    - [개발을 위한 SQLite 사용, 프로덕션을 위한 SQL Server 사용](#개발을-위한-sqlite-사용-프로덕션을-위한-sql-server-사용)
  - [초기 마이그레이션](#초기-마이그레이션)
  - [앱 테스트](#앱-테스트)
    - [생성된 데이터베이스 컨텍스트 클래스 및 등록 검사](#생성된-데이터베이스-컨텍스트-클래스-및-등록-검사)
    - [종속성 주입](#종속성-주입)
    - [생성된 데이터베이스 연결 문자열 검사](#생성된-데이터베이스-연결-문자열-검사)
    - [`InitialCreate` 클래스](#initialcreate-클래스)
  - [컨트롤러에서 종속성 주입](#컨트롤러에서-종속성-주입)
  - [강력한 형식의 모델 및 `@model` 지시문](#강력한-형식의-모델-및-model-지시문)
  - [추가 리소스](#추가-리소스)
  - [출처](#출처)
  - [다음](#다음)

---

이 튜토리얼에서는 데이터베이스에서 영화를 관리하기 위한 클래스를 추가합니다. 이 클래스들은 **M**VC 앱의 "**M**odel" 부분을 구성합니다.

이 모델 클래스들은 [Entity Framework Core](https://learn.microsoft.com/en-us/ef/core) (EF Core)를 사용하여 데이터베이스와 작업합니다. EF Core는 데이터 접근 코드를 단순화하는 객체 관계 매핑(ORM) 프레임워크입니다.

생성된 모델 클래스들은 **P**lain **O**ld **C**LR **O**bjects, 즉 ***POCO*** 클래스라고 불립니다. POCO 클래스는 EF Core에 의존하지 않습니다. 이 클래스들은 데이터베이스에 저장될 데이터의 속성만 정의합니다.

이 튜토리얼에서는 모델 클래스를 먼저 생성하고, EF Core가 데이터베이스를 생성합니다.

## 데이터 모델 클래스 추가

**Visual Studio Code**

* *Models* 폴더에 `Movie.cs` 파일을 추가합니다.


`Models/Movie.cs` 파일을 다음 코드로 업데이트합니다:

```C#
using System.ComponentModel.DataAnnotations;

namespace MvcMovie.Models;

public class Movie
{
    public int Id { get; set; }
    public string? Title { get; set; }
    [DataType(DataType.Date)]
    public DateTime ReleaseDate { get; set; }
    public string? Genre { get; set; }
    public decimal Price { get; set; }
}
```

`Movie` 클래스는 기본 키를 위해 데이터베이스에서 필요한 `Id` 필드를 포함합니다.

`ReleaseDate`의 `DataType` 속성은 데이터 유형을 `Date`로 지정합니다. 이 속성을 사용하면:

* 사용자가 날짜 필드에 시간 정보를 입력할 필요가 없습니다.
* 시간 정보 없이 날짜만 표시됩니다.

[DataAnnotations](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations)는 후속 튜토리얼에서 다룹니다.

`string` 뒤의 물음표는 속성이 널(nullable)일 수 있음을 나타냅니다. 자세한 내용은 [널 가능 참조 형식](https://learn.microsoft.com/en-us/dotnet/csharp/nullable-references)을 참조하세요.

## NuGet 패키지 추가

**Visual Studio Code**

다음 .NET CLI 명령을 실행하십시오:

```dotnetcli
dotnet tool uninstall --global dotnet-aspnet-codegenerator
dotnet tool install --global dotnet-aspnet-codegenerator
dotnet tool uninstall --global dotnet-ef
dotnet tool install --global dotnet-ef
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet add package Microsoft.EntityFrameworkCore.SQLite
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools
```

위 명령은 다음을 추가합니다:
* [EF Core를 위한 명령줄 인터페이스(CLI) 도구](https://learn.microsoft.com/en-us/ef/core/miscellaneous/cli/dotnet)
* [aspnet-codegenerator 스캐폴딩 도구](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/tools/dotnet-aspnet-codegenerator?view=aspnetcore-8.0)
* EF Core 디자인 시간 도구
* EF Core 패키지를 종속성으로 설치하는 EF Core SQLite 공급자
* 스캐폴딩에 필요한 패키지: `Microsoft.VisualStudio.Web.CodeGeneration.Design` 및 `Microsoft.EntityFrameworkCore.SqlServer`

환경에 따라 데이터베이스 컨텍스트를 구성할 수 있도록 하는 다중 환경 구성을 위한 지침은 [Use multiple environments in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/environments?view=aspnetcore-8.0#environment-based-startup-class-and-methods)을 참조하십시오.

> [!NOTE]
> 기본적으로 설치할 .NET 바이너리의 아키텍처는 현재 실행 중인 OS 아키텍처를 나타냅니다. 다른 OS 아키텍처를 지정하려면 [dotnet tool install, --arch 옵션](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-tool-install#options)을 참조하십시오.
> 자세한 내용은 GitHub 이슈 [dotnet/AspNetCore.Docs #29262](https://github.com/dotnet/AspNetCore.Docs/issues/29262)를 참조하십시오.

Visual Studio Code에서 <kbd>Ctrl</kbd>+<kbd>F5</kbd> (Windows) 또는 <kbd>⌘</kbd>+<kbd>F5</kbd> (macOS)를 눌러 디버깅 없이 앱을 실행합니다.

편집기 영역 아래의 *Panel*에서 *PROBLEMS* 탭을 선택하거나, *View* 메뉴에서 *Problems*를 선택하여 컴파일 오류가 없는지 확인합니다.

---

## 영화 페이지 스캐폴딩

스캐폴딩 도구를 사용하여 영화 모델에 대한 `생성`, `읽기`, `업데이트`, `삭제` (CRUD) 페이지를 생성합니다.

**Visual Studio Code**

프로젝트 디렉터리에서 명령 창을 엽니다. 프로젝트 디렉터리는 `Program.cs` 및 `.csproj` 파일이 있는 디렉터리입니다.

macOS 및 Linux에서 스캐폴드 도구 경로를 내보냅니다:

```console
export PATH=$HOME/.dotnet/tools:$PATH
```

다음 명령을 실행합니다:

```dotnetcli
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovie.Data.MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries --databaseProvider sqlite
```

다음 표는 ASP.NET Core 코드 생성기 매개변수의 세부 사항을 설명합니다:

| 매개변수                   | 설명|
| ----------------- | ------------ |
| -m  | 모델의 이름입니다. |
| -dc  | 데이터 컨텍스트입니다. |
| --relativeFolderPath | 파일을 생성할 상대 출력 폴더 경로입니다. |
| --useDefaultLayout\|-udl | 뷰에 기본 레이아웃을 사용해야 합니다. |
| --referenceScriptLibraries | Edit 및 Create 페이지에 `_ValidationScriptsPartial`을 추가합니다. |
| --databaseProvider sqlite | `DbContext`가 SQL Server 대신 SQLite를 사용하도록 지정합니다. |

`aspnet-codegenerator controller` 명령어에 대한 도움말을 얻으려면 `h` 스위치를 사용하십시오:

```dotnetcli
dotnet aspnet-codegenerator controller -h
```

자세한 내용은 [dotnet aspnet-codegenerator](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/tools/dotnet-aspnet-codegenerator?view=aspnetcore-8.0)를 참조하십시오.

<a name="scaffolding-created"></a>

스캐폴딩은 다음을 생성합니다:

* 영화 컨트롤러: `Controllers/MoviesController.cs`
* **생성**, **삭제**, **세부 정보**, **편집**, **목록** 페이지에 대한 Razor 뷰 파일: `Views/Movies/*.cshtml`
* 데이터베이스 컨텍스트 클래스: `Data/MvcMovieContext.cs`

스캐폴딩은 다음을 업데이트합니다:

* `Program.cs` 파일에 데이터베이스 컨텍스트를 등록합니다.
* `appsettings.json` 파일에 데이터베이스 연결 문자열을 추가합니다.

이러한 파일 생성 및 파일 업데이트의 자동 생성 과정을 *스캐폴딩*이라고 합니다.

데이터베이스가 존재하지 않기 때문에 스캐폴드된 페이지는 아직 사용할 수 없습니다. 앱을 실행하고 **Movie App** 링크를 선택하면 *데이터베이스를 열 수 없음* 또는 *no such table: Movie* 오류 메시지가 표시됩니다.

오류가 없는지 확인하기 위해 앱을 빌드합니다.

<a name="sqlite-dev-vsc"></a>

### 개발을 위한 SQLite 사용, 프로덕션을 위한 SQL Server 사용

`Program.cs`의 다음 강조된 코드는 개발에서 SQLite를 사용하고 프로덕션에서 SQL Server를 사용하는 방법을 보여줍니다.

```C#
var builder = WebApplication.CreateBuilder(args);

if (builder.Environment.IsDevelopment())
{
    builder.Services.AddDbContext<MvcMovieContext>(options =>
        options.UseSqlite(builder.Configuration.GetConnectionString("MvcMovieContext")));
}
else
{
    builder.Services.AddDbContext<MvcMovieContext>(options =>
        options.UseSqlServer(builder.Configuration.GetConnectionString("ProductionMvcMovieContext")));
}
```

## 초기 마이그레이션

EF Core [마이그레이션](https://learn.microsoft.com/en-us/aspnet/core/data/ef-mvc/migrations?view=aspnetcore-8.0) 기능을 사용하여 데이터베이스를 생성합니다. *마이그레이션*은 데이터 모델과 일치하도록 데이터베이스를 생성하고 업데이트하는 도구 세트입니다.

**Visual Studio Code / Visual Studio for Mac**

다음 .NET CLI 명령을 실행합니다:

```dotnetcli
dotnet ef migrations add InitialCreate
```

```dotnetcli
dotnet ef database update
```

* `ef migrations add InitialCreate`: `Migrations/{timestamp}_InitialCreate.cs` 마이그레이션 파일을 생성합니다. `InitialCreate` 인수는 마이그레이션 이름입니다. 어떤 이름이든 사용할 수 있지만, 일반적으로 마이그레이션을 설명하는 이름을 선택합니다. 이것이 첫 번째 마이그레이션이므로, 생성된 클래스는 데이터베이스 스키마를 생성하는 코드를 포함합니다. 데이터베이스 스키마는 `Data/MvcMovieContext.cs` 파일의 `MvcMovieContext` 클래스에 지정된 모델을 기반으로 합니다.
* `ef database update`: 데이터베이스를 최신 마이그레이션으로 업데이트합니다. 이 명령은 `Migrations/{timestamp}_InitialCreate.cs` 파일의 `Up` 메서드를 실행하여 데이터베이스를 생성합니다.

Microsoft SQL Server 및 SQLite와 같은 여러 공급자를 유지 관리하는 방법에 대한 자세한 내용은 [여러 공급자와 함께하는 마이그레이션](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/providers)을 참조하십시오.

---

<a name="test"></a>

## 앱 테스트

**Visual Studio Code / Visual Studio for Mac**

앱을 실행하고 **Movie App** 링크를 선택합니다.

다음과 같은 예외가 발생하는 경우 마이그레이션 단계에서 `dotnet ef database update` 명령을 놓쳤을 수 있습니다:

```console
SqliteException: SQLite Error 1: 'no such table: Movie'.
```

---

> [!NOTE]
> `Price` 필드에 소수점 쉼표를 입력할 수 없을 수도 있습니다. 소수점으로 쉼표(",")를 사용하는 비영어권 로캘과 비미국 영어 날짜 형식을 위한 [jQuery 유효성 검사](https://jqueryvalidation.org/)를 지원하려면 앱을 글로벌화해야 합니다. 글로벌화 지침은 [이 GitHub 이슈](https://github.com/dotnet/AspNetCore.Docs/issues/4076#issuecomment-326590420)를 참조하십시오.

<a name="dc"></a>

### 생성된 데이터베이스 컨텍스트 클래스 및 등록 검사

EF Core를 사용하면 모델을 사용하여 데이터에 접근합니다. 모델은 엔터티 클래스와 데이터베이스와의 세션을 나타내는 컨텍스트 개체로 구성됩니다. 컨텍스트 개체를 사용하여 데이터를 쿼리하고 저장할 수 있습니다. 데이터베이스 컨텍스트는 [Microsoft.EntityFrameworkCore.DbContext](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext)에서 파생되며 데이터 모델에 포함할 엔터티를 지정합니다.

스캐폴딩은 `Data/MvcMovieContext.cs` 데이터베이스 컨텍스트 클래스를 생성합니다:

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.EntityFrameworkCore;
using MvcMovie.Models;

namespace MvcMovie.Data
{
    public class MvcMovieContext : DbContext
    {
        public MvcMovieContext (DbContextOptions<MvcMovieContext> options)
            : base(options)
        {
        }

        public DbSet<MvcMovie.Models.Movie> Movie { get; set; }
    }
}
```

위 코드는 데이터베이스의 영화를 나타내는 [DbSet\<Movie>](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbset-1) 속성을 생성합니다.

### 종속성 주입

ASP.NET Core는 [종속성 주입(DI)](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)으로 빌드되었습니다. 데이터베이스 컨텍스트와 같은 서비스는 `Program.cs`에서 DI로 등록됩니다. 이러한 서비스는 생성자 매개변수를 통해 필요한 구성 요소에 제공됩니다.

`Controllers/MoviesController.cs` 파일에서 생성자는 [종속성 주입](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 사용하여 `MvcMovieContext` 데이터베이스 컨텍스트를 컨트롤러에 주입합니다. 데이터베이스 컨텍스트는 컨트롤러의 각 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 메서드에서 사용됩니다.

스캐폴딩은 `Program.cs`에 다음 강조된 코드를 생성했습니다:


**Visual Studio Code / Visual Studio for Mac**

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddDbContext<MvcMovieContext>(options =>
    options.UseSqlite(builder.Configuration.GetConnectionString("MvcMovieContext")));
```

---

[ASP.NET Core 구성 시스템](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0)은 "MvcMovieContext" 데이터베이스 연결 문자열을 읽습니다.

<a name="cs"></a>

### 생성된 데이터베이스 연결 문자열 검사

스캐폴딩은 `appsettings.json` 파일에 연결 문자열을 추가했습니다:

**Visual Studio Code / Visual Studio for Mac**

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "MvcMovieContext": "Data Source=MvcMovie.db"
  }
}
```
---

로컬 개발에서는 [ASP.NET Core 구성 시스템](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-8.0)이 `appsettings.json` 파일에서 `ConnectionString` 키를 읽습니다.

### `InitialCreate` 클래스

`Migrations/{timestamp}_InitialCreate.cs` 마이그레이션 파일을 검사합니다:

```C#
using System;
using Microsoft.EntityFrameworkCore.Migrations;

#nullable disable

namespace MvcMovie.Migrations
{
    public partial class InitialCreate : Migration
    {
        protected override void Up(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.CreateTable(
                name: "Movie",
                columns: table => new
                {
                    Id = table.Column<int>(type: "int", nullable: false)
                        .Annotation("SqlServer:Identity", "1, 1"),
                    Title = table.Column<string>(type: "nvarchar(max)", nullable: true),
                    ReleaseDate = table.Column<DateTime>(type: "datetime2", nullable: false),
                    Genre = table.Column<string>(type: "nvarchar(max)", nullable: true),
                    Price = table.Column<decimal>(type: "decimal(18,2)", nullable: false)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_Movie", x => x.Id);
                });
        }

        protected override void Down(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.DropTable(
                name: "Movie");
        }
    }
}
```

위 코드에서:

* `InitialCreate.Up`은 Movie 테이블을 생성하고 `Id`를 기본 키로 설정합니다.
* `InitialCreate.Down`은 `Up` 마이그레이션이 수행한 스키마 변경을 되돌립니다.

## 컨트롤러에서 종속성 주입

`Controllers/MoviesController.cs` 파일을 열고 생성자를 검사합니다:

```C#
public class MoviesController : Controller
{
    private readonly MvcMovieContext _context;

    public MoviesController(MvcMovieContext context)
    {
        _context = context;
    }
```

생성자는 [종속성 주입](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0)을 사용하여 데이터베이스 컨텍스트(`MvcMovieContext`)를 컨트롤러에 주입합니다. 데이터베이스 컨텍스트는 컨트롤러의 각 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 메서드에서 사용됩니다.

**생성** 페이지를 테스트합니다. 데이터를 입력하고 제출합니다.

**편집**, **세부 정보**, **삭제** 페이지를 테스트합니다.

<a name="strongly-typed-models-and-the--keyword"></a>

## 강력한 형식의 모델 및 `@model` 지시문

이 튜토리얼의 앞부분에서 컨트롤러가 `ViewData` 사전을 사용하여 뷰에 데이터를 전달하는 방법을 보았습니다. `ViewData` 사전은 뷰에 정보를 전달하는 편리한 지연 바인딩 방식을 제공하는 동적 개체입니다.

MVC는 강력한 형식의 모델 객체를 뷰에 전달할 수 있는 기능을 제공합니다. 이 강력한 형식 접근 방식은 컴파일 시간 코드 검사를 가능하게 합니다. 스캐폴딩 메커니즘은 `MoviesController` 클래스와 뷰에서 강력한 형식의 모델을 전달했습니다.

`Controllers/MoviesController.cs` 파일의 생성된 `Details` 메서드를 검사합니다:

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

`id` 매개변수는 일반적으로 경로 데이터로 전달됩니다. 예를 들어, `https://localhost:5001/movies/details/1`은 다음을 설정합니다:

* 첫 번째 URL 세그먼트는 컨트롤러를 `movies`로 설정합니다.
* 두 번째 URL 세그먼트는 액션을 `details`로 설정합니다.
* 마지막 URL 세그먼트는 `id`를 1로 설정합니다.

`id`는 다음 예와 같이 쿼리 문자열로 전달될 수도 있습니다:

`https://localhost:5001/movies/details?id=1`

`id` 매개변수는 [nullable 형식](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/nullable-types/index) (`int?`)으로 정의되어 `id` 값이 제공되지 않은 경우를 대비합니다.

`FirstOrDefaultAsync` 메서드에 람다 식을 전달하여 경로 데이터 또는 쿼리 문자열 값과 일치하는 영화 엔터티를 선택합니다.

```csharp
var movie = await _context.Movie
    .FirstOrDefaultAsync(m => m.Id == id);
```

영화를 찾으면 `Movie` 모델의 인스턴스를 `Details` 뷰에 전달합니다:

```csharp
return View(movie);
```

`Views/Movies/Details.cshtml` 파일의 내용을 검사합니다:

```cshtml
@model MvcMovie.Models.Movie

@{
    ViewData["Title"] = "Details";
}

<h1>Details</h1>

<div>
    <h4>Movie</h4>
    <hr />
    <dl class="row">
        <dt class = "col-sm-2">
            @Html.DisplayNameFor(model => model.Title)
        </dt>
        <dd class = "col-sm-10">
            @Html.DisplayFor(model => model.Title)
        </dd>
        <dt class = "col-sm-2">
            @Html.DisplayNameFor(model => model.ReleaseDate)
        </dt>
        <dd class = "col-sm-10">
            @Html.DisplayFor(model => model.ReleaseDate)
        </dd>
        <dt class = "col-sm-2">
            @Html.DisplayNameFor(model => model.Genre)
        </dt>
        <dd class = "col-sm-10">
            @Html.DisplayFor(model => model.Genre)
        </dd>
        <dt class = "col-sm-2">
            @Html.DisplayNameFor(model => model.Price)
        </dt>
        <dd class = "col-sm-10">
            @Html.DisplayFor(model => model.Price)
        </dd>
    </dl>
</div>
<div>
    <a asp-action="Edit" asp-route-id="@Model.Id">Edit</a> |
    <a asp-action="Index">Back to List</a>
</div>
```

뷰 파일 상단의 `@model` 문은 뷰가 예상하는 객체의 유형을 지정합니다. 영화 컨트롤러가 생성될 때, 다음 `@model` 문이 포함되었습니다:

```cshtml
@model MvcMovie.Models.Movie
```

이 `@model` 지시문은 컨트롤러가 뷰에 전달한 영화에 접근할 수 있게 합니다. `Model` 객체는 강력한 형식입니다. 예를 들어, `Details.cshtml` 뷰에서는 `Model` 객체를 사용하여 각 영화 필드를 `DisplayNameFor` 및 `DisplayFor` HTML 도우미에 전달합니다. `Create` 및 `Edit` 메서드와 뷰도 `Movie` 모델 객체를 전달합니다.

영화 컨트롤러의 `Index.cshtml` 뷰와 `Index` 메서드를 검사합니다. `Index` 액션 메서드가 뷰에 전달하는 `Movies` 목록을 생성할 때 `List` 객체를 생성하는 코드를 확인합니다:

```C#
// GET: Movies
public async Task<IActionResult> Index()
{
    return View(await _context.Movie.ToListAsync());
}
```

`Movie` 속성이 null인 경우 코드가 [문제 세부 사항](https://learn.microsoft.com/en-us/aspnet/core/web-api/handle-errors?view=aspnetcore-8.0#problem-details-service)을 반환합니다.

영화 컨트롤러가 생성될 때, 스캐폴딩은 `Index.cshtml` 파일 상단에 다음 `@model` 문을 포함했습니다:

```cshtml
@model IEnumerable<MvcMovie.Models.Movie>
```

이 `@model` 지시문은 컨트롤러가 뷰에 전달한 영화 목록에 접근할 수 있게 합니다. 예를 들어, `Index.cshtml` 뷰에서 `Model` 객체를 사용하여 강력한 형식의 `Model` 객체에 대해 `foreach` 문을 통해 영화를 순회합니다:

```cshtml
@model IEnumerable<MvcMovie.Models.Movie>

@{
    ViewData["Title"] = "Index";
}

<h1>Index</h1>

<p>
    <a asp-action="Create">Create New</a>
</p>
<table class="table">
    <thead>
        <tr>
            <th>
                @Html.DisplayNameFor(model => model.Title)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.ReleaseDate)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Genre)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Price)
            </th>
            <th></th>
        </tr>
    </thead>
    <tbody>
@foreach (var item in Model) {
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
                <a asp-action="Edit" asp-route-id="@item.Id">Edit</a> |
                <a asp-action="Details" asp-route-id="@item.Id">Details</a> |
                <a asp-action="Delete" asp-route-id="@item.Id">Delete</a>
            </td>
        </tr>
}
    </tbody>
</table>
```

`Model` 객체가 `IEnumerable<Movie>` 객체로 강력한 형식으로 지정되었기 때문에 루프의 각 항목은 `Movie` 형식입니다. 이 외에도 컴파일러는 코드에서 사용된 형식을 검증합니다.

## 추가 리소스

* [Entity Framework Core for Beginners](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oXCPdC3fTFA3Z79-eVH3K-s)
* [태그 도우미](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-8.0)
* [글로벌화 및 지역화](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-8.0)

---
## 출처
[Part 4, add a model to an ASP.NET Core MVC app](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-model?view=aspnetcore-8.0&tabs=visual-studio-code)

---
## [다음](./09_05_working_with_sql.md)
