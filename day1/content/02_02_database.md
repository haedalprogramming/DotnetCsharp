# 웹 애플리케이션을 위한 데이터베이스의 역할과 서버와 DB의 연동

## 목차
- [웹 애플리케이션을 위한 데이터베이스의 역할과 서버와 DB의 연동](#웹-애플리케이션을-위한-데이터베이스의-역할과-서버와-db의-연동)
  - [목차](#목차)
  - [소개](#소개)
  - [1. 데이터베이스의 역할](#1-데이터베이스의-역할)
    - [1.1 데이터 저장](#11-데이터-저장)
    - [1.2 데이터 관리](#12-데이터-관리)
    - [1.3 데이터 검색](#13-데이터-검색)
    - [1.4 데이터 보안](#14-데이터-보안)
  - [2. 데이터베이스 종류](#2-데이터베이스-종류)
    - [2.1 관계형 데이터베이스 (RDBMS)](#21-관계형-데이터베이스-rdbms)
    - [2.2 비관계형 데이터베이스 (NoSQL)](#22-비관계형-데이터베이스-nosql)
  - [3. ASP.NET Core와 데이터베이스 연동](#3-aspnet-core와-데이터베이스-연동)
    - [3.1 프로젝트 생성](#31-프로젝트-생성)
    - [3.2 데이터베이스 컨텍스트 설정](#32-데이터베이스-컨텍스트-설정)
      - [`ApplicationDbContext.cs`](#applicationdbcontextcs)
    - [3.3 모델 클래스 작성](#33-모델-클래스-작성)
      - [`Product.cs`](#productcs)
    - [3.4 연결 문자열 설정](#34-연결-문자열-설정)
      - [`appsettings.json`](#appsettingsjson)
    - [3.5 서비스 등록](#35-서비스-등록)
      - [`Startup.cs`](#startupcs)
    - [3.6 마이그레이션 생성 및 데이터베이스 업데이트](#36-마이그레이션-생성-및-데이터베이스-업데이트)
    - [3.7 컨트롤러 작성](#37-컨트롤러-작성)
      - [`ProductsController.cs`](#productscontrollercs)
    - [3.8 테스트](#38-테스트)
  - [4. 결론](#4-결론)
  - [출처](#출처)
  - [다음](#다음)

---

## 소개
데이터베이스는 웹 애플리케이션에서 중요한 역할을 합니다. 이 문서에서는 데이터베이스의 주요 역할과 ASP.NET Core를 사용한 서버와 데이터베이스의 연동 방법을 설명합니다.

## 1. 데이터베이스의 역할

### 1.1 데이터 저장
데이터베이스는 웹 애플리케이션의 데이터를 안전하게 저장합니다.
- **유저 정보**: 로그인 정보, 프로필 등.
- **게시물**: 블로그 게시물, 댓글 등.
- **제품 정보**: 전자 상거래 사이트의 제품 목록 등.

### 1.2 데이터 관리
데이터베이스는 데이터를 효율적으로 관리할 수 있도록 다양한 기능을 제공합니다.
- **CRUD 작업**: 생성(Create), 읽기(Read), 업데이트(Update), 삭제(Delete).
- **트랜잭션**: 여러 작업을 하나의 단위로 처리하여 데이터 일관성을 보장합니다.

### 1.3 데이터 검색
데이터베이스는 효율적인 데이터 검색을 위해 인덱스를 제공합니다.
- **인덱스**: 빠른 데이터 검색을 위한 데이터 구조.
- **쿼리**: 특정 조건에 맞는 데이터를 검색하는 SQL 명령어.

### 1.4 데이터 보안
데이터베이스는 데이터 보안을 위해 다양한 메커니즘을 제공합니다.
- **인증**: 데이터베이스 접근 권한 확인.
- **권한 부여**: 사용자의 권한에 따라 데이터 접근을 제한.
- **암호화**: 민감한 데이터를 암호화하여 저장.

## 2. 데이터베이스 종류

### 2.1 관계형 데이터베이스 (RDBMS)
- **대표적인 예**: MySQL, PostgreSQL, Microsoft SQL Server, Oracle.
- **특징**: 데이터는 테이블 형태로 저장되며, 테이블 간 관계를 정의합니다.
- **SQL 사용**: 데이터를 관리하기 위해 구조적 질의 언어(SQL)를 사용합니다.

### 2.2 비관계형 데이터베이스 (NoSQL)
- **대표적인 예**: MongoDB, Cassandra, Redis.
- **특징**: 테이블 형태가 아닌 다양한 데이터 모델(문서, 그래프, 키-값 등)을 지원합니다.
- **유연성**: 데이터 스키마가 고정되지 않아 유연한 데이터 구조를 가질 수 있습니다.

## 3. ASP.NET Core와 데이터베이스 연동

### 3.1 프로젝트 생성
먼저 ASP.NET Core 프로젝트를 생성합니다.
```bash
dotnet new webapi -o MyApi
cd MyApi
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools
```

### 3.2 데이터베이스 컨텍스트 설정
데이터베이스 컨텍스트 클래스는 데이터베이스와의 세션을 관리합니다.

#### `ApplicationDbContext.cs`
```csharp
using Microsoft.EntityFrameworkCore;

namespace MyApi
{
    public class ApplicationDbContext : DbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        public DbSet<Product> Products { get; set; }
    }
}
```

### 3.3 모델 클래스 작성
모델 클래스는 데이터베이스 테이블을 나타냅니다.

#### `Product.cs`
```csharp
using System.ComponentModel.DataAnnotations;

namespace MyApi
{
    public class Product
    {
        [Key]
        public int Id { get; set; }
        
        [Required]
        [StringLength(100)]
        public string Name { get; set; }
        
        [Required]
        public decimal Price { get; set; }
    }
}
```

### 3.4 연결 문자열 설정
`appsettings.json` 파일에 데이터베이스 연결 문자열을 설정합니다.

#### `appsettings.json`
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=MyApiDb;Trusted_Connection=True;MultipleActiveResultSets=true"
  },
  ...
}
```

### 3.5 서비스 등록
`Startup.cs` 파일에서 데이터베이스 컨텍스트를 서비스로 등록합니다.

#### `Startup.cs`
```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddControllers();
}
```

### 3.6 마이그레이션 생성 및 데이터베이스 업데이트
마이그레이션을 생성하고 데이터베이스를 업데이트합니다.
```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

### 3.7 컨트롤러 작성
컨트롤러는 HTTP 요청을 처리하고, 데이터베이스와 상호작용합니다.

#### `ProductsController.cs`
```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace MyApi.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class ProductsController : ControllerBase
    {
        private readonly ApplicationDbContext _context;

        public ProductsController(ApplicationDbContext context)
        {
            _context = context;
        }

        // GET: /products
        [HttpGet]
        public async Task<ActionResult<IEnumerable<Product>>> GetProducts()
        {
            return await _context.Products.ToListAsync();
        }

        // GET: /products/{id}
        [HttpGet("{id}")]
        public async Task<ActionResult<Product>> GetProduct(int id)
        {
            var product = await _context.Products.FindAsync(id);

            if (product == null)
            {
                return NotFound();
            }

            return product;
        }

        // POST: /products
        [HttpPost]
        public async Task<ActionResult<Product>> PostProduct(Product product)
        {
            _context.Products.Add(product);
            await _context.SaveChangesAsync();

            return CreatedAtAction(nameof(GetProduct), new { id = product.Id }, product);
        }

        // PUT: /products/{id}
        [HttpPut("{id}")]
        public async Task<IActionResult> PutProduct(int id, Product product)
        {
            if (id != product.Id)
            {
                return BadRequest();
            }

            _context.Entry(product).State = EntityState.Modified;

            try
            {
                await _context.SaveChangesAsync();
            }
            catch (DbUpdateConcurrencyException)
            {
                if (!_context.Products.Any(e => e.Id == id))
                {
                    return NotFound();
                }
                else
                {
                    throw;
                }
            }

            return NoContent();
        }

        // DELETE: /products/{id}
        [HttpDelete("{id}")]
        public async Task<IActionResult> DeleteProduct(int id)
        {
            var product = await _context.Products.FindAsync(id);
            if (product == null)
            {
                return NotFound();
            }

            _context.Products.Remove(product);
            await _context.SaveChangesAsync();

            return NoContent();
        }
    }
}
```

### 3.8 테스트
애플리케이션을 실행하고, API 엔드포인트를 테스트합니다.
```bash
dotnet run
```
브라우저 또는 Postman과 같은 도구를 사용하여 API 엔드포인트를 테스트합니다.
- **GET**: `http://localhost:5000/products`
- **POST**: `http://localhost:5000/products`
  ```json
  {
    "name": "Sample Product",
    "price": 9.99
  }
  ```
- **PUT**: `http://localhost:5000/products/{id}`
  ```json
  {
    "id": 1,
    "name": "Updated Product",
    "price": 19.99
  }
  ```
- **DELETE**: `http://localhost:5000/products/{id}`

## 4. 결론
데이터베이스는 웹 애플리케이션의 핵심적인 역할을 담당하며, 데이터를 안전하게 저장하고 관리합니다. ASP.NET Core를 사용하여 데이터베이스와 서버를 연동하는 방법을 이해하면, 강력하고 확장 가능한 웹 애플리케이션을 개발할 수 있습니다. 이 문서를 통해 데이터베이스의 주요 역할과 ASP.NET Core를 활용한 데이터베이스 연동 방법을 학습할 수 있습니다.


## 출처
- [ASP.NET Core 공식 문서](https://docs.microsoft.com/en-us/aspnet/core/)
- [Entity Framework Core 공식 문서](https://docs.microsoft.com/en-us/ef/core/)

---
## [다음](./03_ASP.NET_Core_소개.md)



