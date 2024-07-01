# Create a web API with ASP.NET Core and MongoDB


## 목차
- [Create a web API with ASP.NET Core and MongoDB](#create-a-web-api-with-aspnet-core-and-mongodb)
  - [목차](#목차)
  - [필수 구성 요소](#필수-구성-요소)
  - [MongoDB 구성](#mongodb-구성)
  - [ASP.NET Core 웹 API 프로젝트 생성](#aspnet-core-웹-api-프로젝트-생성)
  - [엔터티 모델 추가](#엔터티-모델-추가)
  - [구성 모델 추가](#구성-모델-추가)
  - [CRUD 작업 서비스 추가](#crud-작업-서비스-추가)
  - [컨트롤러 추가](#컨트롤러-추가)
  - [웹 API 테스트](#웹-api-테스트)
  - [JSON 직렬화 옵션 구성](#json-직렬화-옵션-구성)
  - [추가 리소스](#추가-리소스)
  - [출처](#출처)

---

이 튜토리얼에서는 [MongoDB](https://www.mongodb.com/what-is-mongodb) NoSQL 데이터베이스에서 CRUD(생성, 읽기, 업데이트, 삭제) 작업을 수행하는 웹 API를 만드는 방법을 설명합니다.

이 튜토리얼에서는 다음을 배우게 됩니다:

> [!div class="checklist"]
> * MongoDB 구성
> * MongoDB 데이터베이스 생성
> * MongoDB 컬렉션 및 스키마 정의
> * 웹 API에서 MongoDB CRUD 작업 수행
> * JSON 직렬화 사용자 지정

## 필수 구성 요소

* [MongoDB 6.0.5 이상](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)
* [MongoDB Shell](https://www.mongodb.com/docs/mongodb-shell/install/)

* [Visual Studio Code](https://code.visualstudio.com/download)
* [Visual Studio Code용 C# (최신 버전)](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
* [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

Visual Studio Code 지침은 프로젝트 생성과 같은 ASP.NET Core 개발 기능을 위해 .NET CLI를 사용합니다. 이 지침은 macOS, Linux 또는 Windows 및 모든 코드 편집기에서 따를 수 있습니다. Visual Studio Code가 아닌 다른 편집기를 사용하는 경우 약간의 변경이 필요할 수 있습니다.

---

## MongoDB 구성

개발 머신(Windows/Linux/macOS)에서 어디에서나 MongoDB 및 MongoDB Shell에 액세스할 수 있도록 설정:

1. MongoDB Shell 다운로드 및 설치:
   * macOS/Linux: MongoDB Shell을 추출할 디렉터리를 선택합니다. `mongosh`의 경로를 `PATH` 환경 변수에 추가합니다.
   * Windows: MongoDB Shell(mongosh.exe)은 *C:\Users\<user>\AppData\Local\Programs\mongosh*에 설치됩니다. `mongosh.exe`의 경로를 `PATH` 환경 변수에 추가합니다.
1. MongoDB 다운로드 및 설치:
   * macOS/Linux: 일반적으로 */usr/local/mongodb*에 설치된 디렉터리를 확인합니다. `mongodb`의 경로를 `PATH` 환경 변수에 추가합니다.
   * Windows: MongoDB는 기본적으로 *C:\\Program Files\MongoDB*에 설치됩니다. *C:\\Program Files\\MongoDB\\Server\\\<version_number>\\bin*을 `PATH` 환경 변수에 추가합니다.
1. 데이터 저장 디렉터리 선택: 데이터 저장을 위한 디렉터리를 선택합니다. 디렉터리가 존재하지 않으면 만듭니다. MongoDB Shell은 새 디렉터리를 만들지 않습니다:
   * macOS/Linux: 예를 들어, `/usr/local/var/mongodb`.
   * Windows: 예를 들어, `C:\\BooksData`.
1. OS 명령 셸(아님 MongoDB Shell)에서 기본 포트 27017에서 MongoDB에 연결하려면 다음 명령을 사용하십시오. 이전 단계에서 선택한 디렉터리로 `<data_directory_path>`를 대체합니다.

   ```console
   mongod --dbpath <data_directory_path>
   ```

이후 단계에서는 이전에 설치한 MongoDB Shell을 사용하여 데이터베이스를 만들고, 컬렉션을 생성하고, 문서를 저장합니다. MongoDB Shell 명령에 대한 자세한 내용은 [`mongosh`](https://docs.mongodb.com/mongodb-shell/run-commands/)를 참조하십시오.

1. `mongosh.exe`를 실행하여 MongoDB 명령 셸 인스턴스를 엽니다.
1. 명령 셸에서 다음 명령을 실행하여 기본 테스트 데이터베이스에 연결합니다:

   ```console
   mongosh
   ```

1. 명령 셸에서 다음 명령을 실행합니다:

   ```console
   use BookStore
   ```

   *BookStore*라는 데이터베이스가 이미 존재하지 않으면 생성됩니다. 데이터베이스가 존재하는 경우, 트랜잭션을 위해 연결이 열립니다.

1. 다음 명령을 사용하여 `Books` 컬렉션을 만듭니다:

   ```console
   db.createCollection('Books')
   ```

   다음 결과가 표시됩니다:

   ```console
   { "ok" : 1 }
   ```

1. 다음 명령을 사용하여 `Books` 컬렉션의 스키마를 정의하고 두 개의 문서를 삽입합니다:

   ```console
   db.Books.insertMany([{ "Name": "Design Patterns", "Price": 54.93, "Category": "Computers", "Author": "Ralph Johnson" }, { "Name": "Clean Code", "Price": 43.15, "Category": "Computers","Author": "Robert C. Martin" }])
   ```

   다음과 유사한 결과가 표시됩니다:

   ```console
   {
       "acknowledged" : true,
       "insertedIds" : [
           ObjectId("61a6058e6c43f32854e51f51"),
           ObjectId("61a6058e6c43f32854e51f52")
        ]
    }
   ```

   > [!NOTE]
   > 이전 결과에 표시된 `ObjectId`는 명령 셸에 표시된 것과 일치하지 않을 수 있습니다.

1. 다음 명령을 사용하여 데이터베이스의 문서를 확인합니다:

   ```console
   db.Books.find().pretty()
   ```

   다음과 유사한 결과가 표시됩니다:

   ```console
   {
        "_id" : ObjectId("61a6058e6c43f32854e51f51"),
        "Name" : "Design Patterns",
        "Price" : 54.93,
        "Category" : "Computers",
        "Author" : "Ralph Johnson"
    }
    {
        "_id" : ObjectId("61a6058e6c43f32854e51f52"),
        "Name" : "Clean Code",
        "Price" : 43.15,
        "Category" : "Computers",
        "Author" : "Robert C. Martin"
    }
   ```

   스키마는 각 문서에 대해 `ObjectId` 유형의 자동 생성된 `_id` 속성을 추가합니다.

## ASP.NET Core 웹 API 프로젝트 생성

1. 명령 셸에서 다음 명령을 실행합니다:

   ```dotnetcli
   dotnet new webapi -o BookStoreApi
   code BookStoreApi
   ```

   앞의 명령은 새 ASP.NET Core 웹 API 프로젝트를 생성한 다음 Visual Studio Code에서 프로젝트를 엽니다.

2. OmniSharp 서버가 시작되면 **필수 빌드 및 디버그 자산이 'BookStoreApi'에서 누락되었습니다. 추가하시겠습니까?**라는 대화 상자가 나타납니다. **예**를 선택합니다.
3. **통합 터미널**을 열고 다음 명령을 실행하여 MongoDB용 .NET 드라이버를 설치합니다:

   ```dotnetcli
   dotnet add package MongoDB.Driver
   ```
---

## 엔터티 모델 추가

1. 프로젝트 루트에 *Models* 디렉터리를 추가합니다.
1. *Models* 디렉터리에 `Book` 클래스를 다음 코드로 추가합니다:

    ```C#
    using MongoDB.Bson;
    using MongoDB.Bson.Serialization.Attributes;

    namespace BookStoreApi.Models;

    public class Book
    {
        [BsonId]
        [BsonRepresentation(BsonType.ObjectId)]
        public string? Id { get; set; }

        [BsonElement("Name")]
        public string BookName { get; set; } = null!;

        public decimal Price { get; set; }

        public string Category { get; set; } = null!;

        public string Author { get; set; } = null!;
    }
    ```

   앞의 클래스에서 `Id` 속성은 다음과 같습니다:

   * CLR(Common Language Runtime) 객체를 MongoDB 컬렉션에 매핑하기 위해 필요합니다.
   * 문서의 기본 키로 이 속성을 만들기 위해 [`[BsonId]`](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Bson_Serialization_Attributes_BsonIdAttribute.htm)로 주석이 추가되었습니다.
   * 매개변수를 [ObjectId](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Bson_ObjectId.htm) 구조 대신 `string` 유형으로 전달할 수 있도록 [`[BsonRepresentation(BsonType.ObjectId)]`](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Bson_Serialization_Attributes_BsonRepresentationAttribute.htm)로 주석이 추가되었습니다. Mongo는 `string`을 `ObjectId`로 변환합니다.

   `BookName` 속성은 [`[BsonElement]`](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Bson_Serialization_Attributes_BsonElementAttribute.htm) 속성으로 주석이 추가되었습니다. 속성의 값인 `Name`은 MongoDB 컬렉션의 속성 이름을 나타냅니다.

## 구성 모델 추가

1. `appsettings.json`에 다음 데이터베이스 구성 값을 추가합니다:

    ```json
    {
        "BookStoreDatabase": {
            "ConnectionString": "mongodb://localhost:27017",
            "DatabaseName": "BookStore",
            "BooksCollectionName": "Books"
        },
        "Logging": {
            "LogLevel": {
                "Default": "Information",
                "Microsoft.AspNetCore": "Warning"
            }
        },
        "AllowedHosts": "*"
    }
    ```

2. *Models* 디렉터리에 `BookStoreDatabaseSettings` 클래스를 다음 코드로 추가합니다:

    ```C#
    namespace BookStoreApi.Models;

    public class BookStoreDatabaseSettings
    {
        public string ConnectionString { get; set; } = null!;

        public string DatabaseName { get; set; } = null!;

        public string BooksCollectionName { get; set; } = null!;
    }
    ```

   앞의 `BookStoreDatabaseSettings` 클래스는 `appsettings.json` 파일의 `BookStoreDatabase` 속성 값을 저장하는 데 사용됩니다. 매핑 과정을 용이하게 하기 위해 JSON 및 C# 속성 이름이 동일하게 지정되었습니다.

3. `Program.cs`에 다음 강조된 코드를 추가합니다:

    ```C#
    var builder = WebApplication.CreateBuilder(args);

    // Add services to the container.
    builder.Services.Configure<BookStoreDatabaseSettings>(
        builder.Configuration.GetSection("BookStoreDatabase"));
    ```

   앞의 코드에서, `appsettings.json` 파일의 `BookStoreDatabase` 섹션이 바인딩된 구성 인스턴스가 종속성 주입(DI) 컨테이너에 등록됩니다. 예를 들어, `BookStoreDatabaseSettings` 객체의 `ConnectionString` 속성은 `appsettings.json`의 `BookStoreDatabase:ConnectionString` 속성으로 채워집니다.

4. `BookStoreDatabaseSettings` 참조를 해결하기 위해 `Program.cs` 상단에 다음 코드를 추가합니다:

    ```C#
    using BookStoreApi.Models;
    ```

## CRUD 작업 서비스 추가

1. 프로젝트 루트에 *Services* 디렉터리를 추가합니다.
2. *Services* 디렉터리에 `BooksService` 클래스를 다음 코드로 추가합니다:

    ```C#
    using BookStoreApi.Models;
    using Microsoft.Extensions.Options;
    using MongoDB.Driver;

    namespace BookStoreApi.Services;

    public class BooksService
    {
        private readonly IMongoCollection<Book> _booksCollection;

        public BooksService(
            IOptions<BookStoreDatabaseSettings> bookStoreDatabaseSettings)
        {
            var mongoClient = new MongoClient(
                bookStoreDatabaseSettings.Value.ConnectionString);

            var mongoDatabase = mongoClient.GetDatabase(
                bookStoreDatabaseSettings.Value.DatabaseName);

            _booksCollection = mongoDatabase.GetCollection<Book>(
                bookStoreDatabaseSettings.Value.BooksCollectionName);
        }

        public async Task<List<Book>> GetAsync() =>
            await _booksCollection.Find(_ => true).ToListAsync();

        public async Task<Book?> GetAsync(string id) =>
            await _booksCollection.Find(x => x.Id == id).FirstOrDefaultAsync();

        public async Task CreateAsync(Book newBook) =>
            await _booksCollection.InsertOneAsync(newBook);

        public async Task UpdateAsync(string id, Book updatedBook) =>
            await _booksCollection.ReplaceOneAsync(x => x.Id == id, updatedBook);

        public async Task RemoveAsync(string id) =>
            await _booksCollection.DeleteOneAsync(x => x.Id == id);
    }
    ```

   앞의 코드에서, `BookStoreDatabaseSettings` 인스턴스는 생성자 주입을 통해 DI에서 검색됩니다. 이 기술을 통해 [구성 모델 추가]섹션에서 추가된 `appsettings.json` 구성 값에 액세스할 수 있습니다.

3. `Program.cs`에 다음 강조된 코드를 추가합니다:

    ```C#
    var builder = WebApplication.CreateBuilder(args);

    // Add services to the container.
    builder.Services.Configure<BookStoreDatabaseSettings>(
        builder.Configuration.GetSection("BookStoreDatabase"));

    builder.Services.AddSingleton<BooksService>();
    ```

   앞의 코드에서, `BooksService` 클래스는 소비 클래스에서 생성자 주입을 지원하기 위해 DI에 등록됩니다. `BooksService`는 `MongoClient`에 직접 의존하므로 단일 서비스 수명이 가장 적합합니다. 공식 [Mongo 클라이언트 재사용 가이드라인](https://mongodb.github.io/mongo-csharp-driver/2.14/reference/driver/connecting/#re-use)에 따르면, `MongoClient`는 단일 서비스 수명으로 DI에 등록되어야 합니다.

4. `BooksService` 참조를 해결하기 위해 `Program.cs` 상단에 다음 코드를 추가합니다:

    ```C#
    using BookStoreApi.Services;
    ```

`BooksService` 클래스는 데이터베이스에 대해 CRUD 작업을 실행하기 위해 다음 `MongoDB.Driver` 멤버를 사용합니다:

* [MongoClient](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Driver_MongoClient.htm): 데이터베이스 작업을 실행하기 위해 서버 인스턴스를 읽습니다. 이 클래스의 생성자는 MongoDB 연결 문자열에서 제공됩니다:

    ```C#
    public BooksService(
        IOptions<BookStoreDatabaseSettings> bookStoreDatabaseSettings)
    {
        var mongoClient = new MongoClient(
            bookStoreDatabaseSettings.Value.ConnectionString);

        var mongoDatabase = mongoClient.GetDatabase(
            bookStoreDatabaseSettings.Value.DatabaseName);

        _booksCollection = mongoDatabase.GetCollection<Book>(
            bookStoreDatabaseSettings.Value.BooksCollectionName);
    }
    ```

* [IMongoDatabase](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Driver_IMongoDatabase.htm): 작업을 실행하기 위해 Mongo 데이터베이스를 나타냅니다. 이 튜토리얼에서는 특정 컬렉션의 데이터에 액세스하기 위해 인터페이스의 일반 [GetCollection\<TDocument>(collection)](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/M_MongoDB_Driver_IMongoDatabase_GetCollection__1.htm) 메서드를 사용합니다. 이 메서드가 호출된 후 컬렉션에 대해 CRUD 작업을 실행합니다. `GetCollection<TDocument>(collection)` 메서드 호출에서:

  * `collection`은 컬렉션 이름을 나타냅니다.
  * `TDocument`는 컬렉션에 저장된 CLR 객체 유형을 나타냅니다.

`GetCollection<TDocument>(collection)`는 컬렉션을 나타내는 [MongoCollection](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/T_MongoDB_Driver_MongoCollection.htm) 객체를 반환합니다. 이 튜토리얼에서는 다음 메서드가 컬렉션에서 호출됩니다:

* [DeleteOneAsync](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/M_MongoDB_Driver_IMongoCollection_1_DeleteOneAsync_1.htm): 제공된 검색 기준과 일치하는 단일 문서를 삭제합니다.
* [Find\<TDocument>](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/M_MongoDB_Driver_IMongoCollectionExtensions_Find__1.htm): 제공된 검색 기준과 일치하는 컬렉션의 모든 문서를 반환합니다.
* [InsertOneAsync](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/M_MongoDB_Driver_IMongoCollection_1_InsertOneAsync_1.htm): 제공된 객체를 새 문서로 컬렉션에 삽입합니다.
* [ReplaceOneAsync](https://mongodb.github.io/mongo-csharp-driver/2.14/apidocs/html/M_MongoDB_Driver_IMongoCollection_1_ReplaceOneAsync.htm): 제공된 검색 기준과 일치하는 단일 문서를 제공된 객체로 교체합니다.

## 컨트롤러 추가

*Controllers* 디렉터리에 `BooksController` 클래스를 다음 코드로 추가합니다:

```C#
using BookStoreApi.Models;
using BookStoreApi.Services;
using Microsoft.AspNetCore.Mvc;

namespace BookStoreApi.Controllers;

[ApiController]
[Route("api/[controller]")]
public class BooksController : ControllerBase
{
    private readonly BooksService _booksService;

    public BooksController(BooksService booksService) =>
        _booksService = booksService;

    [HttpGet]
    public async Task<List<Book>> Get() =>
        await _booksService.GetAsync();

    [HttpGet("{id:length(24)}")]
    public async Task<ActionResult<Book>> Get(string id)
    {
        var book = await _booksService.GetAsync(id);

        if (book is null)
        {
            return NotFound();
        }

        return book;
    }

    [HttpPost]
    public async Task<IActionResult> Post(Book newBook)
    {
        await _booksService.CreateAsync(newBook);

        return CreatedAtAction(nameof(Get), new { id = newBook.Id }, newBook);
    }

    [HttpPut("{id:length(24)}")]
    public async Task<IActionResult> Update(string id, Book updatedBook)
    {
        var book = await _booksService.GetAsync(id);

        if (book is null)
        {
            return NotFound();
        }

        updatedBook.Id = book.Id;

        await _booksService.UpdateAsync(id, updatedBook);

        return NoContent();
    }

    [HttpDelete("{id:length(24)}")]
    public async Task<IActionResult> Delete(string id)
    {
        var book = await _booksService.GetAsync(id);

        if (book is null)
        {
            return NotFound();
        }

        await _booksService.RemoveAsync(id);

        return NoContent();
    }
}
```

앞의 웹 API 컨트롤러는:

* CRUD 작업을 실행하기 위해 `BooksService` 클래스를 사용합니다.
* GET, POST, PUT 및 DELETE HTTP 요청을 지원하는 작업 메서드를 포함합니다.
* `Create` 작업 메서드에서 `CreatedAtAction` 을 호출하여 [HTTP 201](https://www.rfc-editor.org/rfc/rfc9110#status.201) 응답을 반환합니다. 상태 코드 201은 서버에 새 리소스를 생성하는 HTTP POST 메서드의 표준 응답입니다. `CreatedAtAction`은 응답에 `Location` 헤더도 추가합니다. `Location` 헤더는 새로 생성된 책의 URI를 지정합니다.

## 웹 API 테스트

1. 앱을 빌드하고 실행합니다.

1. 앱의 자동 할당된 포트 번호가 `<port>`로 표시된 `https://localhost:<port>/api/books`로 이동하여 컨트롤러의 매개변수 없는 `Get` 작업 메서드를 테스트하고, **Try it out** > **Execute**를 선택합니다. 다음과 유사한 JSON 응답이 표시됩니다:

   ```json
   [
     {
       "id": "61a6058e6c43f32854e51f51",
       "bookName": "Design Patterns",


       "price": 54.93,
       "category": "Computers",
       "author": "Ralph Johnson"
     },
     {
       "id": "61a6058e6c43f32854e51f52",
       "bookName": "Clean Code",
       "price": 43.15,
       "category": "Computers",
       "author": "Robert C. Martin"
     }
   ]
   ```

1. 컨트롤러의 오버로드된 `Get` 작업 메서드를 테스트하기 위해 `https://localhost:<port>/api/books/{id here}`로 이동합니다. 다음과 유사한 JSON 응답이 표시됩니다:

   ```json
   {
     "id": "61a6058e6c43f32854e51f52",
     "bookName": "Clean Code",
     "price": 43.15,
     "category": "Computers",
     "author": "Robert C. Martin"
   }
   ```

## JSON 직렬화 옵션 구성

[웹 API 테스트] 섹션에서 반환된 JSON 응답에 대해 변경해야 할 두 가지 세부 사항이 있습니다:

* 속성 이름의 기본 camel case를 CLR 객체의 속성 이름과 일치하도록 Pascal case로 변경해야 합니다.
* `bookName` 속성은 `Name`으로 반환되어야 합니다.

위의 요구 사항을 충족하려면 다음 변경 사항을 수행하십시오:

1. `Program.cs`에서 `AddControllers` 메서드 호출에 다음 강조된 코드를 체인으로 추가합니다:

    ```C#
    var builder = WebApplication.CreateBuilder(args);

    // Add services to the container.
    builder.Services.Configure<BookStoreDatabaseSettings>(
        builder.Configuration.GetSection("BookStoreDatabase"));

    builder.Services.AddSingleton<BooksService>();

    builder.Services.AddControllers()
        .AddJsonOptions(
            options => options.JsonSerializerOptions.PropertyNamingPolicy = null);
    ```

   위의 변경 사항으로 웹 API의 직렬화된 JSON 응답의 속성 이름이 해당하는 CLR 객체 유형의 속성 이름과 일치합니다. 예를 들어, `Book` 클래스의 `Author` 속성은 `author` 대신 `Author`로 직렬화됩니다.

2. `Models/Book.cs`에서 `BookName` 속성을 [`[JsonPropertyName]`](https://learn.microsoft.com/en-us/dotnet/api/system.text.json.serialization.jsonpropertynameattribute) 속성으로 주석 처리합니다:

    ```C#
    [BsonElement("Name")]
    [JsonPropertyName("Name")]
    public string BookName { get; set; } = null!;
    ```

   `[JsonPropertyName]` 속성의 값인 `Name`은 웹 API의 직렬화된 JSON 응답에서 속성 이름을 나타냅니다.

3. `[JsonProperty]` 속성 참조를 해결하기 위해 `Models/Book.cs` 상단에 다음 코드를 추가합니다:

    ```C#
    using System.Text.Json.Serialization;
    ```

4. [웹 API 테스트] 섹션에 정의된 단계를 반복합니다. JSON 속성 이름의 차이를 확인합니다.

## 추가 리소스

* [샘플 코드 보기 또는 다운로드](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/tutorials/first-mongo-app/samples) ([다운로드 방법](https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-8.0#how-to-download-a-sample))

:::moniker-end

---
## 출처
[Create a web API with ASP.NET Core and MongoDB](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mongo-app?view=aspnetcore-8.0&tabs=visual-studio)


