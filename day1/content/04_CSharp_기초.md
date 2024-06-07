# C# 기초

## 목차
- [C# 기초](#c-기초)
  - [목차](#목차)
  - [C# 언어 둘러보기](#c-언어-둘러보기)
    - [.NET 아키텍처](#net-아키텍처)
    - [Hello World](#hello-world)
    - [형식 및 변수](#형식-및-변수)
    - [프로그램 구조](#프로그램-구조)
  - [로컬 환경 설정](#로컬-환경-설정)
    - [개발 환경 선택](#개발-환경-선택)
    - [기본 애플리케이션 개발 흐름](#기본-애플리케이션-개발-흐름)
  - [C#에서 정수 및 부동 소수점 숫자를 사용하는 방법](#c에서-정수-및-부동-소수점-숫자를-사용하는-방법)
    - [정수 계산 살펴보기](#정수-계산-살펴보기)
    - [연산 순서 알아보기](#연산-순서-알아보기)
    - [정수 전체 자릿수 및 한도 살펴보기](#정수-전체-자릿수-및-한도-살펴보기)
    - [double 형식 작업](#double-형식-작업)
      - [과제](#과제)
    - [10진 형식으로 작업](#10진-형식으로-작업)
      - [과제](#과제-1)
  - [C# if 문 및 루프 - 조건부 논리 자습서](#c-if-문-및-루프---조건부-논리-자습서)
    - [if 문을 사용하여 결정하기](#if-문을-사용하여-결정하기)
    - [if와 else를 함께 사용하기](#if와-else를-함께-사용하기)
    - [루프를 사용하여 작업 반복](#루프를-사용하여-작업-반복)
    - [for 루프 작업](#for-루프-작업)
    - [중첩 루프 만들기](#중첩-루프-만들기)
    - [분기 및 루프 결합](#분기-및-루프-결합)
  - [C#에서 목록 를 사용하여 데이터 수집을 관리하는 방법 알아보기](#c에서-목록-를-사용하여-데이터-수집을-관리하는-방법-알아보기)
    - [기본 목록 예제](#기본-목록-예제)
    - [목록 콘텐츠 수정](#목록-콘텐츠-수정)
    - [목록 검색 및 정렬](#목록-검색-및-정렬)
    - [다른 형식 목록](#다른-형식-목록)
    - [과제](#과제-2)
  - [C# 프로그램의 일반적인 구조체](#c-프로그램의-일반적인-구조체)
  - [Main()과 명령줄 인수](#main과-명령줄-인수)
    - [개요](#개요)
    - [Main() 반환 값](#main-반환-값)
    - [비동기 Main 반환 값](#비동기-main-반환-값)
    - [명령줄 인수](#명령줄-인수)
  - [최상위 문 - Main 메서드가 없는 프로그램](#최상위-문---main-메서드가-없는-프로그램)
    - [하나의 최상위 파일만](#하나의-최상위-파일만)
    - [다른 진입점 없음](#다른-진입점-없음)
    - [using 지시문](#using-지시문)
    - [전역 네임스페이스](#전역-네임스페이스)
    - [네임스페이스 및 형식 정의](#네임스페이스-및-형식-정의)
    - [args](#args)
    - [await](#await)
    - [프로세스의 종료 코드](#프로세스의-종료-코드)
    - [암시적 진입점 메서드](#암시적-진입점-메서드)
  - [C# 형식 시스템](#c-형식-시스템)
    - [변수 선언에서 형식 지정](#변수-선언에서-형식-지정)
    - [기본 제공 형식](#기본-제공-형식)
    - [사용자 지정 형식](#사용자-지정-형식)
    - [CTS(공용 형식 시스템)](#cts공용-형식-시스템)
    - [값 형식](#값-형식)
    - [참조 형식](#참조-형식)
    - [리터럴 값 형식](#리터럴-값-형식)
    - [제네릭 형식](#제네릭-형식)
    - [암시적 형식, 무명 형식 및 nullable 값 형식](#암시적-형식-무명-형식-및-nullable-값-형식)
    - [컴파일 시간 형식 및 런타임 형식](#컴파일-시간-형식-및-런타임-형식)
  - [형식을 구성하도록 네임스페이스 선언](#형식을-구성하도록-네임스페이스-선언)
    - [네임스페이스 개요](#네임스페이스-개요)
  - [클래스 소개](#클래스-소개)
    - [참조 형식](#참조-형식-1)
    - [클래스 선언](#클래스-선언)
    - [개체 만들기](#개체-만들기)
    - [생성자 및 초기화](#생성자-및-초기화)
  - [클래스 상속](#클래스-상속)
  - [C#의 레코드 형식 소개](#c의-레코드-형식-소개)
    - [레코드를 사용하는 경우](#레코드를-사용하는-경우)
      - [값 같음](#값-같음)
      - [불변성](#불변성)
    - [레코드가 클래스 및 구조체와 다른 방식](#레코드가-클래스-및-구조체와-다른-방식)
    - [예제](#예제)
  - [인터페이스 - 여러 형식에 대한 동작 정의](#인터페이스---여러-형식에-대한-동작-정의)
    - [인터페이스 요약](#인터페이스-요약)
  - [제네릭 클래스 및 메서드](#제네릭-클래스-및-메서드)
    - [제네릭 개요](#제네릭-개요)
  - [무명 형식](#무명-형식)
  - [C#의 클래스, 구조체 및 레코드 개요](#c의-클래스-구조체-및-레코드-개요)
    - [캡슐화](#캡슐화)
    - [멤버](#멤버)
    - [접근성](#접근성)
    - [상속](#상속)
    - [인터페이스](#인터페이스)
    - [제네릭 형식](#제네릭-형식-1)
    - [정적 형식](#정적-형식)
    - [중첩 형식](#중첩-형식)
    - [부분 형식(Partial Type)](#부분-형식partial-type)
    - [개체 이니셜라이저](#개체-이니셜라이저)
    - [익명 형식](#익명-형식)
    - [확장명 메서드](#확장명-메서드)
    - [암시적 형식 지역 변수](#암시적-형식-지역-변수)
    - [레코드](#레코드)
  - [개체 - 형식의 인스턴스 만들기](#개체---형식의-인스턴스-만들기)
    - [구조체 인스턴스 및 클래스 인스턴스](#구조체-인스턴스-및-클래스-인스턴스)
    - [개체 ID와 값 같음 비교](#개체-id와-값-같음-비교)
  - [상속 - 형식을 파생하여 보다 전문화된 동작을 만듭니다.](#상속---형식을-파생하여-보다-전문화된-동작을-만듭니다)
    - [추상 메서드와 가상 메서드](#추상-메서드와-가상-메서드)
    - [추상 기본 클래스](#추상-기본-클래스)
    - [인터페이스](#인터페이스-1)
    - [추가 파생 방지](#추가-파생-방지)
    - [파생 클래스의 기본 클래스 멤버 숨기기](#파생-클래스의-기본-클래스-멤버-숨기기)
  - [다형성](#다형성)
    - [다형성 개요](#다형성-개요)
      - [가상 멤버](#가상-멤버)
      - [새 멤버로 기본 클래스 멤버 숨기기](#새-멤버로-기본-클래스-멤버-숨기기)
      - [파생 클래스가 가상 멤버를 재정의하지 못하도록 설정](#파생-클래스가-가상-멤버를-재정의하지-못하도록-설정)
      - [파생 클래스에서 기본 클래스 가상 멤버에 액세스](#파생-클래스에서-기본-클래스-가상-멤버에-액세스)
  - [패턴 일치 개요](#패턴-일치-개요)
    - [null 검사](#null-검사)
    - [형식 테스트](#형식-테스트)
    - [불연속 값 비교](#불연속-값-비교)
    - [관계형 패턴](#관계형-패턴)
    - [여러 입력](#여러-입력)
    - [목록 패턴](#목록-패턴)
  - [무시 항목 - C# 기본 사항](#무시-항목---c-기본-사항)
    - [튜플 및 개체 분해](#튜플-및-개체-분해)
    - [switch를 사용한 패턴 일치](#switch를-사용한-패턴-일치)
    - [out 매개 변수를 사용한 메서드 호출](#out-매개-변수를-사용한-메서드-호출)
    - [독립 실행형 무시 항목](#독립-실행형-무시-항목)
  - [튜플 및 기타 형식 분해](#튜플-및-기타-형식-분해)
    - [튜플](#튜플)
    - [무시 항목이 있는 튜플 요소](#무시-항목이-있는-튜플-요소)
    - [사용자 정의 형식](#사용자-정의-형식)
    - [무시 항목이 포함된 사용자 정의 형식](#무시-항목이-포함된-사용자-정의-형식)
    - [사용자 정의 형식의 확장 메서드](#사용자-정의-형식의-확장-메서드)
    - [시스템 형식의 확장 메서드](#시스템-형식의-확장-메서드)
    - [record 형식](#record-형식)
  - [예외 및 예외 처리](#예외-및-예외-처리)
    - [예외 개요](#예외-개요)
  - [예외 사용](#예외-사용)
  - [예외 처리(C# 프로그래밍 가이드)](#예외-처리c-프로그래밍-가이드)
    - [catch 블록](#catch-블록)
    - [Finally 블록](#finally-블록)
  - [예외 만들기 및 throw](#예외-만들기-및-throw)
    - [예외를 throw할 때 피해야 하는 작업](#예외를-throw할-때-피해야-하는-작업)
    - [작업 반환 메서드의 예외](#작업-반환-메서드의-예외)
    - [예외 클래스 정의](#예외-클래스-정의)
  - [컴파일러 생성 예외](#컴파일러-생성-예외)
  - [C# 식별자 명명 규칙 및 규칙](#c-식별자-명명-규칙-및-규칙)
    - [이름 지정 규칙](#이름-지정-규칙)
    - [명명 규칙](#명명-규칙)
    - [파스칼식 대/소문자](#파스칼식-대소문자)
    - [카멜식 대/소문자](#카멜식-대소문자)
    - [형식 매개 변수 명명 지침](#형식-매개-변수-명명-지침)
    - [추가 명명 규칙](#추가-명명-규칙)
  - [Common C# code conventions](#common-c-code-conventions)
    - [Tools and analyzers](#tools-and-analyzers)
      - [Diagnostic IDs](#diagnostic-ids)
    - [Language guidelines](#language-guidelines)
      - [String data](#string-data)
      - [Arrays](#arrays)
      - [Delegates](#delegates)
      - [`try-catch` and `using` statements in exception handling](#try-catch-and-using-statements-in-exception-handling)
      - [`&&` and `||` operators](#-and--operators)
      - [`new` operator](#new-operator)
      - [Event handling](#event-handling)
      - [Static members](#static-members)
      - [LINQ queries](#linq-queries)
      - [Implicitly typed local variables](#implicitly-typed-local-variables)
      - [Place the using directives outside the namespace declaration](#place-the-using-directives-outside-the-namespace-declaration)
    - [Style guidelines](#style-guidelines)
      - [Comment style](#comment-style)
      - [Layout conventions](#layout-conventions)
  - [How to display command-line arguments](#how-to-display-command-line-arguments)
    - [Example](#example)
  - [Explore object oriented programming with classes and objects](#explore-object-oriented-programming-with-classes-and-objects)
    - [Create your application](#create-your-application)
    - [Define the bank account type](#define-the-bank-account-type)
    - [Open a new account](#open-a-new-account)
    - [Create deposits and withdrawals](#create-deposits-and-withdrawals)
    - [Challenge - log all transactions](#challenge---log-all-transactions)
  - [Object-Oriented programming (C#)](#object-oriented-programming-c)
  - [출처](#출처)
  - [다음](#다음)

---
## C# 언어 둘러보기

C#(“씨샵”이라고 발음합니다.)은 형식이 안전한 최신 개체 지향 프로그래밍 언어입니다. 개발자는 C#을 사용하면 .NET에서 실행되는 다양한 형식의 안전하고 강력한 애플리케이션을 빌드할 수 있습니다. C#은 C 언어 제품군에서 시작되었으며 C, C++, Java 및 JavaScript 프로그래머에게 친숙할 것입니다. 이 둘러보기에서는 C# 8 이상 언어의 주요 구성 요소를 간략하게 설명합니다. 대화형 예제를 통해 언어를 살펴보려면 C# 소개 자습서를 사용해 보세요.

C#은 개체 지향 구성 요소 지향 프로그래밍 언어입니다. C#은 이러한 개념을 직접적으로 지원하는 언어 구문을 제공함으로써 소프트웨어 구성 요소를 만들고 사용할 수 있는 자연 언어로 자리매김하게 되었습니다. 원본 이후로 C#은 새로운 워크로드를 지원하기 위한 기능 및 새로운 소프트웨어 디자인 사례를 추가했습니다. 핵심 C#은 개체 지향 언어입니다 . 형식 및 해당 동작을 정의합니다.

여러 가지 C# 기능은 강력한 지속형 애플리케이션을 만드는 데 도움이 됩니다. 가비지 수집 은 연결할 수 없는 사용되지 않는 개체가 차지하는 메모리를 자동으로 회수합니다. ‘Nullable 형식’은 할당된 개체를 참조하지 않는 변수로부터 보호합니다. ‘예외 처리’는 오류 검색 및 복구에 대한 구조적이고 확장 가능한 방법을 제공합니다. ‘람다 식’은 함수형 프로그래밍 기술을 지원합니다. ‘LINQ(언어 통합 쿼리)’ 구문은 모든 소스의 데이터로 작업하기 위한 일반적인 패턴을 만듭니다. ‘비동기 작업’에 대한 언어 지원은 분산 시스템을 빌드하기 위한 구문을 제공합니다. C#에는 통합 형식 시스템이 있습니다. int 및 double과 같은 기본 형식을 포함하는 모든 C# 형식은 단일 루트 object에서 상속됩니다. 모든 형식은 일반 작업 집합을 공유합니다. 모든 형식의 값을 일관된 방식으로 저장 및 전송하고 작업을 수행할 수 있습니다. 또한 C#은 사용자 정의 참조 형식 및 값 형식을 모두 지원합니다. C#은 개체의 동적 할당 및 경량 구조체의 인라인 스토리지를 허용합니다. C#은 향상된 형식 안전성과 성능을 제공하는 제네릭 메서드 및 형식을 지원합니다. C#은 컬렉션 클래스의 구현자가 클라이언트 코드에 대한 사용자 지정 동작을 정의하는 데 사용할 수 있는 반복기를 제공합니다.

C#은 버전 관리를 강조하여 프로그램 및 라이브러리가 호환되는 방식으로 시간이 지남에 따라 발전할 수 있도록 합니다. 버전 관리 고려 사항의 직접적인 영향을 받은 C# 설계의 측면에는 별도의 virtual 및 override 한정자, 메서드 오버로드 확인 규칙 및 명시적 인터페이스 멤버 선언에 대한 지원이 포함됩니다.

### .NET 아키텍처

C# 프로그램은 CLR(공용 언어 런타임)이라는 가상 실행 시스템이며 클래스 라이브러리 세트인 .NET에서 실행됩니다. CLR은 국제 표준인 CLI(공용 언어 인프라)를 Microsoft에서 구현한 것입니다. CLI는 언어와 라이브러리가 원활하게 함께 작동하는 실행 및 개발 환경을 만들기 위한 기초입니다.

C#으로 작성된 소스 코드는 CLI 사양을 준수하는 IL(중간 언어)로 컴파일됩니다. IL 코드와 리소스(예: 비트맵 및 문자열)는 일반적으로 .dll 확장명과 함께 어셈블리에 저장됩니다. 어셈블리는 어셈블리의 형식, 버전 및 문화에 대한 정보를 제공하는 매니페스트를 포함합니다.

C# 프로그램이 실행되면 어셈블리가 CLR에 로드됩니다. CLR은 JIT(Just-In-Time) 컴파일을 수행하여 IL 코드를 네이티브 기계어 명령으로 변환합니다. CLR은 자동 가비지 수집, 예외 처리 및 리소스 관리와 관련된 다른 서비스도 제공합니다. CLR에서 실행되는 코드를 "관리 코드"라고도 합니다. "관리되지 않는 코드"는 특정 플랫폼을 대상으로 하는 네이티브 머신 언어로 컴파일됩니다.

언어 상호 운용성은 .NET의 주요 기능입니다. C# 컴파일러에서 생성된 IL 코드는 CTS(공용 형식 사양)를 따릅니다. C#에서 생성된 IL 코드는 F#, Visual Basic, C++의 .NET 버전에서 생성된 코드와 상호 작용할 수 있습니다. 다른 CTS 규격 언어가 20개 이상 있습니다. 단일 어셈블리는 다른 .NET 언어로 작성된 여러 모듈을 포함할 수 있습니다. 형식은 같은 언어로 작성된 것처럼 서로를 참조할 수 있습니다.

런타임 서비스 외에도 .NET에는 광범위한 라이브러리가 포함되어 있습니다. 이러한 라이브러리는 다양한 워크로드를 지원합니다. 다양한 유용한 기능을 제공하는 네임스페이스로 구성됩니다. 이 라이브러리는 파일 입력 및 출력부터 문자열 조작, XML 구문 분석, 웹 애플리케이션 프레임워크, Windows Forms 컨트롤에 이르기까지의 모든 기능을 포함합니다. 전형적인 C# 애플리케이션은 .NET 클래스 라이브러리를 광범위하게 사용하여 일반적인 “배관” 작업을 처리합니다.

.NET에 대한 자세한 내용은 .NET의 개요를 참조하세요.

### Hello World
“Hello, World” 프로그램은 프로그래밍 언어를 소개하는 데 일반적으로 사용됩니다. C#에서는 다음과 같습니다.
```C#
using System;

class Hello
{
    static void Main()
    {
        Console.WriteLine("Hello, World");
    }
}
```
“Hello, World” 프로그램은 System 네임스페이스를 참조하는 using 지시문으로 시작합니다. 네임스페이스는 계층적으로 C# 프로그램 및 라이브러리를 구성하는 방법을 제공합니다. 네임스페이스에는 형식 및 다른 네임스페이스가 포함됩니다. 예를 들어 System 네임스페이스에는 많은 형식(예: 프로그램에 참조되는 Console 클래스) 및 많은 다른 네임스페이스(예: IO 및 Collections)가 포함되어 있습니다. 지정된 네임스페이스를 참조하는 using 지시문을 사용하여 해당 네임스페이스의 멤버인 형식을 정규화되지 않은 방식으로 사용할 수 있습니다. using 지시문 때문에, 프로그램은 Console.WriteLine을 System.Console.WriteLine의 약식으로 사용할 수 있습니다.

“Hello, World” 프로그램에서 선언된 Hello 클래스에는 단일 멤버인 Main 메서드가 있습니다. Main 메서드는 static 한정자로 선언됩니다. 인스턴스 메서드는 키워드 this를 사용하여 특정 바깥쪽 개체 인스턴스를 참조할 수 있지만 정적 메서드는 특정 개체에 대한 참조 없이 작동합니다. 관례상 Main이라는 정적 메서드가 C# 프로그램의 진입점으로 사용됩니다.

프로그램의 출력은 System 네임스페이스에 있는 Console 클래스의 WriteLine 메서드에 의해 생성됩니다. 이 클래스는 기본적으로는 컴파일러에서 자동으로 참조되는 표준 클래스 라이브러리를 통해 제공됩니다.

### 형식 및 변수

형식은 C# 내 모든 데이터의 구조와 동작을 정의합니다. 형식 선언에는 해당 멤버, 기본 형식, 구현하는 인터페이스 및 해당 형식에 허용되는 작업이 포함될 수 있습니다. 변수는 특정 형식의 인스턴스를 참조하는 레이블입니다.

C#에는 두 가지 종류의 형식, 즉 값 형식과 참조 형식이 있습니다. 값 형식의 변수에는 해당 데이터가 직접 포함됩니다. 참조 형식의 변수에는 개체라고도 하는 데이터에 대한 참조가 저장됩니다. 참조 형식에서는 두 개의 변수가 같은 개체를 참조할 수 있고 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다. 값 형식에서는 변수가 자체적으로 데이터 사본을 갖고 있으며 한 변수에 대한 작업이 다른 변수에 영향을 미칠 수 없습니다(ref 및 out 매개 변수 변수 제외).

식별자는 변수 이름입니다. 식별자는 공백이 없는 유니코드 문자 시퀀스입니다. 식별자에 @ 접두사가 있으면 C# 예약어일 수 있습니다. 예약어를 식별자로 사용하면 다른 언어와 상호 작용할 때 유용할 수 있습니다.

C#의 값 형식은 ‘단순 형식’, ‘열거형 형식’, ‘구조체 형식’, ‘null 허용 값 형식’, ‘튜플 값 형식’으로 세분화됩니다. C#의 참조 형식은 클래스 형식, 인터페이스 형식, 배열 형식 및 대리자 형식으로 세분화됩니다.

다음 개요는 C#의 형식 시스템에 대한 개요를 제공합니다.

 - 값 형식
     - 단순 형식
         - 부호 있는 정수: sbyte, short, int, long
         - 부호 없는 정수: byte, ushort, uint, ulong
         - 유니코드 문자: char(UTF-16 코드 단위)
         - IEEE 이진 부동 소수점: float, double
         - 고정밀 10진수 부동 소수점: decimal
         - 부울: bool은 부울 값, 즉 true 또는 false를 나타내는 값입니다.
     - 열거형 형식
         - enum E {...}의 사용자 정의 형식입니다. enum 형식은 명명된 상수가 있는 고유한 형식입니다. 모든 enum 형식은 8가지 정수 형식 중 하나인 내부 형식을 갖습니다. enum 형식의 값 집합은 내부 형식의 값 집합과 동일합니다.
     - 구조체 형식
         - struct S {...} 양식의 사용자 정의 형식
     - Nullable 값 형식
         - null 값을 갖는 다른 모든 값 형식의 확장
     - 튜플 값 형식
         - (T1, T2, ...) 양식의 사용자 정의 형식
 - 참조 형식
     - 클래스 형식
         - 다른 모든 형식의 기본 클래스: object
         - 유니코드 문자열: string(UTF-16 코드 유닛 시퀀스)
         - class C {...} 양식의 사용자 정의 형식
     - 인터페이스 형식
         - interface I {...} 양식의 사용자 정의 형식
     - 배열 형식
         - 1차원 배열, 다차원 배열, 가변 배열. 예: int[], int[,], int[][]
     - 대리자 형식
         - delegate int D(...) 양식의 사용자 정의 형식

C# 프로그램에서는 형식 선언을 사용하여 새 형식을 만듭니다. 형식 선언은 새 형식의 이름과 멤버를 지정합니다. 사용자 정의가 가능한 C#의 6가지 형식 범주는 클래스 형식, 구조체 형식, 인터페이스 형식, 열거형 형식, 대리자 형식, 튜플 값 형식입니다. record 형식, record struct 또는 record class를 선언할 수도 있습니다. 레코드 형식에는 컴파일러 합성 멤버가 포함됩니다. 레코드는 주로 연결된 동작을 최소화하면서 값을 저장하는 데 사용합니다.

 - class 형식은 데이터 멤버(필드) 및 함수 멤버(메서드, 속성 및 기타)를 포함하는 데이터 구조를 정의합니다. 클래스 형식은 단일 상속 및 다형성과 파생된 클래스가 기본 클래스를 확장하고 특수화할 수 있는 메커니즘을 지원합니다.
 - struct 형식은 데이터 멤버 및 함수 멤버로 구조체를 나타내는 클래스 형식과 유사합니다. 그러나 클래스와 달리 구조체는 값 형식이며 일반적으로 힙 할당이 필요하지 않습니다. 구조체 형식은 사용자 지정 상속을 지원하지 않으며 모든 구조체 형식은 object 형식으로부터 암시적으로 상속됩니다.
 - interface 형식은 계약을 공용 멤버의 명명된 집합으로 정의합니다. interface를 구현하는 class 또는 struct는 인터페이스의 멤버 구현을 제공해야 합니다. interface는 여러 기본 인터페이스에서 상속될 수 있으며 class 또는 struct는 여러 인터페이스를 구현할 수 있습니다.
 - delegate 형식은 특정 매개 변수 목록 및 반환 형식이 있는 메서드에 대한 참조를 나타내는 형식입니다. 대리자는 메서드를 변수에 할당되고 매개 변수로 전달될 수 있는 엔터티로 취급할 수 있도록 합니다. 대리자는 함수 언어에서 제공하는 함수 형식과 유사합니다. 대리자는 다른 언어의 함수 포인터와 개념이 비슷하지만 함수 포인터와 달리 대리자는 개체 지향적이며 형식이 안전한 방식입니다.

class, struct, interface 및 delegate 형식은 모두 제네릭을 지원하므로 다른 형식으로 매개 변수화할 수 있습니다.

C#은 모든 형식의 1차원 및 다차원 배열을 지원합니다. 위에 나열된 형식과 달리, 배열 형식은 사용하기 전에 먼저 선언할 필요가 없습니다. 대신, 배열 형식은 형식 이름을 대괄호로 묶어 생성합니다. 예를 들어 int[]는int의 1차원 배열이고, int[,]는 int의 2차원 배열, int[][]는 int의 1차원 배열의 1차원 배열, 즉 "가변" 배열입니다.

nullable 형식에는 별도의 정의가 필요하지 않습니다. null을 허용하지 않는 형식 T의 경우, 대응되는 nullable 형식 T?가 있으며 이는 추가 값 null을 가질 수 있습니다. 예를 들어 int?는 32비트 정수 또는 null 값을 보유할 수 있는 형식이고, string?은 모든 string 또는 null 값을 보유할 수 있는 형식입니다.

C#의 형식 시스템은 모든 형식의 값이 object로 취급될 수 있도록 통합됩니다. C#의 모든 형식은 object 클래스 형식에서 직접 또는 간접적으로 파생되고 object는 모든 형식의 기본 클래스입니다. 참조 형식의 값은 object로 인식함으로써 간단히 개체로 처리됩니다. 값 형식의 값은 boxing 및 unboxing 작업을 수행하여 개체로 처리됩니다. 다음 예제에서 int 값은 object로 변환되었다가 다시 int로 변환됩니다.

```c#
int i = 123;
object o = i;    // Boxing
int j = (int)o;  // Unboxing
```

값 형식의 값이 object 참조에 할당되면 값을 보유하기 위해 "box"가 할당됩니다. 이 상자는 참조 형식의 인스턴스이며 해당 상자에 값이 복사됩니다. 반대로 object 참조가 값 형식으로 캐스트될 때 참조된 object가 올바른 값 형식의 상자인지 확인합니다. 확인에 성공하면 상자의 값이 값 형식에 복사됩니다.

C#의 통합 형식 시스템은 값 형식이 "주문형" 참조로 object 처리됨을 효과적으로 의미합니다. 통합으로 인해 형식을 사용하는 범용 라이브러리는 참조 형식 object 과 값 형식을 모두 포함하여 에서 object파생되는 모든 형식과 함께 사용할 수 있습니다.

C#에는 필드, 배열 요소, 지역 변수 및 매개 변수를 포함하는 여러 종류의 변수가 있습니다. 변수는 저장소 위치를 나타냅니다. 모든 변수에는 아래와 같이 해당 변수에 저장할 수 있는 값을 결정하는 유형이 있습니다.

 - Null을 허용하지 않는 값 형식
     - 정확한 해당 형식의 값
 - Null 허용 값 형식
     - null 값 또는 정확한 해당 형식의 값
 - object
     - null 참조, 참조 형식의 개체에 대한 참조 또는 값 형식의 boxed 값에 대한 참조
 - 클래스 형식
     - null 참조, 해당 클래스 형식의 인스턴스에 대한 참조 또는 해당 클래스 형식에서 파생된 클래스의 인스턴스에 대한 참조
 - 인터페이스 유형
     - null 참조, 해당 인터페이스 형식을 구현하는 클래스 형식의 인스턴스에 대한 참조 또는 해당 인터페이스 형식을 구현하는 값 형식의 boxed 값에 대한 참조
 - 배열 형식
     - null 참조, 해당 배열 형식의 인스턴스에 대한 참조 또는 호환되는 배열 형식의 인스턴스에 대한 참조
 - 대리자 형식
     - null 참조 또는 호환되는 대리자 형식의 인스턴스에 대한 참조


### 프로그램 구조

C#의 주요 조직 개념은 프로그램, 네임스페이스, 형식, 멤버 및 어셈블리입니다. 프로그램은 멤버를 포함하고 네임스페이스로 구성될 수 있는 형식을 선언합니다. 클래스, 구조체 및 인터페이스는 형식의 예입니다. 필드, 메서드, 속성 및 이벤트는 멤버의 예입니다. C# 프로그램을 컴파일하면 실제로 어셈블리로 패키지됩니다. 어셈블리는 일반적으로 애플리케이션 또는 .dll라이브러리를 각각 구현하는지에 따라 파일 확장명.exe 또는 를 갖습니다.

간단한 예로, 다음 코드를 포함하는 어셈블리를 생각해 보세요.

```C#
namespace Acme.Collections;

public class Stack<T>
{
    Entry _top;

    public void Push(T data)
    {
        _top = new Entry(_top, data);
    }

    public T Pop()
    {
        if (_top == null)
        {
            throw new InvalidOperationException();
        }
        T result = _top.Data;
        _top = _top.Next;

        return result;
    }

    class Entry
    {
        public Entry Next { get; set; }
        public T Data { get; set; }

        public Entry(Entry next, T data)
        {
            Next = next;
            Data = data;
        }
    }
}
```

이 클래스의 정규화된 이름은 Acme.Collections.Stack입니다. 클래스에는 필드 _top, 2개의 메서드 Push 및 Pop, 중첩된 클래스 Entry 등의 여러 멤버가 포함됩니다. Entry 클래스에는 Next 속성, Data 속성, 생성자, 이렇게 세 멤버가 더 포함됩니다. Stack은 제네릭 클래스입니다. 이는 사용 시 구체적인 형식으로 대체되는 T 형식 매개 변수 하나를 포함합니다.

스택은 "FILO"(선입후출) 컬렉션입니다. 스택의 맨 위에 새 요소가 추가됩니다. 요소가 제거되면 스택의 맨 위에서 제거됩니다. 이전 예제는 스택의 스토리지 및 동작을 정의하는 Stack 형식을 선언합니다. 해당 기능을 사용하기 위해 Stack 형식의 인스턴스를 참조하는 변수를 선언할 수 있습니다.

어셈블리에는 IL(중간 언어) 명령 형식의 실행 코드와 메타데이터 형식의 기호 정보가 포함됩니다. 어셈블리가 실행되기 전에, .NET 공용 언어 런타임의 JIT(Just-In-Time) 컴파일러가 어셈블리 안의 IL 코드를 해당 프로세서에 맞는 코드로 변환합니다.

어셈블리는 코드와 메타데이터를 모두 포함하는 기능의 자체 설명 단위이므로 C#에서는 #include 지시문과 헤더 파일이 필요하지 않습니다. 특정 어셈블리에 포함된 공용 형식 및 멤버는 프로그램을 컴파일할 때 해당 어셈블리를 참조하는 것만으로 C# 프로그램에서 사용 가능해집니다. 예를 들어 이 프로그램에서는 acme.dll 어셈블리의 Acme.Collections.Stack 클래스를 사용합니다.

```C#
class Example
{
    public static void Main()
    {
        var s = new Acme.Collections.Stack<int>();
        s.Push(1); // stack contains 1
        s.Push(10); // stack contains 1, 10
        s.Push(100); // stack contains 1, 10, 100
        Console.WriteLine(s.Pop()); // stack contains 1, 10
        Console.WriteLine(s.Pop()); // stack contains 1
        Console.WriteLine(s.Pop()); // stack is empty
    }
}
```

이 프로그램을 컴파일하려면 이전 예제에 정의된 스택 클래스를 포함하는 어셈블리를 참조해야 합니다.

C# 프로그램은 여러 원본 파일에 저장될 수 있습니다. C# 프로그램을 컴파일하면 모든 원본 파일이 함께 처리되고 서로를 제약 없이 참조할 수 있습니다. 개념적으로 처리되기 전에 모든 원본 파일이 하나의 대량 파일에 연결된 것과 같습니다. 소수의 경우를 제외하고 선언 순서는 중요하지 않으므로 C#에서는 정방향 선언이 필요한 경우가 없습니다. C#은 소스 파일을 하나의 공용 형식만 선언하도록 제한하거나 소스 파일 이름이 소스 파일에 선언된 형식과 일치하도록 요구하지 않습니다.

이 둘러보기의 추가 문서에서는 이러한 조직 구성 요소에 대해 설명합니다.

---
## 로컬 환경 설정

### 개발 환경 선택
 - Windows 또는 Mac용 Visual Studio 를 사용하는 것이 좋습니다. Visual Studio 다운로드 페이지에서 무료 버전을 다운로드할 수 있습니다. Visual Studio에는 .NET SDK가 포함되어 있습니다.
 - Visual Studio Code 편집기를 사용할 수도 있습니다. 최신 .NET SDK 를 별도로 설치해야 합니다.
 - 다른 편집기를 선호하는 경우 최신 .NET SDK를 설치해야 합니다.

### 기본 애플리케이션 개발 흐름

이러한 자습서의 지침에서는 .NET CLI를 사용하여 애플리케이션을 만들고, 빌드하고, 실행한다고 가정합니다. 다음 명령을 사용합니다.

 - dotnet new는 애플리케이션 로더를 만듭니다. 이 명령은 애플리케이션에 필요한 파일과 자산을 생성합니다. C# 소개 자습서에서는 모두 console 애플리케이션 유형을 모두 사용합니다. 기본 사항을 알고 나면 다른 애플리케이션 유형으로 확장할 수 있습니다.
 - dotnet build는 실행 파일을 빌드합니다.
 - dotnet run은 실행 파일을 실행합니다.

이러한 자습서를 위해 Visual Studio 2019을 사용하는 경우 자습서에서 다음 CLI 명령 중 하나를 실행하도록 지시하는 경우 Visual Studio 메뉴 선택을 선택합니다.

 - 파일>새로 만들기>프로젝트는 애플리케이션을 만듭니다.
     - Console Application 프로젝트 템플릿을 권장합니다.
     - 대상 프레임워크를 지정하는 옵션이 제공됩니다. 아래 자습서는 .NET 5 이상을 대상으로 지정할 때 가장 잘 작동합니다.
 - 빌드>솔루션 빌드는 실행 파일을 빌드합니다.
 - 디버그>디버깅하지 않고 시작은 실행 파일을 실행합니다.

---
## C#에서 정수 및 부동 소수점 숫자를 사용하는 방법

### 정수 계산 살펴보기

numbers-quickstart라는 디렉터리를 만듭니다. 현재 디렉터리로 만들고 다음 명령을 실행합니다.

```bash
dotnet new console -n NumbersInCSharp -o .
```

```
!중요!

.NET 6 용 C# 템플릿은 ‘최상위 문’을 사용합니다. .NET 6으로 이미 업그레이드한 경우 애플리케이션이 이 문서의 코드와 일치하지 않을 수 있습니다. 자세한 내용은 최상위 문을 생성하는 새 C# 템플릿을 참조하세요.

.NET 6 SDK는 다음 SDK를 사용하는 프로젝트에 대한 암시적global using 지시문 집합도 추가합니다.

Microsoft.NET.Sdk
Microsoft.NET.Sdk.Web
Microsoft.NET.Sdk.Worker

이러한 암시적 global using 지시문에는 해당 프로젝트 형식의 가장 일반적인 네임스페이스가 포함됩니다.

자세한 내용은 암시적 using 지시문 문서를 참조하세요.
```

원하는 편집기에서 Program.cs를 열고 파일의 콘텐츠를 다음 코드로 바꿉니다.

```C#
int a = 18;
int b = 6;
int c = a + b;
Console.WriteLine(c);
```

명령 창에 dotnet run을 입력하여 이 코드를 실행합니다.

정수를 사용하는 기본 수학 연산 중 하나를 살펴봤습니다. int 형식은 정수(0, 양의 정수 또는 음의 정수)를 나타냅니다. 더하기의 경우 + 기호를 사용합니다. 정수에 대해 다른 일반적인 수학 연산은 다음과 같습니다.

 - 빼기의 경우 -
 - 곱하기의 경우 *
 - 나누기의 경우 /

다른 연산을 살펴보세요. c의 값을 쓰는 줄 뒤에 다음 줄을 추가합니다.

```C#
// subtraction
c = a - b;
Console.WriteLine(c);

// multiplication
c = a * b;
Console.WriteLine(c);

// division
c = a / b;
Console.WriteLine(c);
```

명령 창에 dotnet run을 입력하여 이 코드를 실행합니다.

원하는 경우 동일한 줄에서 여러 수학 연산을 작성하여 실험할 수도 있습니다. 예를 들어 c = a + b - 12 * 17;을 사용해 보세요. 변수와 상수를 혼합해서 사용할 수 있습니다.

```
팁

C# (또는 다른 프로그래밍 언어)를 살펴보면서 코드를 작성할 때 실수를 하게 될 것입니다. 컴파일러는 그러한 오류를 찾아 사용자에게 보고합니다. 출력에 오류 메시지가 포함되어 있으면 예제 코드와 창의 코드를 자세히 살펴보고 수정 사항을 확인하세요. 이 연습은 C# 코드의 구조를 학습하는 데 도움이 됩니다.
```

첫 번째 단계를 완료했습니다. 다음 섹션을 시작하기 전에 현재 코드를 별도의 메서드로 이동합니다. 메서드는 함께 그룹화되고 이름이 지정된 일련의 문입니다. 메서드 이름 뒤에 ()를 써서 메서드를 호출합니다. 코드를 메서드로 구성하면 새 예제 작업을 쉽게 시작할 수 있습니다. 작업을 마치면 코드가 다음과 같이 됩니다.

```C#
WorkWithIntegers();

void WorkWithIntegers()
{
    int a = 18;
    int b = 6;
    int c = a + b;
    Console.WriteLine(c);


    // subtraction
    c = a - b;
    Console.WriteLine(c);

    // multiplication
    c = a * b;
    Console.WriteLine(c);

    // division
    c = a / b;
    Console.WriteLine(c);
}
```

줄 WorkWithIntegers();는 메서드를 호출합니다. 다음 코드는 메서드를 선언하고 정의합니다.

### 연산 순서 알아보기

WorkingWithIntegers()에 대한 호출을 주석으로 처리합니다. 그러면 이 섹션에서 작업할 때 출력이 덜 복잡해집니다.

```C#
//WorkWithIntegers();
```

//는 C#에서 주석을 시작합니다. 주석은 소스 코드에 유지하되 코드로 실행하지는 않으려는 모든 텍스트입니다. 컴파일러는 주석에서 실행 코드를 생성하지 않습니다. WorkWithIntegers()는 메서드이므로 한 줄만 주석으로 처리해야 합니다.

C# 언어는 수학에서 배운 규칙과 일치하는 규칙으로 여러 가지 수학 연산의 우선 순위를 정의합니다. 곱하기와 나누기는 더하기와 빼기보다 우선 순위가 높습니다. 다음 코드를 WorkWithIntegers() 호출 뒤에 추가하고 dotnet run을 실행하여 살펴봅니다.

```C#
int a = 5;
int b = 4;
int c = 2;
int d = a + b * c;
Console.WriteLine(d);
```

출력에서는 곱하기가 수행된 후 더하기가 수행되었음을 보여 줍니다.

먼저 수행하려는 연산 주위에 괄호를 추가하여 다른 연산 순서를 적용할 수 있습니다. 다음 줄을 추가하고 다시 실행합니다.

```C#
d = (a + b) * c;
Console.WriteLine(d);
```

여러 다른 연산을 결합하여 자세히 살펴보세요. 다음과 같은 줄을 추가합니다. dotnet run을 다시 시도해 봅니다.

```C#
d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
Console.WriteLine(d);
```

정수에 대해 흥미로운 동작을 이미 알고 있을 수 있습니다. 정수 나누기는 결과에 소수 또는 소수 부분이 포함될 것으로 예상되는 경우에도 항상 정수 결과를 생성합니다.

이러한 동작을 본 적이 없다면 다음 코드를 시도해 보세요.

```C#
int e = 7;
int f = 4;
int g = 3;
int h = (e + f) / g;
Console.WriteLine(h);
```

dotnet run을 다시 입력하여 결과를 확인합니다.

넘어가기 전에 이 섹션에서 작성한 모든 코드를 새 메서드에 배치해 보겠습니다. 이러한 새 메서드의 이름을 OrderPrecedence라고 하겠습니다. 코드는 다음과 비슷합니다.

```C#
// WorkWithIntegers();
OrderPrecedence();

void WorkWithIntegers()
{
    int a = 18;
    int b = 6;
    int c = a + b;
    Console.WriteLine(c);


    // subtraction
    c = a - b;
    Console.WriteLine(c);

    // multiplication
    c = a * b;
    Console.WriteLine(c);

    // division
    c = a / b;
    Console.WriteLine(c);
}

void OrderPrecedence()
{
    int a = 5;
    int b = 4;
    int c = 2;
    int d = a + b * c;
    Console.WriteLine(d);

    d = (a + b) * c;
    Console.WriteLine(d);

    d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
    Console.WriteLine(d);

    int e = 7;
    int f = 4;
    int g = 3;
    int h = (e + f) / g;
    Console.WriteLine(h);
}
```

### 정수 전체 자릿수 및 한도 살펴보기

마지막 샘플에서는 정수 나누기가 결과를 자르는 것을 보여 줍니다. modulo 연산자(% 문자)를 사용하여 나머지를 얻을 수 있습니다. OrderPrecedence() 메서드 호출 뒤에 다음 코드를 시도합니다.

```C#
int a = 7;
int b = 4;
int c = 3;
int d = (a + b) / c;
int e = (a + b) % c;
Console.WriteLine($"quotient: {d}");
Console.WriteLine($"remainder: {e}");
```

C# 정수 형식은 한 가지 다른 면에서 수학의 정수와 다릅니다. 즉 int 형식에는 최소 한도와 최대 한도가 있습니다. 이 코드를 추가하여 해당 한도를 확인합니다.

```C#
int max = int.MaxValue;
int min = int.MinValue;
Console.WriteLine($"The range of integers is {min} to {max}");
```

계산이 해당 한도를 초과하는 값을 생성하는 경우 언더플로 또는 오버플로 조건이 발생합니다. 답은 한 한도에서 다른 한도로 래핑하는 것으로 나타납니다. 다음 두 줄을 추가하여 예제를 확인합니다.

```C#
int what = max + 3;
Console.WriteLine($"An example of overflow: {what}");
```

답은 최소 (음의) 정수와 아주 가깝습니다. min + 2와 같습니다. 더하기 연산은 정수에 대해 허용된 값을 오버플로했습니다. 오버플로가 가능한 가장 큰 정수에서 가장 작은 정수로 “래핑”하기 때문에 답은 아주 큰 음수입니다.

int 형식이 요구 사항을 충족하지 않을 때 사용하는 여러 한도와 전체 자릿수가 있는 다른 숫자 형식이 있습니다. 다음으로 다른 형식을 살펴보겠습니다. 다음 섹션이 시작하기 전에 이 섹션에서 작성한 코드를 별도의 메서드로 옮깁니다. 이 EventHandler의 이름을 TestLimits로 지정합니다.

### double 형식 작업

double 숫자 형식은 배정밀도 부동 소수점 수를 나타냅니다. 이러한 용어는 생소할 수 있습니다. 부동 소수점 수는 아주 크거나 작은 정수가 아닌 수를 나타낼 때 유용합니다. 배정밀도는 값을 저장하는 데 사용되는 이진 자릿수를 설명하는 상대 용어입니다. 배정밀도 숫자의 이진 자릿수는 단정밀도의 두 배입니다. 최신 컴퓨터에서는 단정밀도 숫자보다 배정밀도를 더 많이 사용합니다. 단정밀도 숫자는 float 키워드를 사용하여 선언됩니다. 지금 살펴보세요. 다음 코드를 추가하고 결과를 확인합니다.

```C#
double a = 5;
double b = 4;
double c = 2;
double d = (a + b) / c;
Console.WriteLine(d);
```

답에 몫의 소수 부분이 포함되어 있습니다. double을 사용하여 약간 더 복잡한 식을 사용해 보세요.

```C#
double e = 19;
double f = 23;
double g = 8;
double h = (e + f) / g;
Console.WriteLine(h);
```

double 값의 범위는 정수 값보다 훨씬 큽니다. 지금까지 작성한 코드 아래에 다음 코드를 사용해 봅니다.

```C#
double max = double.MaxValue;
double min = double.MinValue;
Console.WriteLine($"The range of double is {min} to {max}");
```

이 값은 과학적 표기법으로 인쇄됩니다. E의 왼쪽에 있는 숫자는 유효 숫자입니다. 오른쪽의 숫자는 지수이며 10의 배수입니다. 수학의 10진수 숫자와 마찬가지로, C#에서 double에는 반올림 오류가 발생할 수 있습니다. 다음 코드를 사용해 보세요.

```C#
double third = 1.0 / 3.0;
Console.WriteLine(third);
```

유한한 횟수를 반복하는 것은 과 1/3정확히 동일하지 않다는 것을 알고 0.3 있습니다.

#### 과제

double 형식을 사용하여 큰 숫자, 작은 숫자, 곱하기 및 나누기로 다른 계산을 수행해 보세요. 더 복잡한 계산을 수행해 보세요. 과제를 하느라 약간의 시간을 보낸 후 작성한 코드를 새 메서드에 배치합니다. 이러한 새 메서드의 이름을 WorkWithDoubles로 지정합니다.

### 10진 형식으로 작업

C#의 기본적인 숫자 형식인 정수 형식과 double 형식을 살펴봤습니다. 학습할 또 다른 형식이 있습니다. 바로 decimal 형식입니다. decimal 형식은 범위가 작지만 double보다 전체 자릿수가 큽니다. 이 형식에 대해 살펴보겠습니다.

```C#
decimal min = decimal.MinValue;
decimal max = decimal.MaxValue;
Console.WriteLine($"The range of the decimal type is {min} to {max}");
```

범위가 double 형식보다 작습니다. 다음 코드를 사용하여 소수점이 있는 더 큰 전체 자릿수를 확인할 수 있습니다.

```C#
double a = 1.0;
double b = 3.0;
Console.WriteLine(a / b);

decimal c = 1.0M;
decimal d = 3.0M;
Console.WriteLine(c / d);
```

숫자의 M 접미사는 상수가 decimal 형식을 사용해야 함을 나타내는 방법입니다. 형식을 지정하지 않으면 컴파일러는 double 형식으로 간주합니다.

```
참고

문자 M은 double 키워드와 decimal 키워드 사이에서 가장 시각적으로 고유한 문자로 선택되었습니다.
```

소수점 형식을 사용하는 수학에는 소수점 오른쪽에 더 많은 숫자가 있습니다.

#### 과제

이제 여러 가지 숫자 형식을 살펴봤으므로 반지름이 2.50센티미터인 원의 면적을 계산하는 코드를 작성하세요. 원의 면적은 반지름 제곱 곱하기 PI입니다. 힌트: .NET에는 PI의 상수가 포함되어 있습니다. 즉 해당 값에 사용할 수 있는 Math.PI입니다. System.Math 네임스페이스에 선언된 모든 상수와 마찬가지로 Math.PI는 double 값입니다. 이러한 이유로 이 과제에는 decimal 값 대신 double을 사용해야 합니다.

---
## C# if 문 및 루프 - 조건부 논리 자습서

이 자습서에서는 변수를 검사하고 해당 변수에 따라 실행 경로를 변경하는 C# 코드를 작성하는 방법을 설명합니다. C# 코드를 작성하고 컴파일 및 실행 결과를 확인합니다. 이 자습서에는 C#에서 분기 및 루프 구문을 살펴보는 일련의 단원이 포함되어 있습니다. 이러한 단원에서는 C# 언어의 기본 사항을 설명합니다.

### if 문을 사용하여 결정하기

branches-tutorial이라는 디렉터리를 만듭니다. 현재 디렉터리로 만들고 다음 명령을 실행합니다.

```bash
dotnet new console -n BranchesAndLoops -o .
```

```
! 중요
.NET 6 용 C# 템플릿은 ‘최상위 문’을 사용합니다. .NET 6으로 이미 업그레이드한 경우 애플리케이션이 이 문서의 코드와 일치하지 않을 수 있습니다. 자세한 내용은 최상위 문을 생성하는 새 C# 템플릿을 참조하세요.

.NET 6 SDK는 다음 SDK를 사용하는 프로젝트에 대한 암시적global using 지시문 집합도 추가합니다.

Microsoft.NET.Sdk
Microsoft.NET.Sdk.Web
Microsoft.NET.Sdk.Worker
이러한 암시적 global using 지시문에는 해당 프로젝트 형식의 가장 일반적인 네임스페이스가 포함됩니다.

자세한 내용은 암시적 using 지시문 문서를 참조하세요.
```

이 명령은 현재 디렉터리에 새 .NET 콘솔 애플리케이션을 만듭니다. 원하는 편집기에서 Program.cs를 열고 콘텐츠를 다음 코드로 대체합니다.

```C#
int a = 5;
int b = 6;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10.");
```

콘솔 창에 dotnet run을 입력하여 이 코드를 사용해 봅니다. 콘솔에 "대답이 10보다 큽니다."라는 메시지가 표시됩니다. 합계가 10보다 작도록 b의 선언을 수정합니다.

```C#
int b = 3;
```
dotnet run을 다시 입력합니다. 답이 10보다 작기 때문에 아무것도 출력되지 않습니다. 테스트하는 조건은 false입니다. if 문에 대해 가능한 분기 중 하나(true 분기)만 작성했기 때문에 실행할 코드가 없습니다.

```
팁
C# (또는 다른 프로그래밍 언어)를 살펴보면서 코드를 작성할 때 실수를 하게 될 것입니다. 컴파일러가 오류를 찾아 보고합니다. 오류 출력 및 오류를 생성한 코드를 자세히 살펴봅니다. 일반적으로 컴파일러 오류는 문제를 찾는 데 도움이 될 수 있습니다.
```

이 첫 번째 샘플에서는 if의 기능과 부울 형식을 보여 줍니다. 부울은 true 또는 false의 두 값 중 하나를 가질 수 있는 변수입니다. C#은 부울 변수에 대한 특수 형식 bool을 정의합니다. if 문은 bool의 값을 확인합니다. 값이 true인 경우 if 뒤의 문이 실행됩니다. 그렇지 않으면 건너뜁니다. 조건을 확인하고 해당 조건에 따라 문을 실행하는 이 프로세스는 강력합니다.

### if와 else를 함께 사용하기

true 분기와 false 분기의 여러 코드를 실행하려면 조건이 false일 때 실행되는 else 분기를 생성합니다. else 분기를 시도합니다. 아래 코드의 마지막 두 줄을 추가합니다(처음 네 줄은 이미 있음).

```C#
int a = 5;
int b = 3;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10");
else
    Console.WriteLine("The answer is not greater than 10");
```

else 키워드 뒤의 문은 테스트하는 조건이 false인 경우에만 실행됩니다. if 및 else를 부울 조건과 결합하면 true와 false 조건을 모두 처리하는 데 필요한 모든 기능이 제공됩니다.

```
중요
if 및 else 문 아래의 들여쓰기는 사용자가 보기 편하도록 하기 위함입니다. C# 언어는 들여쓰기 또는 공백을 중요하게 취급하지 않습니다. if 또는 else 키워드 뒤의 문은 조건에 따라 실행됩니다. 이 자습서의 모든 샘플에서는 문의 제어 흐름을 기준으로 줄을 들여쓰는 일반적인 방법을 따릅니다.
```

들여쓰기는 중요하지 않기 때문에 { 및 }를 사용하여 두 개 이상의 문이 조건부로 실행되는 블록의 일부가 되는 시기를 나타내야 합니다. C# 프로그래머는 일반적으로 모든 if 및 else 절에서 중괄호를 사용합니다. 다음 예제는 앞서 작성한 코드와 같습니다. 다음 코드와 일치하도록 위의 코드를 수정합니다.

```C#
int a = 5;
int b = 3;
if (a + b > 10)
{
    Console.WriteLine("The answer is greater than 10");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
}
```

더 복잡한 조건을 테스트할 수 있습니다. 지금까지 작성한 코드 뒤에 다음 코드를 추가합니다.

```C#
int c = 4;
if ((a + b + c > 10) && (a == b))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("And the first number is equal to the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("Or the first number is not equal to the second");
}
```

== 기호는 같음을 테스트합니다. ==을 사용하면 같음 테스트가 a = 5에서 확인한 할당과 구분됩니다.

&&는 “and”를 나타냅니다. true 분기에서 문을 실행하려면 두 조건이 모두 true여야 합니다. 이러한 예제에서는 { 및 }로 문을 묶으면 각 조건부 분기에 여러 문을 가질 수 있음도 보여 줍니다. 를 사용하여 || "or"를 나타낼 수도 있습니다. 지금까지 작성한 코드 뒤에 다음 코드를 추가합니다.

```C#
if ((a + b + c > 10) || (a == b))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("Or the first number is equal to the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("And the first number is not equal to the second");
}
```

a, b 및 c의 값을 수정하고 && 및 || 간에 전환하여 살펴봅니다. && 및 || 연산자가 어떻게 작동하는지 더 잘 이해할 수 있습니다.

첫 번째 단계를 완료했습니다. 다음 섹션을 시작하기 전에 현재 코드를 별도의 메서드로 이동합니다. 이렇게 하면 새 예제 작업을 쉽게 시작할 수 있습니다. ExploreIf()라는 메서드에 기존 코드를 배치합니다. 프로그램 위에서 호출합니다. 변경을 완료하면 코드가 다음과 같이 표시됩니다.

```C#
ExploreIf();

void ExploreIf()
{
    int a = 5;
    int b = 3;
    if (a + b > 10)
    {
        Console.WriteLine("The answer is greater than 10");
    }
    else
    {
        Console.WriteLine("The answer is not greater than 10");
    }

    int c = 4;
    if ((a + b + c > 10) && (a > b))
    {
        Console.WriteLine("The answer is greater than 10");
        Console.WriteLine("And the first number is greater than the second");
    }
    else
    {
        Console.WriteLine("The answer is not greater than 10");
        Console.WriteLine("Or the first number is not greater than the second");
    }

    if ((a + b + c > 10) || (a > b))
    {
        Console.WriteLine("The answer is greater than 10");
        Console.WriteLine("Or the first number is greater than the second");
    }
    else
    {
        Console.WriteLine("The answer is not greater than 10");
        Console.WriteLine("And the first number is not greater than the second");
    }
}
```
ExploreIf()에 대한 호출을 주석으로 처리합니다. 그러면 이 섹션에서 작업할 때 출력이 덜 복잡해집니다.

```C#
//ExploreIf();
```
//는 C#에서 주석을 시작합니다. 주석은 소스 코드에 유지하되 코드로 실행하지는 않으려는 모든 텍스트입니다. 컴파일러는 주석에서 실행 코드를 생성하지 않습니다.

### 루프를 사용하여 작업 반복

이 섹션에서는 루프를 사용하여 문을 반복합니다. ExploreIf 호출 후 이 코드를 추가합니다.

```C#
int counter = 0;
while (counter < 10)
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
}
```

while 문은 조건을 검사하고 while 뒤에 있는 문 또는 문 블록을 실행합니다. 조건이 false가 될 때까지 해당 문을 실행하여 조건을 반복적으로 확인합니다.

이 예제에서는 다른 새 연산자가 하나 있습니다. counter 변수 뒤의 ++는 증가 연산자입니다. 이 연산자는 counter의 값에 1을 더하고 해당 값을 counter 변수에 저장합니다.

```
 중요

코드를 실행할 때 while 루프 조건이 false로 바뀌는지 확인합니다. 그러하지 않으면 프로그램이 종료되지 않는 무한 루프를 생성합니다. 이러한 내용이 이 샘플에 설명되어 있지는 않은데, CTRL-C 또는 다른 방법을 사용하여 프로그램을 강제 종료해야 하기 때문입니다.
```

while 루프는 while 뒤에 코드를 실행하기 전에 조건을 테스트합니다. do ... while 루프는 코드를 먼저 실행한 후 조건을 확인합니다. do while 루프는 다음 코드에 나와 있습니다.

```C#
int counter = 0;
do
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
} while (counter < 10);
```
이 do 루프 및 이전 while 루프는 같은 출력을 생성합니다.

### for 루프 작업

C#에서는 일반적으로 for 루프가 사용됩니다. 다음 코드를 사용해 보세요.

```C#
for (int index = 0; index < 10; index++)
{
    Console.WriteLine($"Hello World! The index is {index}");
}
```

이전 코드는 while 루프 및 이미 사용한 do 루프와 동일한 작업을 수행합니다. for 문에는 작동 방식을 제어하는 세 부분이 있습니다.

첫 번째 부분은 for 이니셜라이저입니다. int index = 0;은 index가 루프 변수임을 선언하고 첫 번째 값을 0으로 설정합니다.

중간 부분은 for 조건입니다. index < 10은 이 for 루프가 카운터 값이 10보다 작으면 계속 실행됨을 선언합니다.

마지막 부분은 for 반복기입니다. index++는 for 문 다음의 블록을 실행한 후 루프 변수를 수정하는 방법을 지정합니다. 여기서 index는 블록이 실행될 때마다 1씩 증가하도록 지정합니다.

직접 실험해 보세요. 다음 변형을 각각 시도합니다.

 - 다른 값으로 시작하도록 이니셜라이저를 변경합니다.
 - 다른 값에서 중지하도록 조건을 변경합니다.

완료하면, 학습한 내용을 토대로 직접 코드를 작성해 보겠습니다.

이 자습서에서 다루지 않은 다른 반복 문이 하나 있는데, foreach 문이 그것입니다. foreach 문은 항목 시퀀스의 모든 항목에 대해 해당 문을 반복합니다. 컬렉션과 함께 사용되는 경우가 가장 많으므로 다음 자습서에서 설명합니다.

### 중첩 루프 만들기

while, do 또는 for 루프를 다른 루프 내에 중첩하여 내부 루프에 있는 각 항목과 외부 루프에 있는 각 항목의 조합을 사용하여 행렬을 만들 수 있습니다. 행과 열을 나타내는 영숫자 쌍 세트를 작성하겠습니다.

하나의 for 루프가 행을 생성할 수 있습니다.

```C#
for (int row = 1; row < 11; row++)
{
    Console.WriteLine($"The row is {row}");
}
```

다른 루프는 열을 생성할 수 있습니다.

```C#
for (char column = 'a'; column < 'k'; column++)
{
    Console.WriteLine($"The column is {column}");
}
```

한 루프를 다른 루프 안에 중첩하여 쌍을 구성할 수 있습니다.

```C#
for (int row = 1; row < 11; row++)
{
    for (char column = 'a'; column < 'k'; column++)
    {
        Console.WriteLine($"The cell is ({row}, {column})");
    }
}
```

내부 루프의 전체 실행마다 외부 루프가 한 번씩 증가하는 것을 볼 수 있습니다. 행과 열 중첩을 반대로 바꾸고 변경 내용을 직접 확인하세요. 완료되면 ExploreLoops()라는 메서드에 이 섹션의 코드를 배치합니다.

### 분기 및 루프 결합

이제 C# 언어로 된 if 문과 루프 구조를 확인했습니다. C# 코드를 작성하여 3으로 나눌 수 있는, 1에서 20까지의 모든 정수의 합계를 찾을 수 있는지 확인해 보세요. 다음은 몇 가지 힌트입니다.

 - % 연산자는 나누기 연산의 나머지를 제공합니다.
 - if 문은 숫자가 합계의 일부여야 하는지를 확인하는 조건을 제공합니다.
 - for 루프는 1에서 20까지의 모든 숫자에 대해 일련의 단계를 반복하는 데 도움이 됩니다.

직접 시도해 보세요. 그런 다음 어떻게 했는지 확인하세요. 답으로 63을 받아야 합니다. GitHub에서 완성된 코드를 보고 가능한 한 가지 답을 확인할 수 있습니다.

---
## C#에서 목록<T> 를 사용하여 데이터 수집을 관리하는 방법 알아보기

### 기본 목록 예제

list-tutorial이라는 디렉터리를 만듭니다. 현재 디렉터리로 지정하고 dotnet new console을 실행합니다.

```
중요

.NET 6 용 C# 템플릿은 ‘최상위 문’을 사용합니다. .NET 6으로 이미 업그레이드한 경우 애플리케이션이 이 문서의 코드와 일치하지 않을 수 있습니다. 자세한 내용은 최상위 문을 생성하는 새 C# 템플릿을 참조하세요.

.NET 6 SDK는 다음 SDK를 사용하는 프로젝트에 대한 암시적global using 지시문 집합도 추가합니다.

Microsoft.NET.Sdk
Microsoft.NET.Sdk.Web
Microsoft.NET.Sdk.Worker
이러한 암시적 global using 지시문에는 해당 프로젝트 형식의 가장 일반적인 네임스페이스가 포함됩니다.

자세한 내용은 암시적 using 지시문 문서를 참조하세요.
```

편집기에서 Program.cs를 열고 기존 코드를 다음으로 바꿉니다.

```C#
List<string> names = ["<name>", "Ana", "Felipe"];
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

<name>을 사용자의 이름으로 바꿉니다. Program.cs를 저장합니다. 콘솔 창에 dotnet run을 입력하여 시도해 보세요.

문자열 목록을 만들고, 해당 목록에 세 개의 이름을 추가하고, 모든 CAPS에 이름을 인쇄했습니다. 이전 자습서에서 학습한 개념을 사용하여 목록을 반복합니다.

이름을 표시하는 코드는 문자열 보간 기능을 사용합니다. string 앞에 $ 문자를 넣으면 문자열 선언에 C# 코드를 포함할 수 있습니다. 실제 문자열은 C# 코드를 생성하는 값으로 바꿉니다. 이 예제에서는 ToUpper 메서드를 호출했기 때문에 {name.ToUpper()}를 대문자로 변환된 각 이름으로 바꿉니다.

계속해서 살펴보겠습니다.

### 목록 콘텐츠 수정

생성한 컬렉션은 List<T> 형식을 사용합니다. 이 형식은 요소의 시퀀스를 저장합니다. 꺾쇠 괄호 사이의 요소 형식을 지정합니다.

이 List<T> 형식은 늘리거나 줄일 수 있어 요소를 추가하거나 제거할 수 있습니다. 이 코드를 프로그램 끝에 추가합니다.

```C#
Console.WriteLine();
names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

목록 끝에 이름을 두 개 더 추가했습니다. 또한 이름을 하나 제거했습니다. 파일을 저장하고 dotnet run을 입력하여 시도해 보세요.

List<T>를 사용하면 인덱스별로 각 항목을 참조할 수도 있습니다. 목록 이름 뒤 [와 ] 토큰 사이에 인덱스를 배치합니다. C#은 첫 번째 인덱스에 0을 사용합니다. 방금 추가한 코드 바로 아래에 이 코드를 추가하여 시도합니다.

```C#
Console.WriteLine($"My name is {names[0]}");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");
```

목록의 끝을 벗어나는 인덱스에 액세스할 수 없습니다. 인덱스는 0부터 시작하므로, 가장 큰 유효 인덱스는 목록의 항목 수보다 하나 작습니다. Count 속성을 사용하여 목록의 길이를 확인할 수 있습니다. 프로그램 끝에 다음 코드를 추가합니다.

```C#
Console.WriteLine($"The list has {names.Count} people in it");
```

파일을 저장하고 dotnet run을 다시 입력하여 결과를 확인합니다.

### 목록 검색 및 정렬

샘플에서는 상대적으로 작은 목록을 사용하지만 애플리케이션에서는 수천에 달하는 많은 요소가 포함된 목록을 작성할 수 있습니다. 이러한 큰 컬렉션에서 요소를 찾으려면 여러 항목의 목록을 검색해야 합니다. IndexOf 메서드는 항목을 검색하고 항목의 인덱스를 반환합니다. 목록에 항목이 없으면 IndexOf가 -1을 반환합니다. 프로그램 맨 아래에 이 코드를 추가합니다.

```C#
var index = names.IndexOf("Felipe");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");
}

index = names.IndexOf("Not Found");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");

}
```

목록의 항목도 정렬할 수 있습니다. Sort 메서드는 일반적인 순서(문자열의 경우 사전순)로 목록의 모든 항목을 정렬합니다. 프로그램 맨 아래에 이 코드를 추가합니다.

```C#
names.Sort();
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

파일을 저장하고 dotnet run을 입력하여 이 최신 버전을 사용해 보세요.

다음 섹션을 시작하기 전에 현재 코드를 별도의 메서드로 이동합니다. 이렇게 하면 새 예제 작업을 쉽게 시작할 수 있습니다. 작성한 모든 코드를 WorkWithStrings()라는 새 메서드에 넣습니다. 프로그램 위에서 해당 메서드를 호출합니다. 작업을 마치면 코드가 다음과 같이 됩니다.

```C#
WorkWithStrings();

void WorkWithStrings()
{
    List<string> names = ["<name>", "Ana", "Felipe"];
    foreach (var name in names)
    {
        Console.WriteLine($"Hello {name.ToUpper()}!");
    }

    Console.WriteLine();
    names.Add("Maria");
    names.Add("Bill");
    names.Remove("Ana");
    foreach (var name in names)
    {
        Console.WriteLine($"Hello {name.ToUpper()}!");
    }

    Console.WriteLine($"My name is {names[0]}");
    Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");

    Console.WriteLine($"The list has {names.Count} people in it");

    var index = names.IndexOf("Felipe");
    if (index == -1)
    {
        Console.WriteLine($"When an item is not found, IndexOf returns {index}");
    }
    else
    {
        Console.WriteLine($"The name {names[index]} is at index {index}");
    }

    index = names.IndexOf("Not Found");
    if (index == -1)
    {
        Console.WriteLine($"When an item is not found, IndexOf returns {index}");
    }
    else
    {
        Console.WriteLine($"The name {names[index]} is at index {index}");

    }

    names.Sort();
    foreach (var name in names)
    {
        Console.WriteLine($"Hello {name.ToUpper()}!");
    }
}
```

### 다른 형식 목록

지금까지 목록에 string 형식을 사용했습니다. 다른 형식을 사용하여 List<T>를 만들어 보겠습니다. 숫자 집합을 빌드하겠습니다.

WorkWithStrings()를 호출한 후 다음을 프로그램에 추가합니다.

```C#
List<int> fibonacciNumbers = [1, 1];
```

정수 목록을 만들고 처음 두 정수를 값 1로 설정합니다. 숫자 시퀀스인 피보나치 시퀀스의 첫 번째 두 값입니다. 다음 각 피보나치 수는 이전의 두 수의 합계를 사용하여 찾습니다. 이 코드를 추가합니다.

```C#
var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

fibonacciNumbers.Add(previous + previous2);

foreach (var item in fibonacciNumbers)
{
    Console.WriteLine(item);
}
```

파일을 저장하고 dotnet run을 입력하여 결과를 확인합니다.

```
 팁

이 섹션에만 집중하려면 WorkWithStrings();를 호출하는 코드를 주석으로 처리할 수 있습니다. 두 / 문자를 다음과 같이 // WorkWithStrings();호출 앞에 넣습니다.
```

### 과제

이 단원과 이전 단원에서 학습한 개념을 함께 적용할 수 있는지 확인하세요. 피보나치 수를 사용하여 지금까지 빌드한 내용을 확장합니다. 코드를 작성하여 시퀀스에서 처음 20개 수를 생성합니다. (힌트: 20번째 피보나치 수는 6765입니다.)

---
## C# 프로그램의 일반적인 구조체

C# 프로그램은 하나 이상의 파일로 구성됩니다. 각 파일은 0개 이상의 네임스페이스가 포함합니다. 네임스페이스는 클래스, 구조체, 인터페이스, 열거형 및 대리자와 같은 형식이나 다른 네임스페이스를 포함합니다. 다음 예제는 이러한 모든 요소를 포함하는 C# 프로그램의 기본 구조입니다.

```C#
// A skeleton of a C# program
using System;

// Your program starts here:
Console.WriteLine("Hello world!");

namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }
}
```

앞의 예제에서는 프로그램의 진입점에 대해 최상위 문을 사용합니다. 다음 예제와 같이 프로그램의 진입점으로 Main(이)라는 정적 메서드를 만들 수도 있습니다.

```C#
// A skeleton of a C# program
using System;
namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            //Your program starts here...
            Console.WriteLine("Hello world!");
        }
    }
}
```
---
## Main()과 명령줄 인수


Main 메서드는 C# 애플리케이션의 진입점입니다. (라이브러리와 서비스에는 Main 메서드가 진입점으로 필요하지 않습니다.) 애플리케이션이 시작될 때 Main 메서드는 호출되는 첫 번째 메서드입니다.

C# 프로그램에는 하나의 진입점만 있을 수 있습니다. Main 메서드가 있는 클래스가 둘 이상 있는 경우 StartupObject 컴파일러 옵션으로 프로그램을 컴파일하여 진입점으로 사용할 Main 메서드를 지정해야 합니다. 자세한 내용은 StartupObject(C# 컴파일러 옵션)를 참조하세요.

```C#
class TestClass
{
    static void Main(string[] args)
    {
        // Display the number of command line arguments.
        Console.WriteLine(args.Length);
    }
}
```

한 파일의 최상위 문을 애플리케이션의 진입점으로 사용할 수도 있습니다. 메서드와 Main 마찬가지로 최상위 문은 값을 반환하고 명령줄 인수에 액세스할 수도 있습니다. 자세한 내용은 최상위 문을 참조 하세요.

```C#
using System.Text;

StringBuilder builder = new();
builder.AppendLine("The following arguments are passed:");

// Display the command line arguments using the args variable.
foreach (var arg in args)
{
    builder.AppendLine($"Argument={arg}");
}

Console.WriteLine(builder.ToString());

// Return a success code.
return 0;
```

### 개요

 - Main 메서드는 실행 가능한 프로그램의 진입점으로, 프로그램의 제어가 시작되고 끝나는 위치합니다.
 - Main은 클래스 또는 구조체 내부에 선언됩니다 Main은 static이어야 하며 public일 필요는 없습니다. (이전 예제에서는 .의 private기본 액세스를 받습니다.) 은 묶을 class 수 있습니다 static.
 - Main은 void, int, Task 또는 Task<int> 반환 형식을 가질 수 있습니다.
 - Main에서 Task 또는 Task<int>을 반환하는 경우에만 Main 선언에 async 한정자가 포함될 수 있습니다. 이는 특히 async void Main 메서드를 제외합니다.
 - Main 메서드는 명령줄 인수를 포함하는 string[] 매개 변수 사용 여부에 관계 없이 선언될 수 있습니다. Visual Studio를 사용하여 Windows 애플리케이션을 만드는 경우 매개 변수를 수동으로 추가하거나 GetCommandLineArgs() 메서드를 사용하여 명령줄 인수를 가져올 수 있습니다. 매개 변수는 0부터 시작하는 명령줄 인수로 읽힙니다. C 및 C++와 달리, 프로그램의 이름이 args 배열의 첫 번째 명령줄 인수로 처리되지 않지만, GetCommandLineArgs() 메서드의 첫 번째 요소입니다.

다음 목록은 유효한 Main 서명을 보여 줍니다.

```C#
public static void Main() { }
public static int Main() { }
public static void Main(string[] args) { }
public static int Main(string[] args) { }
public static async Task Main() { }
public static async Task<int> Main() { }
public static async Task Main(string[] args) { }
public static async Task<int> Main(string[] args) { }
```

앞의 예에서는 모두 public 접근자 한정자를 사용합니다. 이는 일반적이지만 필수는 아닙니다.

async 및 Task, Task<int> 반환 형식을 추가하면 콘솔 애플리케이션을 시작해야 하고 비동기 작업을 Main에서 await해야 하는 경우에 프로그램 코드가 간소화됩니다.

### Main() 반환 값

다음 방법 중 하나로 메서드를 정의하여 Main 메서드에서 int를 반환할 수 있습니다.

| Main 메서드 코드            | Main 서명                                    |
|------------------------|--------------------------------------------|
| args 또는 await 사용 안 함   | static int Main()                          |
| args 사용, await 사용 안 함  | static int Main(string[] args)             |
| args 사용 안 함 , await 사용 | static async Task<int> Main()              |
| args 및 await 사용        | static async Task<int> Main(string[] args) |

Main의 반환 값을 사용하지 않는 경우 void 또는 Task를 반환하면 코드가 다소 단순해집니다.

| Main 메서드 코드            | Main 서명                               |
|------------------------|---------------------------------------|
| args 또는 await 사용 안 함   | static void Main()                    |
| args 사용, await 사용 안 함  | static void Main(string[] args)       |
| args 사용 안 함 , await 사용 | static async Task Main()              |
| args 및 await 사용        | static async Task Main(string[] args) |

그러나 int 또는 Task<int>를 반환하면 프로그램이 실행 파일을 호출하는 다른 프로그램이나 스크립트에 상태 정보를 전달할 수 있습니다.

다음 예제에서는 프로세스의 종료 코드에 액세스할 수 있는 방법을 보여줍니다.

이 예제에서는 .NET Core 명령줄 도구를 사용합니다. .NET Core 명령줄 도구에 대해 잘 모르는 경우 이 시작 문서에서 알아볼 수 있습니다.

dotnet new console을 실행하여 새 애플리케이션을 만듭니다. Program.cs 에서 Main 메서드를 다음과 같이 수정합니다.

```C#
// Save this program as MainReturnValTest.cs.
class MainReturnValTest
{
    static int Main()
    {
        //...
        return 0;
    }
}
```

Windows에서 프로그램을 실행하는 경우 Main 함수에서 반환된 값은 환경 변수에 저장됩니다. 이 환경 변수는 배치 파일에서 ERRORLEVEL을 사용하거나 PowerShell에서 $LastExitCode를 사용하여 검색할 수 있습니다.

dotnet CLIdotnet build 명령을 사용하여 애플리케이션을 빌드할 수 있습니다.

다음으로 애플리케이션을 실행하고 결과를 표시하는 PowerShell 스크립트를 만듭니다. 다음 코드를 텍스트 파일에 붙여넣고 이 파일을 프로젝트가 포함된 폴더에 test.ps1로 저장합니다. PowerShell 프롬프트에 test.ps1을 입력하여 PowerShell 스크립트를 실행합니다.

코드에서 0을 반환하기 때문에 배치 파일이 성공했다고 보고합니다. 그러나 0이 아닌 값을 반환하도록 MainReturnValTest.cs를 변경한 다음 프로그램을 다시 컴파일하면 다음에 PowerShell 스크립트를 실행할 때 오류가 보고됩니다.

```shell
dotnet run
if ($LastExitCode -eq 0) {
    Write-Host "Execution succeeded"
} else
{
    Write-Host "Execution Failed"
}
Write-Host "Return value = " $LastExitCode
```
```
Execution succeeded
Return value = 0
```
### 비동기 Main 반환 값

Main에 대한 async 반환 값을 선언하면 컴파일러는 Main에서 비동기 메서드를 호출하기 위한 상용구 코드를 생성합니다. async 키워드를 지정하지 않으면 다음 예와 같이 해당 코드를 직접 작성해야 합니다. 예의 코드는 비동기 작업이 완료될 때까지 프로그램이 실행되도록 보장합니다.

```C#
class AsyncMainReturnValTest
{
    public static void Main()
    {
        AsyncConsoleWork().GetAwaiter().GetResult();
    }

    private static async Task<int> AsyncConsoleWork()
    {
        // Main body here
        return 0;
    }
}
```

이 상용구 코드는 다음으로 바뀔 수 있습니다.

```C#
class Program
{
    static async Task<int> Main(string[] args)
    {
        return await AsyncConsoleWork();
    }

    private static async Task<int> AsyncConsoleWork()
    {
        // main body here 
        return 0;
    }
}
```

Main을 async로 선언하면 컴파일러가 항상 올바른 코드를 생성한다는 이점이 있습니다.

애플리케이션 진입점에서 Task 또는 Task<int>를 반환하는 경우 컴파일러는 애플리케이션 코드에서 선언된 진입점 메서드를 호출하는 새 진입점을 생성합니다. 이 진입점이 $GeneratedMain이라고 가정하면 컴파일러는 이러한 진입점에 대해 다음 코드를 생성합니다.

 - static Task Main() - 컴파일러에서 private static void $GeneratedMain() => Main().GetAwaiter().GetResult();에 해당하는 코드를 내보냅니다.
 - static Task Main(string[]) - 컴파일러에서 private static void $GeneratedMain(string[] args) => Main(args).GetAwaiter().GetResult();에 해당하는 코드를 내보냅니다.
 - static Task<int> Main() - 컴파일러에서 private static int $GeneratedMain() => Main().GetAwaiter().GetResult();에 해당하는 코드를 내보냅니다.
 - static Task<int> Main(string[]) - 컴파일러에서 private static int $GeneratedMain(string[] args) => Main(args).GetAwaiter().GetResult();에 해당하는 코드를 내보냅니다.

```
 참고

예제에서 Main 메서드에 async 한정자를 사용하더라도 컴파일러는 동일한 코드를 생성합니다.
```

### 명령줄 인수

다음 방법 중 하나로 메서드를 정의하여 인수를 Main 메서드에 보낼 수 있습니다.

| Main 메서드 코드          | Main 서명                                    |
|----------------------|--------------------------------------------|
| 반환 값 없음, await 사용 없음 | static void Main(string[] args)            |
| 반환 값, await 사용 없음    | static int Main(string[] args)             |
| 반환 값 없음, await 사용    | static async Task Main(string[] args)      |
| 반환 값, await 사용       | static async Task<int> Main(string[] args) |

인수가 사용되지 않는 경우 약간 더 간단한 코드를 위해 메서드 서명에서 args를 생략할 수 있습니다.

| Main 메서드 코드          | Main 서명                       |
|----------------------|-------------------------------|
| 반환 값 없음, await 사용 없음 | static void Main()            |
| 반환 값, await 사용 없음    | static int Main()             |
| 반환 값 없음, await 사용    | static async Task Main()      |
| 반환 값, await 사용       | static async Task<int> Main() |

```
참고

Environment.CommandLine 또는 Environment.GetCommandLineArgs를 사용하여 콘솔 또는 Windows Forms 애플리케이션의 임의 지점에서 명령줄 인수에 액세스할 수 있습니다. Windows Forms 애플리케이션의 Main 메서드 서명에서 명령줄 인수를 사용하도록 설정하려면 Main의 서명을 수동으로 수정해야 합니다. Windows Forms 디자이너에서 생성된 코드는 입력 매개 변수 없이 Main을 만듭니다.
```

Main 메서드의 매개 변수는 명령줄 인수를 나타내는 String 배열입니다. 일반적으로 다음과 같이 Length 속성을 테스트하여 인수가 있는지 확인합니다.

```c#
if (args.Length == 0)
{
    System.Console.WriteLine("Please enter a numeric argument.");
    return 1;
}
```
```
 팁

args 배열은 null일 수 없습니다. 따라서 null 검사 없이 Length 속성에 액세스하는 것이 안전합니다.
```

Convert 클래스 또는 Parse 메서드를 사용하여 문자열 인수를 숫자 형식으로 변환할 수도 있습니다. 예를 들어 다음 문은 Parse 메서드를 사용하여 string을 long 숫자로 변환합니다.

```C#
long num = Int64.Parse(args[0]);
```
Int64의 별칭을 지정하는 C# 형식 long을 사용할 수도 있습니다.

```C#
long num = long.Parse(args[0]);
```
Convert 클래스 메서드 ToInt64를 사용하여 같은 작업을 수행할 수도 있습니다.

```C#
long num = Convert.ToInt64(s);
```
자세한 내용은 Parse 및 Convert를 참조하세요.

```
팁

명령줄 인수 구문 분석이 복잡할 수 있습니다. System.CommandLine 라이브러리(현재 베타)를 사용하여 프로세스를 간소화하는 것이 좋습니다.
```

다음 예제에서는 콘솔 애플리케이션에서 명령줄 인수를 사용하는 방법을 보여 줍니다. 애플리케이션은 런타임에 하나의 인수를 사용하고, 인수를 정수로 변환하고, 숫자의 계승을 계산합니다. 인수가 제공되지 않으면 애플리케이션에서는 프로그램의 올바른 사용법을 설명하는 메시지를 표시합니다.

명령 프롬프트에서 애플리케이션을 컴파일 및 실행하려면 다음 단계를 수행합니다.

 1. 다음 코드를 텍스트 편집기에 붙여넣고 이름 Factorial.cs를 사용하여 파일을 텍스트 파일로 저장합니다.
 ```C#
 public class Functions
 {
    public static long Factorial(int n)
    {
        // Test for invalid input.
        if ((n < 0) || (n > 20))
        {
            return -1;
        }

        // Calculate the factorial iteratively rather than recursively.
        long tempResult = 1;
        for (int i = 1; i <= n; i++)
        {
            tempResult *= i;
        }
        return tempResult;
    }
 }

 class MainClass
 {
    static int Main(string[] args)
    {
        // Test if input arguments were supplied.
        if (args.Length == 0)
        {
            Console.WriteLine("Please enter a numeric argument.");
            Console.WriteLine("Usage: Factorial <num>");
            return 1;
        }

        // Try to convert the input arguments to numbers. This will throw
        // an exception if the argument is not a number.
        // num = int.Parse(args[0]);
        int num;
        bool test = int.TryParse(args[0], out num);
        if (!test)
        {
            Console.WriteLine("Please enter a numeric argument.");
            Console.WriteLine("Usage: Factorial <num>");
            return 1;
        }

        // Calculate factorial.
        long result = Functions.Factorial(num);

        // Print result.
        if (result == -1)
            Console.WriteLine("Input must be >= 0 and <= 20.");
        else
            Console.WriteLine($"The Factorial of {num} is {result}.");

        return 0;
    }
 }
 // If 3 is entered on command line, the
 // output reads: The factorial of 3 is 6.
 ```
 2. 시작 화면이나 시작 메뉴에서 Visual Studio 개발자 명령 프롬프트 창을 열고 만든 파일이 포함된 폴더로 이동합니다.
 3. 다음 명령을 입력하여 애플리케이션을 컴파일합니다.<br>dotnet build<br>애플리케이션에 컴파일 오류가 없으면 Factorial.exe라는 실행 파일이 만들어집니다.
 4. 다음 명령을 입력하여 3의 계승을 계산합니다.<br>dotnet run -- 3
 5. 이 명령은 다음 출력을 생성합니다. The factorial of 3 is 6.


```
참고

Visual Studio에서 애플리케이션을 실행할 경우 프로젝트 디자이너, 디버그 페이지에서 명령줄 인수를 지정할 수 있습니다.
```

---
## 최상위 문 - Main 메서드가 없는 프로그램

콘솔 애플리케이션 프로젝트에 Main 메서드를 명시적으로 포함할 필요가 없습니다. 대신 최상위 문 기능을 사용하여 작성해야 하는 코드를 최소화할 수 있습니다.

최상위 문을 사용하면 파일의 루트에 직접 실행 코드를 작성할 수 있으므로 클래스 또는 메서드에서 코드를 래핑할 필요가 없습니다. 따라서 Program 클래스 및 Main 메서드의 형식 없이 프로그램을 만들 수 있습니다. 이 경우 컴파일러는 애플리케이션에 대한 진입점 메서드를 사용하여 Program 클래스를 생성합니다. 생성된 메서드의 이름은 Main이(가) 아니며, 코드에서 직접 참조할 수 없는 구현 세부 정보입니다.

다음은 C# 10의 완전한 C# 프로그램인 Program.cs 파일입니다.

```C#
Console.WriteLine("Hello World!");
```

최상위 문을 사용하면 Azure Functions 및 GitHub Actions와 같은 소규모 유틸리티에 대한 간단한 프로그램을 작성할 수 있습니다. 또한 새로운 C# 프로그래머가 코드를 학습하고 작성하는 작업을 더 쉽게 수행할 수 있습니다.

다음 섹션에서는 최상위 문으로 수행할 수 있는 작업과 수행할 수 없는 작업에 대한 규칙을 설명합니다.

### 하나의 최상위 파일만

애플리케이션에는 진입점이 하나만 있어야 합니다. 프로젝트에는 최상위 문이 있는 파일이 하나만 있을 수 있습니다. 프로젝트의 두 개 이상의 파일에 최상위 문을 넣으면 다음과 같은 컴파일러 오류가 발생합니다.

> CS8802 하나의 컴파일 단위만 최상위 문을 포함할 수 있습니다.

프로젝트에는 최상위 문이 없는 추가 소스 코드 파일이 얼마든지 있을 수 있습니다.

### 다른 진입점 없음

Main 메서드를 명시적으로 작성할 수 있지만 진입점으로 작동할 수는 없습니다. 컴파일러에서 다음과 같은 경고가 발생합니다.

> CS7022 프로그램의 진입점은 전역 코드이며 'Main()' 진입점은 무시됩니다.

최상위 문이 있는 프로젝트에서는 프로젝트에 하나 이상의 Main 메서드가 있는 경우에도 -main 컴파일러 옵션을 사용하여 진입점을 선택할 수 없습니다.

### using 지시문

using 지시문을 포함하는 경우 다음 예제와 같이 파일에서 먼저 제공되어야 합니다.

```C#
using System.Text;

StringBuilder builder = new();
builder.AppendLine("The following arguments are passed:");

// Display the command line arguments using the args variable.
foreach (var arg in args)
{
    builder.AppendLine($"Argument={arg}");
}

Console.WriteLine(builder.ToString());

// Return a success code.
return 0;
```

### 전역 네임스페이스

최상위 문은 전역 네임스페이스에서 암시적으로 사용할 수 있습니다.

### 네임스페이스 및 형식 정의

최상위 문이 있는 파일에는 네임스페이스 및 형식 정의도 포함될 수 있지만 최상위 문 뒤에 와야 합니다. 예시:
```C#
MyClass.TestMethod();
MyNamespace.MyClass.MyMethod();

public class MyClass
{
    public static void TestMethod()
    {
        Console.WriteLine("Hello World!");
    }
}

namespace MyNamespace
{
    class MyClass
    {
        public static void MyMethod()
        {
            Console.WriteLine("Hello World from MyNamespace.MyClass.MyMethod!");
        }
    }
}
```

### args
최상위 문은 args 변수를 참조하여 입력된 명령줄 인수에 액세스할 수 있습니다. args 변수는 null이 아니지만 명령줄 인수가 제공되지 않은 경우 Length는 0입니다. 예시:

```C#
if (args.Length > 0)
{
    foreach (var arg in args)
    {
        Console.WriteLine($"Argument={arg}");
    }
}
else
{
    Console.WriteLine("No arguments");
}
```
### await
await를 사용하여 비동기 메서드를 호출할 수 있습니다. 예시:

```C#
Console.Write("Hello ");
await Task.Delay(5000);
Console.WriteLine("World!");
```

### 프로세스의 종료 코드
애플리케이션 종료될 때 int 값을 반환하려면 int를 반환하는 Main 메서드에서와 같이 return 문을 사용합니다. 예시:
```C#
string? s = Console.ReadLine();

int returnValue = int.Parse(s ?? "-1");
return returnValue;
```

### 암시적 진입점 메서드
컴파일러는 최상위 문이 있는 프로젝트의 프로그램 진입점 역할을 하는 메서드를 생성합니다. 메서드의 서명은 최상위 문에 await 키워드 또는 return 문이 포함되어 있는지 여부에 따라 달라집니다. 다음 표에서는 편의를 위해 표에 있는 메서드 이름 Main을 사용하여 메서드 서명이 어떻게 표시되는지 보여줍니다.

| 최상위 코드에는 다음이 포함됩니다. | 암시적 Main 서명                                 |
|---------------------|---------------------------------------------|
| await 및 return      | static async Task<int> Main(string[] args)  |
| await               | static async Task Main(string[] args)       |
| return              | static int Main(string[] args)              |
| await 또는 return 없음  | static void Main(string[] args)             |

---
## C# 형식 시스템

C#은 강력한 형식의 언어입니다. 모든 변수 및 상수에는 값으로 계산되는 모든 식을 실행하는 형식이 있습니다. 모든 메서드 선언은 각 입력 매개 변수와 반환 값의 이름, 형식, 종류(값, 참조 또는 출력)를 지정합니다. .NET 클래스 라이브러리는 기본 제공 숫자 형식과 다양한 구문을 나타내는 복합 형식을 정의합니다. 여기에는 파일 시스템, 네트워크 연결, 개체의 컬렉션과 배열, 날짜가 포함됩니다. 일반 C# 프로그램에서는 클래스 라이브러리의 형식 및 프로그램의 문제 도메인에 관련된 개념을 모델링하는 사용자 정의 형식을 사용합니다.

형식에 저장된 정보에는 다음 항목이 포함될 수 있습니다.

 - 형식 변수에 필요한 스토리지 공간.
 - 형식이 나타낼 수 있는 최대값 및 최소값.
 - 형식에 포함되는 멤버(메서드, 필드, 이벤트 등).
 - 형식이 상속하는 기본 형식.
 - 구현하는 인터페이스.
 - 허용되는 작업 유형.

컴파일러는 형식 정보를 사용하여 코드에서 수행되는 모든 작업의 형식이 안전한지 확인합니다. 예를 들어 int 형식의 변수를 선언하는 경우 컴파일러를 통해 더하기 및 빼기 작업에서 변수를 사용할 수 있습니다. bool 형식의 변수에 대해 같은 작업을 수행하려고 하면 컴파일러는 다음 예제와 같이 오류를 생성합니다.

```C#
int a = 5;
int b = a + 2; //OK

bool test = true;

// Error. Operator '+' cannot be applied to operands of type 'int' and 'bool'.
int c = a + test;
```

```
참고

C 및 C++ 개발자는 C#에서 bool이(가) int(으)로 변환될 수 없음을 알고 있습니다.
```

컴파일러는 형식 정보를 실행 파일에 메타데이터로 포함합니다. CLR(공용 언어 런타임)는 런타임에 이 메타데이터를 사용하여 메모리를 할당 및 회수할 때 형식 안정성을 추가로 보장합니다.


### 변수 선언에서 형식 지정

프로그램에서 변수나 상수를 선언할 때 컴파일러가 형식을 유추하게 하려면 형식을 지정하거나 var 키워드를 사용해야 합니다. 다음 예제에서는 기본 제공 숫자 형식 및 복잡한 사용자 정의 형식을 둘 다 사용하는 일부 변수 선언을 보여 줍니다.

```C#
// Declaration only:
float temperature;
string name;
MyClass myClass;

// Declaration with initializers (four examples):
char firstLetter = 'C';
var limit = 3;
int[] source = [0, 1, 2, 3, 4, 5];
var query = from item in source
            where item <= limit
            select item;
```

메서드 매개 변수 및 반환 값의 형식은 메서드 선언에서 지정됩니다. 다음 시그니처는 입력 인수로 int(이)가 필요하고 문자열을 반환하는 메서드를 보여줍니다.

```C#
public string GetName(int ID)
{
    if (ID < names.Length)
        return names[ID];
    else
        return String.Empty;
}
private string[] names = ["Spencer", "Sally", "Doug"];
```
변수를 선언한 후에는 새 형식으로 다시 선언할 수 없으며 선언된 형식과 호환되지 않는 값을 할당할 수 없습니다. 예를 들어 int을(를) 선언한 다음 여기에 true 부울 값을 할당할 수 없습니다. 그러나 값은 새 변수에 할당되거나 메서드 인수로 전달될 경우 다른 형식으로 변환할 수 있습니다. 데이터 손실을 일으키지 않는 형식 변환은 컴파일러에서 자동으로 수행됩니다. 데이터 손실을 일으킬 수 있는 변환의 경우 소스 코드에 캐스트가 있어야 합니다.

자세한 내용은 캐스팅 및 형식 변환을 참조하세요.


### 기본 제공 형식

C#은 기본 제공 형식의 표준 집합을 제공합니다. 이러한 표준 집합은 정수, 부동 소수점 값, 부울 식, 텍스트 문자, 10진수 값, 기타 데이터 형식을 나타냅니다. 이 밖에도 기본 제공 string 및 object 형식이 있습니다. 이러한 형식을 이러한 형식을 모든 C# 프로그램에서 사용할 수 있습니다. 기본 제공 형식의 전체 목록은 기본 제공 형식을 참조하세요.


### 사용자 지정 형식

struct, class, interface, enum, record 구문을 사용하여 자체 사용자 지정 형식을 만듭니다. .NET 클래스 라이브러리 자체는 자체 애플리케이션에서 사용할 수 있는 사용자 지정 형식의 컬렉션입니다. 기본적으로 클래스 라이브러리의 가장 자주 사용되는 형식을 모든 C# 프로그램에서 사용할 수 있습니다. 기타 형식은 해당 형식을 정의하는 어셈블리에 프로젝트 참조를 명시적으로 추가하는 경우에만 사용할 수 있습니다. 컴파일러에 어셈블리에 대한 참조가 포함된 후에는 소스 코드에서 해당 어셈블리에 선언된 형식의 변수(및 상수)를 선언할 수 있습니다. 자세한 내용은 .NET 클래스 라이브러리를 참조하세요.


### CTS(공용 형식 시스템)

.NET의 형식 시스템에 대한 다음과 같은 두 가지 기초 사항을 이해해야 합니다.

 - 형식 시스템은 상속 원칙을 지원합니다. 형식은 기본 형식이라는 다른 형식에서 파생될 수 있습니다. 파생 형식은 기본 형식의 메서드, 속성 및 기타 멤버를 상속합니다(몇 가지 제한 사항 있음). 기본 형식이 다른 형식에서 파생될 수도 있습니다. 이 경우 파생 형식은 상속 계층 구조에 있는 두 기본 형식의 멤버를 상속합니다. System.Int32(C# 키워드: int)과 같은 기본 제공 숫자 형식을 포함한 모든 형식은 궁극적으로 단일 기본 형식 System.Object(C# 키워드: object)에서 파생됩니다. 이 통합 형식 계층 구조를 CTS(공용 형식 시스템)라고 합니다. C#의 상속에 대한 자세한 내용은 상속을 참조하세요.
 - CTS의 각 형식은 값 형식 또는 참조 형식으로 정의됩니다. 이러한 형식에는 .NET 클래스 라이브러리의 모든 사용자 지정 형식과 자체 사용자 정의 형식도 포함됩니다. struct을(를) 사용하여 정의한 형식은 값 형식이고, 모든 기본 제공 숫자 형식은 structs입니다. class 또는 record 키워드를 사용하여 정의한 형식은 참조 형식입니다. 참조 형식과 값 형식의 컴파일 시간 규칙 및 런타임 동작은 서로 다릅니다.

다음 그림에서는 CTS에서 값 형식과 참조 형식 간의 관계를 보여 줍니다.

![](./img/value-reference-types-common-type-system.png)

```
 참고

가장 일반적으로 사용되는 형식은 모두 System 네임스페이스에 구성되어 있다는 사실을 알 수 있습니다. 그러나 형식이 포함된 네임스페이스는 형식이 값 형식인지 또는 참조 형식인지와 관련이 없습니다.
```

클래스 및 구조체는 .NET의 CTS(공용 형식 시스템)의 기본 구문 중 두 가지입니다. 각각은 기본적으로 하나의 논리 단위에 속하는 데이터 및 동작 집합을 캡슐화하는 데이터 구조입니다. 데이터와 동작은 클래스, 구조체 또는 레코드의 ‘멤버’입니다. 멤버는 이 문서의 뒷부분에 나열된 대로 해당 메서드, 속성, 이벤트 등을 포함합니다.

클래스, 구조체 또는 레코드 선언은 런타임에 인스턴스 또는 개체를 만드는 데 사용되는 청사진과도 같습니다. Person이라는 클래스, 구조체 또는 레코드를 정의하는 경우 Person이 형식의 이름입니다. 형식 Person의 변수 p를 선언하고 초기화하면 p는 Person의 개체 또는 인스턴스로 지칭됩니다. 같은 Person 형식의 여러 인스턴스를 만들 수 있으며 각 인스턴스는 속성 및 필드에 서로 다른 값을 가질 수 있습니다.

클래스는 참조 형식입니다. 이 형식의 개체가 만들어지면 개체가 할당되는 변수는 해당 메모리에 대한 참조만 보유합니다. 개체 참조가 새 변수에 할당되면 새 변수는 원래 개체를 나타냅니다. 모두 동일한 데이터를 참조하므로 한 변수의 변경 내용이 다른 변수에도 반영됩니다.

구조체는 값 형식입니다. 구조체가 만들어지면 해당 구조체가 할당되는 변수에 구조체의 실제 데이터가 포함됩니다. 구조체를 새 변수에 할당하면 구조체가 복사됩니다. 따라서 새 변수와 원래 변수에 동일한 데이터의 두 가지 별도 복사본이 포함됩니다. 한 복사본의 변경 내용은 다른 복사본에 영향을 주지 않습니다.

레코드 형식은 참조 형식(record class) 또는 값 형식(record struct)일 수 있습니다. 레코드 형식에는 값 같음을 지원하는 메서드가 포함되어 있습니다.

일반적으로 클래스는 더 복잡한 동작을 모델링하는 데 사용됩니다. 클래스는 일반적으로 클래스 개체가 만들어진 후 수정할 데이터를 저장합니다. 구조체는 작은 데이터 구조에 가장 적합합니다. 구조체는 일반적으로 구조체가 만들어진 후 수정하지 않을 데이터를 저장합니다. 레코드 형식은 추가 컴파일러 합성 멤버가 있는 데이터 구조입니다. 레코드는 일반적으로 개체가 만들어진 후 수정하지 않을 데이터를 저장합니다.


### 값 형식

값 형식은 System.Object에서 파생되는 System.ValueType에서 파생됩니다. System.ValueType에서 파생되는 형식에는 CLR의 특수 동작이 있습니다. 값 형식 변수에는 해당 값이 직접 포함됩니다. 구조체의 메모리는 변수가 선언된 컨텍스트(무엇이든지)에서 인라인으로 할당됩니다. 값 형식 변수에 대한 별도 힙 할당이나 가비지 수집 오버헤드는 없습니다. 값 형식인 record struct 형식을 선언하고 레코드의 합성 멤버를 포함할 수 있습니다.

값 형식에는 struct 및 enum의 두 가지 범주가 있습니다.

기본 제공 숫자 형식은 구조체이며, 액세스할 수 있는 필드와 메서드가 있습니다.

```C#
// constant field on type byte.
byte b = byte.MaxValue;
```

하지만 단순 비집계 형식처럼 값을 선언하고 변수에 할당합니다.

```C#
byte num = 0xA;
int i = 5;
char c = 'Z';
```

값 형식은 sealed입니다. 값 형식(예: System.Int32)에서 형식을 파생할 수 없습니다. 구조체는 System.ValueType에서만 상속할 수 있기 때문에 사용자 정의 클래스 또는 구조체에서 상속하는 구조체를 정의할 수 없습니다. 그러나 구조체는 하나 이상의 인터페이스를 구현할 수 있습니다. 구조체 형식을 구현하는 인터페이스 형식으로 캐스팅할 수 있습니다. 이 캐스트로 인해 boxing 작업은 관리되는 힙의 참조 형식 개체 내에 구조체를 래핑합니다. Boxing 작업은 System.Object 또는 인터페이스 형식을 입력 매개 변수로 사용하는 메서드에 값 형식을 전달할 때 발생합니다. 자세한 내용은 boxing 및 unboxing을 참조하세요.

struct 키워드를 사용하여 고유한 사용자 지정 값 형식을 만듭니다. 일반적으로 구조체는 다음 예제와 같이 소규모 관련 변수 집합의 컨테이너로 사용됩니다.

```C#
public struct Coords
{
    public int x, y;

    public Coords(int p1, int p2)
    {
        x = p1;
        y = p2;
    }
}
```

구조체에 대한 자세한 내용은 구조 형식을 참조하세요. 값 형식에 대한 자세한 내용은 값 형식을 참조하세요.

값 형식의 다른 범주는 enum입니다. 열거형은 명명된 정수 상수 집합을 정의합니다. 예를 들어, .NET 클래스 라이브러리의 System.IO.FileMode 열거형에는 파일을 여는 방법을 지정하는 명명된 상수 정수 집합이 포함됩니다. 이 패턴은 다음 예제와 같이 정의됩니다.

```C#
public enum FileMode
{
    CreateNew = 1,
    Create = 2,
    Open = 3,
    OpenOrCreate = 4,
    Truncate = 5,
    Append = 6,
}
```

System.IO.FileMode.Create 상수 값은 2입니다. 그러나 이 이름은 소스 코드를 읽는 사람에게 훨씬 더 의미가 있습니다. 따라서 상수 리터럴 숫자 대신 열거형을 사용하는 것이 더 좋습니다. 자세한 내용은 System.IO.FileMode를 참조하세요.

모든 열거형은 System.ValueType에서 상속받는 System.Enum에서 상속됩니다. 구조체에 적용되는 모든 규칙이 열거형에도 적용됩니다. 열거형에 대한 자세한 내용은 열거형 형식을 참조하세요.


### 참조 형식

class, record, delegate, 배열 또는 interface로 정의된 형식은 reference type입니다.

reference type의 변수를 선언하는 경우 해당 형식의 인스턴스로 할당하거나 new 연산자를 사용해 생성할 때까지 값 null을 포함합니다. 다음 예제에서는 클래스의 생성 및 할당을 보여줍니다.

```C#
MyClass myClass = new MyClass();
MyClass myClass2 = myClass;
```

interface는 new 연산자를 사용하여 직접 인스턴스화할 수 없습니다. 대신, 인터페이스를 구현하는 클래스의 인스턴스를 만들고 할당합니다. 다음 예제를 참조하세요.

```C#
MyClass myClass = new MyClass();

// Declare and assign using an existing value.
IMyInterface myInterface = myClass;

// Or create and assign a value in a single statement.
IMyInterface myInterface2 = new MyClass();
```

개체가 만들어지면 관리되는 힙에 메모리가 할당됩니다. 변수는 개체의 위치에 대한 참조만 포함합니다. 관리되는 힙의 형식은 할당될 때와 회수될 때 모두 오버헤드가 필요합니다. ‘가비지 수집’은 회수를 수행하는 CLR의 자동 메모리 관리 기능입니다. 그러나 가비지 수집은 고도로 최적화되고 대부분 시나리오에서 성능 문제를 일으키지 않습니다. 가비지 수집에 대한 자세한 내용은 자동 메모리 관리를 참조하세요.

모든 배열은 해당 요소가 값 형식이더라도 참조 형식입니다. 배열은 System.Array 클래스에서 암시적으로 파생됩니다. 다음 예제와 같이 C#에서 제공하는 단순한 구문을 사용하여 배열을 선언하고 사용할 수 있습니다.

```C#
// Declare and initialize an array of integers.
int[] nums = [1, 2, 3, 4, 5];

// Access an instance property of System.Array.
int len = nums.Length;
```
참조 형식은 상속을 완벽하게 지원합니다. 클래스를 만들 때 sealed로 정의되지 않은 기타 인터페이스 또는 클래스에서 상속할 수 있습니다. 기타 클래스는 직접 만든 클래스에서 상속되고 가상 메서드를 재정의할 수 있습니다. 클래스를 직접 만드는 방법에 대한 자세한 내용은 클래스, 구조체, 레코드를 참조하세요. 상속 및 가상 메서드에 대한 자세한 내용은 상속을 참조하세요.


### 리터럴 값 형식
C#에서는 리터럴 값이 컴파일러에서 형식을 받습니다. 숫자의 끝에 문자를 추가하여 숫자 리터럴의 입력 방법을 지정할 수 있습니다. 예를 들어 값 4.56이 float로 처리되도록 지정하려면 숫자 뒤에 "f" 또는 "F"를 추가합니다(4.56f). 문자를 추가하지 않으면 컴파일러가 리터럴의 형식을 유추합니다. 문자 접미사를 사용하여 지정할 수 있는 형식에 대한 자세한 내용은 정수 숫자 형식 및 부동 소수점 숫자 형식을 참조하세요.

리터럴은 형식화되고 모든 형식이 궁극적으로 System.Object에서 파생되기 때문에 다음과 같은 코드를 작성하고 컴파일할 수 있습니다.

```C#
string s = "The answer is " + 5.ToString();
// Outputs: "The answer is 5"
Console.WriteLine(s);

Type type = 12345.GetType();
// Outputs: "System.Int32"
Console.WriteLine(type);
```


### 제네릭 형식
실제 형식(‘구체적 형식’)에 대한 자리 표시자로 사용되는 하나 이상의 ‘형식 매개 변수’를 사용하여 형식을 선언할 수 있습니다. 클라이언트 코드는 형식의 인스턴스를 만들 때 구체적 형식을 제공합니다. 해당 형식을 제네릭 형식이라고 합니다. 예를 들어 .NET 형식 System.Collections.Generic.List<T>에는 변환을 통해 이름 T가 제공되는 하나의 형식 매개 변수가 있습니다. 형식의 인스턴스를 만들 때 목록에 포함될 개체의 형식(예: string)을 지정합니다.

```C#
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```

형식 매개 변수를 사용하면 각 요소를 개체로 변환할 필요 없이 같은 클래스를 재사용하여 요소 형식을 포함할 수 있습니다. 컴파일러는 컬렉션 요소의 특정 형식을 인식하며, 예를 들어 이전 예제에서 stringList 개체에 정수를 추가하려는 경우 컴파일 시간에 오류를 발생시킬 수 있기 때문에 제네릭 컬렉션 클래스를 강력한 형식의 컬렉션이라고 합니다. 자세한 내용은 제네릭을 참조하세요.


### 암시적 형식, 무명 형식 및 nullable 값 형식

var 키워드를 사용하여 클래스 멤버가 아닌 로컬 변수를 암시적으로 형식화할 수 있습니다. 이 변수는 컴파일 타임에 형식을 받지만 형식은 컴파일러에서 제공됩니다. 자세한 내용은 암시적으로 형식화된 지역 변수를 참조하세요.

저장하거나 메서드 경계 외부로 전달할 의도가 없는 관련 값의 단순 집합에 대한 명명된 형식을 만드는 것이 불편할 수 있습니다. 이 목적으로는 무명 형식을 만들 수 있습니다. 자세한 내용은 무명 형식을 참조하세요.

일반적인 값 형식은 null 값을 가질 수 없습니다. 그러나 형식 뒤에 ?를 추가하면 null 허용 값 형식을 만들 수 있습니다. 예를 들어 int?는 null 값을 가질 수도 있는 int 형식입니다. nullable 값 형식은 제네릭 구조체 형식 System.Nullable<T>의 인스턴스입니다. null 허용 값 형식은 특히 숫자 값이 null일 수 있는 데이터베이스에 데이터를 전달하는 경우에 유용합니다. 자세한 내용은 nullable 값 형식을 참조하세요.


### 컴파일 시간 형식 및 런타임 형식

변수의 컴파일 시간과 런타임 형식은 서로 다를 수 있습니다. 컴파일 시간 형식은 소스 코드에서 선언되거나 유추되는 변수의 형식입니다. 런타임 형식은 해당 변수에서 참조하는 인스턴스의 형식입니다. 다음 예제에서는 이와 같은 두 가지 유형이 동일한 경우가 많습니다.

```C#
string message = "This is a string of characters";
```

하지만 다음 두 가지 예에서 보듯 컴파일 시간 형식이 다른 경우도 있습니다.

```
object anotherMessage = "This is another string of characters";
IEnumerable<char> someCharacters = "abcdefghijklmnopqrstuvwxyz";
```

앞선 두 예제에서 런타임 형식은 string입니다. 컴파일 시간 형식은 첫 번째 줄에서 object, 두 번째 줄에서 IEnumerable<char>입니다.

두 형식이 변수에 대해 다른 경우 컴파일 시간 형식과 런타임 형식이 적용되는 경우를 이해하는 것이 중요합니다. 컴파일 시간 형식에 따라 컴파일러가 수행하는 모든 작업이 결정됩니다. 이러한 컴파일러 동작으로는 메서드 호출 확인, 오버로드 확인 및 사용 가능한 암시적 및 명시적 캐스트가 있습니다. 런타임 형식에 따라 런타임에서 확인되는 모든 작업이 결정됩니다. 이러한 런타임 동작에는 가상 메서드 호출 디스패치, is 및 switch 식 계산, 기타 형식 테스트 API가 포함됩니다. 코드가 형식과 상호 작용하는 방식을 보다 효과적으로 이해하려면 어떤 작업이 어떤 형식에 적용되는지를 알아야 합니다.

---
## 형식을 구성하도록 네임스페이스 선언

네임스페이스는 C# 프로그래밍에서 두 가지 방법으로 많이 사용됩니다. 먼저 .NET은 다음과 같이 네임스페이스를 사용하여 여러 클래스를 구성합니다.

```C#
System.Console.WriteLine("Hello World!");
```

System은 네임스페이스이고 Console은 해당 네임스페이스의 클래스입니다. 다음 예제와 같이 전체 이름이 필요하지 않도록 using 키워드를 사용할 수 있습니다.

```C#
using System;
```

```C#
Console.WriteLine("Hello World!");
```

자세한 내용은 using 지시문을 참조하세요.

```
중요

.NET 6 용 C# 템플릿은 ‘최상위 문’을 사용합니다. .NET 6으로 이미 업그레이드한 경우 애플리케이션이 이 문서의 코드와 일치하지 않을 수 있습니다. 자세한 내용은 최상위 문을 생성하는 새 C# 템플릿을 참조하세요.

.NET 6 SDK는 다음 SDK를 사용하는 프로젝트에 대한 암시적global using 지시문 집합도 추가합니다.

Microsoft.NET.Sdk
Microsoft.NET.Sdk.Web
Microsoft.NET.Sdk.Worker
이러한 암시적 global using 지시문에는 해당 프로젝트 형식의 가장 일반적인 네임스페이스가 포함됩니다.

자세한 내용은 암시적 using 지시문에 대한 문서를 참조하세요.
```

둘째, 고유한 네임스페이스를 선언하면 대규모 프로그래밍 프로젝트에서 클래스 및 메서드 이름의 범위를 제어할 수 있습니다. 다음 예와 같이 네임스페이스 키워드를 사용하여 네임스페이스를 선언합니다.

```C#
namespace SampleNamespace
{
    class SampleClass
    {
        public void SampleMethod()
        {
            System.Console.WriteLine(
                "SampleMethod inside SampleNamespace");
        }
    }
}
```
네임스페이스 이름은 유효한 C# 식별자 이름이어야 합니다.

C# 10부터 다음 예제와 같이 해당 파일에 정의된 모든 형식에 대한 네임스페이스를 선언할 수 있습니다.

```C#
namespace SampleNamespace;

class AnotherSampleClass
{
    public void AnotherSampleMethod()
    {
        System.Console.WriteLine(
            "SampleMethod inside SampleNamespace");
    }
}
```
이 새로운 구문의 장점은 가로 공간과 중괄호를 절약하여 더 간단하다는 것입니다. 이렇게 하면 코드를 더 쉽게 읽을 수 있습니다.

### 네임스페이스 개요

네임스페이스에는 다음과 같은 속성이 있습니다.

 - 대규모 코드 프로젝트를 구성합니다.
 - . 연산자를 사용하여 구분됩니다.
 - using 지시문은 모든 클래스에 대해 네임스페이스 이름을 지정할 필요가 없습니다.
 - global 네임스페이스는 “루트” 네임스페이스입니다. global::System은 항상 .NET System 네임스페이스를 가리킵니다.

---
## 클래스 소개

### 참조 형식
class(으)로 정의된 형식은 참조 형식입니다. 런타임에 참조 형식의 변수를 선언할 때 변수는 new 연산자를 사용하여 클래스의 인스턴스를 명시적으로 만들거나 다음 예제와 같이 다른 곳에서 생성되었을 수 있는 호환되는 형식의 개체를 할당할 때까지 null 값을 포함합니다.

```C#
//Declaring an object of type MyClass.
MyClass mc = new MyClass();

//Declaring another object of the same type, assigning it the value of the first object.
MyClass mc2 = mc;
```
개체가 만들어지면 해당 특정 개체에 대해 관리되는 힙에 충분한 메모리가 할당되고 변수에는 개체 위치에 대한 참조만 포함됩니다. 개체에서 사용하는 메모리는 가비지 수집으로 알려진 CLR의 자동 메모리 관리 기능에 의해 회수됩니다. 가비지 수집에 대한 자세한 내용은 자동 메모리 관리 및 가비지 수집을 참조하세요.

### 클래스 선언

클래스는 다음 예제와 같이 class 키워드와 뒤에 고유 식별자를 사용하여 선언됩니다.

```C#
//[access modifier] - [class] - [identifier]
public class Customer
{
   // Fields, properties, methods and events go here...
}
```
선택적 액세스 한정자는 class 키워드 앞에 옵니다. 이 경우 public(이)가 사용되므로 누구나 이 클래스의 인스턴스를 만들 수 있습니다. 클래스 이름은 class 키워드 뒤에 옵니다. 클래스의 이름은 유효한 C# 식별자 이름이어야 합니다. 정의의 나머지 부분은 동작과 데이터가 정의되는 클래스 본문입니다. 클래스의 필드, 속성, 메서드 및 이벤트를 모두 클래스 멤버라고 합니다.

### 개체 만들기
서로 같은 의미로 사용되는 경우도 있지만 클래스와 개체는 서로 다릅니다. 클래스는 개체의 형식을 정의하지만 개체 자체는 아닙니다. 개체는 클래스에 기반을 둔 구체적 엔터티이고 클래스의 인스턴스라고도 합니다.

다음과 같이 new 키워드와 뒤에 클래스 이름을 사용하여 개체를 만들 수 있습니다.

```C#
Customer object1 = new Customer();
```
클래스 인스턴스가 만들어질 때 개체에 대한 참조가 다시 프로그래머에게 전달됩니다. 이전 예제에서 object1은 Customer에 기반을 둔 개체에 대한 참조입니다. 이 참조는 새 개체를 참조하지만 개체 데이터 자체는 포함하지 않습니다. 실제로 개체를 만들지 않고도 개체 참조를 만들 수 있습니다.

```
Customer object2;
```

이러한 참조를 통해 개체에 액세스하려고 하면 런타임에 실패하므로 개체를 참조하지 않는 개체 참조를 만들지 않는 것이 좋습니다. 새 개체를 만들거나 다음과 같은 기존 개체를 할당하여 개체를 참조하도록 참조를 생성할 수 있습니다.

```C#
Customer object3 = new Customer();
Customer object4 = object3;
```
이 코드에서는 같은 개체를 참조하는 두 개의 개체 참조를 만듭니다. 따라서 object3을 통해 이루어진 모든 개체 변경 내용은 이후 object4 사용 시 반영됩니다. 클래스에 기반을 둔 개체는 참조를 통해 참조되므로 클래스를 참조 형식이라고 합니다.

### 생성자 및 초기화

이전 섹션에서는 클래스 형식을 선언하고 해당 형식의 인스턴스를 만드는 구문을 소개했습니다. 형식의 인스턴스를 만들 때 해당 필드와 속성이 유용한 값으로 초기화되었는지 확인하려고 합니다. 값을 초기화하는 방법에는 여러 가지가 있습니다.

 - 기본값 수용
 - 필드 이니셜라이저
 - 생성자 매개 변수
 - 개체 이니셜라이저

모든 .NET 형식에는 기본값이 있습니다. 일반적으로 이 값은 숫자 형식의 경우 0이고 모든 참조 형식에 대해서는 null입니다. 앱에서 적절한 경우 해당 기본값을 사용할 수 있습니다.

.NET 기본값이 올바른 값이 아닌 경우 필드 이니셜라이저를 사용하여 초기 값을 설정할 수 있습니다.

```C#
public class Container
{
    // Initialize capacity field to a default value of 10:
    private int _capacity = 10;
}
```

호출자가 초기 값을 설정하는 생성자를 정의하여 초기 값을 제공하도록 요구할 수 있습니다.

```C#
public class Container
{
    private int _capacity;

    public Container(int capacity) => _capacity = capacity;
}
```

C# 12부터 클래스 선언의 일부로 기본 생성자를 정의할 수 있습니다.

```C#
public class Container(int capacity)
{
    private int _capacity = capacity;
}
```
클래스 이름에 매개 변수를 추가하면 기본 생성자가 정의됩니다. 이러한 매개 변수는 해당 멤버를 포함하는 클래스 본문에서 사용할 수 있습니다. 이를 사용하여 필드 또는 필요한 다른 곳을 초기화할 수 있습니다.

속성에서 required 한정자를 사용하고 호출자가 개체 이니셜라이저를 사용하여 속성의 초기 값을 설정하도록 허용할 수도 있습니다.

```C#
public class Person
{
    public required string LastName { get; set; }
    public required string FirstName { get; set; }
}
```
required 키워드를 추가하면 호출자가 해당 속성을 new 식의 일부로 설정해야 합니다.

```C#
var p1 = new Person(); // Error! Required properties not set
var p2 = new Person() { FirstName = "Grace", LastName = "Hopper" };
```

---
## 클래스 상속

클래스는 개체 지향 프로그래밍의 기본적인 특성인 ‘상속’을 완전히 지원합니다. 클래스를 만들 때 sealed(으)로 정의되지 않은 다른 클래스에서 상속할 수 있습니다. 다른 클래스는 클래스에서 상속하고 클래스 가상 메서드를 재정의할 수 있습니다. 또한 하나 이상의 인터페이스를 구현할 수 있습니다.

상속은 파생을 통해 수행합니다. 즉, 클래스는 데이터와 동작을 상속하는 소스 기본 클래스를 사용하여 선언됩니다. 다음과 같이 파생 클래스 이름 뒤에 콜론 및 기본 클래스 이름을 추가하여 기본 클래스를 지정합니다.

```C#
public class Manager : Employee
{
    // Employee fields, properties, methods and events are inherited
    // New Manager fields, properties, methods and events go here...
}
```

클래스 선언에 기본 클래스가 포함된 경우 생성자를 제외한 기본 클래스의 모든 멤버를 상속합니다. 자세한 내용은 상속을 참조하세요.

C#의 클래스는 하나의 기본 클래스에서만 직접 상속할 수 있습니다. 그러나 기본 클래스 자체가 다른 클래스에서 상속될 수 있으므로 클래스는 여러 기본 클래스를 간접적으로 상속할 수 있습니다. 또한 클래스는 하나 이상의 인터페이스를 직접 구현할 수 있습니다. 자세한 내용은 인터페이스를 참조하세요.

클래스는 abstract(으)로 선언할 수 있습니다. 추상 클래스에는 시그니처 정의가 있지만 구현이 없는 추상 메서드가 포함됩니다. 추상 클래스는 인스턴스화할 수 없습니다. 추상 클래스는 추상 메서드를 구현하는 파생 클래스를 통해서만 사용할 수 있습니다. 반면, 봉인된 클래스는 다른 클래스에서 파생되는 것을 허용하지 않습니다. 자세한 내용은 Abstract 및 Sealed 클래스와 클래스 멤버를 참조하세요.

클래스 정의는 여러 소스 파일로 분할될 수 있습니다. 자세한 내용은 참조 Partial 클래스 및 메서드합니다.

---
## C#의 레코드 형식 소개

C#의 레코드는 데이터 모델 작업에 특별한 구문과 동작을 제공하는 클래스 또는 구조체입니다. record 한정자는 주 역할이 데이터를 저장하는 형식에 유용한 멤버를 합성하도록 컴파일러에 지시합니다. 이러한 멤버에는 값 같음을 지원하는 ToString() 및 멤버의 오버로드가 포함됩니다.


### 레코드를 사용하는 경우
다음 시나리오에서 클래스 또는 구조체 대신 레코드를 사용하는 것이 좋습니다.

 - 값 같음 여부에 따라 달라지는 데이터 모델을 정의하려는 경우
 - 변경할 수 없는 개체의 형식을 정의하려고 합니다.

#### 값 같음
레코드의 경우 값 같음은 형식이 일치하고 모든 속성 및 필드 값이 일치하는 경우 레코드 형식의 두 변수가 같다는 것을 의미합니다. 클래스와 같은 다른 참조 형식의 경우 같음은 참조 같음을 의미합니다. 즉, 클래스 형식의 두 변수는 같은 개체를 참조하는 경우 같습니다. 두 레코드 인스턴스의 같음을 확인하는 메서드와 연산자에서 값 같음을 사용합니다.

일부 데이터 모델은 값 같음을 사용하지 않습니다. 예를 들어, Entity Framework Core는 참조 같음을 사용하여 개념적으로 하나의 엔터티에 해당하는 엔터티 형식의 인스턴스를 하나만 사용하는지 확인합니다. 이러한 이유로 레코드 형식은 Entity Framework Core에서 엔터티 형식으로 사용하기에 적절하지 않습니다.

#### 불변성
변경할 수 없는 형식은 인스턴스화된 후 개체의 속성 또는 필드 값을 변경하는 것을 방지하는 형식입니다. 불변성은 형식이 스레드로부터 안전해야 하거나 해시 테이블에서 동일하게 남아 있는 해시 코드를 사용하는 경우에 유용할 수 있습니다. 레코드는 변경할 수 없는 형식을 만들고 사용하기 위한 간결한 구문을 제공합니다.

불변성은 모든 데이터 시나리오에 적합하지 않습니다. 예를 들어, Entity Framework Core는 변경할 수 없는 엔터티 형식을 사용한 업데이트를 지원하지 않습니다.

### 레코드가 클래스 및 구조체와 다른 방식
클래스 또는 구조체를 선언하고 인스턴스화하는 동일한 구문을 레코드와 함께 사용할 수 있습니다. class 키워드를 record(으)로 대체하거나 struct 대신 record struct(을)를 사용합니다. 마찬가지로, 상속 관계를 표현하기 위한 동일한 구문은 레코드 클래스에서 지원됩니다. 레코드가 클래스와 다른 점은 다음과 같습니다.

 - 기본 생성자에서 위치 매개 변수를 사용하여 변경할 수 없는 속성을 사용하여 형식을 만들고 인스턴스화할 수 있습니다.
 - 클래스에서 참조 같음 또는 같지 않음(예: Object.Equals(Object) 및 ==)을 나타내는 동일한 메서드와 연산자가 레코드에서 값 같음 또는 같지 않음을 나타냅니다.
 - with 식을 사용하여 선택된 속성에 새 값을 포함하는 변경할 수 없는 개체의 복사본을 만들 수 있습니다.
 - 레코드의 ToString 메서드는 개체 형식 이름과 모든 퍼블릭 속성의 이름과 값을 표시하는 형식 문자열을 만듭니다.
 - 레코드는 다른 레코드에서 상속될 수 있습니다. 레코드는 클래스에서 상속될 수 없으며 클래스는 레코드에서 상속될 수 없습니다.

레코드 구조체는 컴파일러가 같음과 ToString을(를) 위한 메서드를 합성한다는 점에서 구조체와 다릅니다. 컴파일러는 위치 레코드 구조체에 대한 Deconstruct 메서드를 합성합니다.

컴파일러는 record class의 각 기본 생성자 매개 변수에 대한 공개 초기화 전용 속성을 합성합니다. record struct에서 컴파일러는 공개 읽기/쓰기 속성을 합성합니다. 컴파일러는 record 한정자를 포함하지 않는 class 및 struct 형식에서 기본 생성자 매개 변수에 대한 속성을 만들지 않습니다.

### 예제

다음 예제에서는 위치 매개 변수를 사용하여 레코드를 선언하고 인스턴스화하는 퍼블릭 레코드를 정의합니다. 그런 다음 형식 이름 및 속성 값을 출력합니다.

```C#
public record Person(string FirstName, string LastName);

public static class Program
{
    public static void Main()
    {
        Person person = new("Nancy", "Davolio");
        Console.WriteLine(person);
        // output: Person { FirstName = Nancy, LastName = Davolio }
    }

}
```
다음 예제에서는 레코드에서 값 같음을 보여 줍니다.

```C#
public record Person(string FirstName, string LastName, string[] PhoneNumbers);
public static class Program
{
    public static void Main()
    {
        var phoneNumbers = new string[2];
        Person person1 = new("Nancy", "Davolio", phoneNumbers);
        Person person2 = new("Nancy", "Davolio", phoneNumbers);
        Console.WriteLine(person1 == person2); // output: True

        person1.PhoneNumbers[0] = "555-1234";
        Console.WriteLine(person1 == person2); // output: True

        Console.WriteLine(ReferenceEquals(person1, person2)); // output: False
    }
}
```
다음 예제에서는 with 식을 사용하여 변경할 수 없는 개체를 복사하고 속성 중 하나를 변경하는 방법을 보여 줍니다.

```C#
public record Person(string FirstName, string LastName)
{
    public required string[] PhoneNumbers { get; init; }
}

public class Program
{
    public static void Main()
    {
        Person person1 = new("Nancy", "Davolio") { PhoneNumbers = new string[1] };
        Console.WriteLine(person1);
        // output: Person { FirstName = Nancy, LastName = Davolio, PhoneNumbers = System.String[] }

        Person person2 = person1 with { FirstName = "John" };
        Console.WriteLine(person2);
        // output: Person { FirstName = John, LastName = Davolio, PhoneNumbers = System.String[] }
        Console.WriteLine(person1 == person2); // output: False

        person2 = person1 with { PhoneNumbers = new string[1] };
        Console.WriteLine(person2);
        // output: Person { FirstName = Nancy, LastName = Davolio, PhoneNumbers = System.String[] }
        Console.WriteLine(person1 == person2); // output: False

        person2 = person1 with { };
        Console.WriteLine(person1 == person2); // output: True
    }
}
```
---
## 인터페이스 - 여러 형식에 대한 동작 정의

인터페이스에는 비추상 클래스 class 또는 struct이(가) 구현해야 하는 관련 기능 그룹에 대한 정의가 포함되어 있습니다. 인터페이스에서는 구현이 있어야 하는 static 메서드를 정의할 수 있습니다. 인터페이스는 멤버에 대한 기본 구현을 정의할 수 있습니다. 인터페이스에서는 필드, 자동 구현 속성, 속성과 유사한 이벤트 등과 같은 인스턴스 데이터를 선언할 수 없습니다.

예를 들어 인터페이스를 사용하면 여러 소스의 동작을 클래스에 포함할 수 있습니다. 해당 기능은 언어가 클래스의 여러 상속을 지원하지 않기 때문에 C#에서 중요합니다. 또한 구조체는 다른 구조체나 클래스에서 실제로 상속할 수 없기 때문에 구조체에 대한 상속을 시뮬레이트하려는 경우 인터페이스를 사용해야 합니다.

다음 예제와 같이 interface 키워드를 사용하여 인터페이스를 정의합니다.

```C#
interface IEquatable<T>
{
    bool Equals(T obj);
}
```

인터페이스 이름은 유효한 C# 식별자 이름이어야 합니다. 규칙에 따라 인터페이스 이름은 대문자 I로 시작합니다.

IEquatable<T> 인터페이스를 구현하는 모든 클래스나 구조체에는 인터페이스에서 지정한 서명과 일치하는 Equals 메서드에 대한 정의가 포함되어 있어야 합니다. 따라서 IEquatable<T>을 구현하는 클래스를 계산하여 클래스의 인스턴스에서 동일한 클래스의 다른 인스턴스와 동일한지 여부를 확인할 수 있는 Equals 메서드를 포함할 수 있습니다.

IEquatable<T>의 정의에서는 Equals에 대한 구현을 제공하지 않습니다. 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있지만 클래스는 단일 클래스에서만 상속할 수 있습니다.

추상 클래스에 대한 자세한 내용은 추상 및 봉인 클래스와 클래스 멤버를 참조하세요.

인터페이스에는 인스턴스 메서드, 속성, 이벤트, 인덱서 또는 이러한 네 가지 멤버 형식의 조합이 포함될 수 있습니다. 인터페이스에는 정적 생성자, 필드, 상수 또는 연산자가 포함될 수 있습니다. C# 11부터는 필드가 아닌 인터페이스 멤버는 static abstract일 수 있습니다. 인터페이스에는 인스턴스 필드, 인스턴스 생성자 또는 종료자가 포함될 수 없습니다. 인터페이스 멤버는 기본적으로 공용이며, public, protected, internal, private, protected internal 또는 private protected 등의 접근성 한정자를 명시적으로 지정할 수 있습니다. private 멤버에는 기본 구현이 있어야 합니다.

인터페이스 멤버를 구현하려면 구현 클래스의 해당 멤버가 공용이고 비정적이어야 하며 인터페이스 멤버와 동일한 이름 및 서명을 사용해야 합니다.

```
참고

인터페이스가 정적 멤버를 선언하는 경우 해당 인터페이스를 구현하는 형식은 동일한 서명을 가진 정적 멤버를 선언할 수도 있습니다. 멤버는 이를 선언하는 형식에 의해 구분되고 고유하게 식별됩니다. 형식에서 선언된 정적 멤버는 인터페이스에서 선언된 정적 멤버를 재정의하지 않습니다.
```

인터페이스를 구현하는 클래스 또는 구조체는 인터페이스에서 제공하는 기본 구현 없이 선언된 모든 멤버에 대한 구현을 제공해야 합니다. 그러나 기본 클래스에서 인터페이스를 구현하는 경우에는 기본 클래스에서 파생되는 모든 클래스가 해당 구현을 상속합니다.

다음 예제에서는 IEquatable<T> 인터페이스의 구현을 보여 줍니다. 구현 클래스 Car는 Equals 메서드의 구현을 제공해야 합니다.

```C#
public class Car : IEquatable<Car>
{
    public string? Make { get; set; }
    public string? Model { get; set; }
    public string? Year { get; set; }

    // Implementation of IEquatable<T> interface
    public bool Equals(Car? car)
    {
        return (this.Make, this.Model, this.Year) ==
            (car?.Make, car?.Model, car?.Year);
    }
}
```

클래스의 속성 및 인덱서는 인터페이스에 정의된 속성이나 인덱서에 대해 추가 접근자를 정의할 수 있습니다. 예를 들어 인터페이스는 get 접근자가 있는 속성을 선언할 수 있습니다. 인터페이스를 구현하는 클래스는 get 및 set 접근자를 둘 다 사용하는 동일한 속성을 선언할 수 있습니다. 그러나 속성 또는 인덱서에서 명시적 구현을 사용하는 경우에는 접근자가 일치해야 합니다. 명시적 구현에 대한 자세한 내용은 명시적 인터페이스 구현 및 인터페이스 속성(C# 프로그래밍 가이드)을 참조하세요.

인터페이스는 하나 이상의 인터페이스에서 상속할 수 있습니다. 파생 인터페이스는 기본 인터페이스에서 멤버를 상속합니다. 파생 인터페이스를 구현하는 클래스는 파생 인터페이스의 기본 인터페이스 멤버 모두를 포함해 파생 인터페이스의 모든 멤버를 구현해야 합니다. 이 클래스는 파생 인터페이스나 해당하는 기본 인터페이스로 암시적으로 변환될 수 있습니다. 클래스는 상속하는 기본 클래스 또는 다른 인터페이스에서 상속하는 인터페이스를 통해 인터페이스를 여러 번 포함할 수 있습니다. 그러나 클래스는 인터페이스의 구현을 한 번만 제공할 수 있으며 클래스가 인터페이스를 클래스 정의의 일부로 선언하는 경우에만 제공할 수 있습니다(class ClassName : InterfaceName). 인터페이스를 구현하는 기본 클래스를 상속했기 때문에 인터페이스가 상속되는 경우 기본 클래스는 인터페이스 멤버의 구현을 제공합니다. 그러나 파생 클래스는 상속된 구현을 사용하는 대신 가상 인터페이스 멤버를 다시 구현할 수 있습니다. 인터페이스가 메서드의 기본 구현을 선언하면 해당 인터페이스를 구현하는 모든 클래스가 해당 구현을 상속합니다(인터페이스 멤버의 기본 구현에 액세스하려면 클래스 인스턴스를 인터페이스 형식으로 캐스팅해야 합니다).

또한 기본 클래스는 가상 멤버를 사용하여 인터페이스 멤버를 구현할 수 있습니다. 이 경우 파생 클래스는 가상 멤버를 재정의하여 인터페이스 동작을 변경할 수 있습니다. 가상 멤버에 대한 자세한 내용은 다형성을 참조하세요.


### 인터페이스 요약
인터페이스에는 다음과 같은 속성이 있습니다.

 - 8.0 이전 C# 버전에서 인터페이스는 추상 멤버만 있는 추상 기본 클래스와 유사합니다. 인터페이스를 구현하는 클래스 또는 구조체는 해당 멤버를 모두 구현해야 합니다.
 - C# 8.0부터 인터페이스에서 해당 멤버 일부 또는 모두의 기본 구현을 정의할 수 있습니다. 인터페이스를 구현하는 클래스 또는 구조체는 기본 구현이 있는 멤버를 구현할 필요가 없습니다. 자세한 내용은 기본 인터페이스 메서드를 참조하세요.
 - 인터페이스는 직접 인스턴스화할 수 없습니다. 해당 멤버는 인터페이스를 구현하는 클래스 또는 구조체에 의해 구현됩니다.
 - 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다. 클래스는 기본 클래스를 상속할 수 있으며 하나 이상의 인터페이스를 제공할 수도 있습니다.

---
## 제네릭 클래스 및 메서드

제네릭은 .NET에 형식 매개 변수의 개념을 소개합니다. 제네릭을 사용하면 코드에서 클래스 또는 메서드를 사용할 때까지 하나 이상의 형식 매개 변수 사양을 연기하는 클래스와 메서드를 디자인할 수 있습니다. 예를 들어 제네릭 형식 매개 변수 T를 사용하여 여기에 표시된 것처럼, 다른 클라이언트 코드에서 런타임 캐스팅 또는 boxing 작업에 대한 비용이나 위험을 발생하지 않고 사용할 수 있는 단일 클래스를 작성할 수 있습니다.

```C#
// Declare the generic class.
public class GenericList<T>
{
    public void Add(T input) { }
}
class TestGenericList
{
    private class ExampleClass { }
    static void Main()
    {
        // Declare a list of type int.
        GenericList<int> list1 = new GenericList<int>();
        list1.Add(1);

        // Declare a list of type string.
        GenericList<string> list2 = new GenericList<string>();
        list2.Add("");

        // Declare a list of type ExampleClass.
        GenericList<ExampleClass> list3 = new GenericList<ExampleClass>();
        list3.Add(new ExampleClass());
    }
}
```
제네릭 클래스와 메서드는 재사용성, 형식 안전성 및 효율성을 제네릭이 아닌 클래스에서 사용할 수 없는 방식으로 결합합니다. 제네릭 형식 매개 변수는 컴파일 중에 형식 인수로 대체됩니다. 앞의 예제에서 컴파일러는 .로 int바뀝니다T. 제네릭은 컬렉션 및 해당 컬렉션에서 작동하는 메서드에서 가장 자주 사용됩니다. System.Collections.Generic 네임스페이스에는 몇 가지 제네릭 기반 컬렉션 클래스가 있습니다. 비제네릭 컬렉션(예: ArrayList 권장되지 않음)은 호환성 목적으로만 기본. 자세한 내용은 .NET의 제네릭을 참조하세요.

사용자 지정 제네릭 형식 및 메서드를 만들어 형식이 안전하고 효율적인 일반화된 솔루션 및 디자인 패턴을 직접 제공할 수도 있습니다. 다음 코드 예제에서는 데모용으로 간단한 제네릭 연결된 목록 클래스를 보여 줍니다. (대부분의 경우 직접 만드는 대신 .NET에서 제공하는 클래스를 사용해야 List<T> 합니다.) 형식 매개 변수 T 는 구체적인 형식이 일반적으로 목록에 저장된 항목의 형식을 나타내는 데 사용되는 여러 위치에서 사용됩니다.
 - AddHead 메서드에서 메서드 매개 변수의 형식.
 - 중첩 Node 클래스에서 Data 속성의 반환 형식.
 - 중첩 클래스에서 private 멤버 data의 형식.

T는 중첩된 Node 클래스에 사용할 수 있습니다. GenericList<T> 예를 들어 구체적인 형식으로 GenericList<int>인스턴스화되면 각 발생 T 항목이 .로 int바뀝다.

```C#
// type parameter T in angle brackets
public class GenericList<T>
{
    // The nested class is also generic on T.
    private class Node
    {
        // T used in non-generic constructor.
        public Node(T t)
        {
            next = null;
            data = t;
        }

        private Node? next;
        public Node? Next
        {
            get { return next; }
            set { next = value; }
        }

        // T as private member data type.
        private T data;

        // T as return type of property.
        public T Data
        {
            get { return data; }
            set { data = value; }
        }
    }

    private Node? head;

    // constructor
    public GenericList()
    {
        head = null;
    }

    // T as method parameter type:
    public void AddHead(T t)
    {
        Node n = new Node(t);
        n.Next = head;
        head = n;
    }

    public IEnumerator<T> GetEnumerator()
    {
        Node? current = head;

        while (current != null)
        {
            yield return current.Data;
            current = current.Next;
        }
    }
}
```
다음 코드 예제에서는 클라이언트 코드에서 제네릭 GenericList<T> 클래스를 사용하여 정수 목록을 만드는 방법을 보여 줍니다. 형식 인수를 변경하는 경우 다음 코드는 문자열 목록 또는 다른 사용자 지정 형식을 만듭니다.

```C#
class TestGenericList
{
    static void Main()
    {
        // int is the type argument
        GenericList<int> list = new GenericList<int>();

        for (int x = 0; x < 10; x++)
        {
            list.AddHead(x);
        }

        foreach (int i in list)
        {
            System.Console.Write(i + " ");
        }
        System.Console.WriteLine("\nDone");
    }
}
```
```
참고

제네릭 형식은 클래스로 제한되지 않습니다. 앞의 예제에서는 형식을 사용 class 하지만 형식을 포함하여 record 제네릭 interface 및 struct 형식을 정의할 수 있습니다.
```

### 제네릭 개요
 - 제네릭 형식을 사용하여 코드 재사용, 형식 안전성 및 성능을 최대화합니다.
 - 가장 일반적으로 제네릭은 컬렉션 클래스를 만드는 데 사용됩니다.
 - .NET 클래스 라이브러리에는 System.Collections.Generic 네임스페이스의 여러 제네릭 컬렉션 클래스가 포함됩니다. 제네릭 컬렉션은 가능할 때마다 System.Collections 네임스페이스의 ArrayList처럼 클래스 대신 사용되어야 합니다.
 - 사용자 고유의 제네릭 인터페이스, 클래스, 메서드, 이벤트 및 대리자를 만들 수 있습니다.
 - 제네릭 클래스는 특정 데이터 형식의 메서드에 액세스할 수 있도록 제한될 수 있습니다.
 - 리플렉션을 사용하여 제네릭 데이터 형식에 사용되는 형식에 대한 정보를 런타임에 가져올 수 있습니다.

---
## 무명 형식

익명 형식을 사용하면 먼저 명시적으로 형식을 정의할 필요 없이 읽기 전용 속성 집합을 단일 개체로 편리하게 캡슐화할 수 있습니다. 형식 이름은 컴파일러에 의해 생성되며 소스 코드 수준에서 사용할 수 없습니다. 각 속성의 형식은 컴파일러에서 유추합니다.

new 연산자를 개체 이니셜라이저와 함께 사용하여 무명 형식을 만듭니다. 개체 이니셜라이저에 대한 자세한 내용은 개체 및 컬렉션 이니셜라이저를 참조하세요.

다음 예제에서는 Amount 및 Message라는 두 속성으로 초기화된 익명 형식을 보여 줍니다.
```C#
var v = new { Amount = 108, Message = "Hello" };

// Rest the mouse pointer over v.Amount and v.Message in the following
// statement to verify that their inferred types are int and string.
Console.WriteLine(v.Amount + v.Message);
```
일반적으로 무명 형식은 소스 시퀀스에 있는 각 개체의 속성 하위 집합을 반환하기 위해 쿼리 식의 select 절에 사용됩니다. 쿼리에 대한 자세한 내용은 C#의 LINQ를 참조하세요.

익명 형식은 하나 이상의 public 읽기 전용 속성을 포함합니다. 메서드 또는 이벤트와 같은 다른 종류의 클래스 멤버는 유효하지 않습니다. 속성을 초기화하는 데 사용되는 식은 null, 익명 함수 또는 포인터 형식일 수 없습니다.

가장 일반적인 시나리오는 다른 형식의 속성으로 익명 형식을 초기화하는 것입니다. 다음 예제에서는 Product라는 클래스가 있다고 가정합니다. Product 클래스에는 Color 및 Price 속성뿐만 아니라 관심 없는 다른 속성도 포함되어 있습니다. products 변수는 Product 개체의 컬렉션입니다. 익명 형식 선언은 new 키워드로 시작합니다. 선언에서는 Product의 두 속성만 사용하는 새 형식을 초기화합니다. 무명 형식을 사용하면 더 적은 양의 데이터가 쿼리에 반환됩니다.

무명 형식에 멤버 이름을 지정하지 않으면 컴파일러가 무명 형식 멤버에 해당 멤버를 초기화하는 데 사용되는 속성과 동일한 이름을 제공합니다. 앞의 예제에 표시된 것처럼, 식으로 초기화되는 속성의 이름을 제공합니다. 다음 예제에서 익명 형식의 속성 이름은 Color 및 Price입니다.
```C#
var productQuery =
    from prod in products
    select new { prod.Color, prod.Price };

foreach (var v in productQuery)
{
    Console.WriteLine("Color={0}, Price={1}", v.Color, v.Price);
}
```
```
팁

.NET 스타일 규칙 IDE0037을 사용하여 유추된 멤버 이름 또는 명시적 멤버 이름 중 어느 것이 선호되는지를 적용할 수 있습니다.
```
클래스, 구조체 또는 다른 무명 형식과 같은 다른 형식의 개체별로 필드를 정의할 수도 있습니다. 이 작업은 이미 인스턴스화된 사용자 정의 형식을 사용하여 두 개의 무명 형식이 만들어지는 다음 예제와 마찬가지로 이 개체를 보유하는 변수를 사용하여 수행됩니다. 두 경우 모두 무명 형식 shipment 및 shipmentWithBonus의 product 필드는 각 필드의 기본값을 포함하는 Product 형식이 됩니다. 그리고 bonus 필드는 컴파일러에서 만든 무명 형식이 됩니다.

```C#
var product = new Product();
var bonus = new { note = "You won!" };
var shipment = new { address = "Nowhere St.", product };
var shipmentWithBonus = new { address = "Somewhere St.", product, bonus };
```
일반적으로 무명 형식을 사용하여 변수를 초기화할 때는 var을 사용하여 변수를 암시적 형식 지역 변수로 선언합니다. 컴파일러만 익명 형식의 기본 이름에 액세스할 수 있으므로 변수 선언에는 형식 이름을 지정할 수 없습니다. var에 대한 자세한 내용은 암시적 형식 지역 변수를 참조하세요.

다음 예제에 표시된 것처럼, 암시적으로 형식화된 지역 변수와 암시적으로 형식화된 배열을 결합하여 익명으로 형식화된 요소의 배열을 만들 수 있습니다.
```C#
var anonArray = new[] { new { name = "apple", diam = 4 }, new { name = "grape", diam = 1 }};
```
무명 형식은 object에서 직접 파생되고 object를 제외한 어떠한 형식으로도 캐스팅될 수 없는 class 형식입니다. 컴파일러는 애플리케이션에서 해당 익명 형식에 액세스할 수 없더라도 각 익명 형식의 이름을 제공합니다. 공용 언어 런타임의 관점에서 익명 형식은 다른 참조 형식과 다를 바가 없습니다.

어셈블리에서 둘 이상의 익명 개체 이니셜라이저가 순서와 이름 및 형식이 동일한 속성의 시퀀스를 지정하는 경우 컴파일러는 개체를 동일한 형식의 인스턴스로 처리합니다. 이러한 개체는 컴파일러에서 생성된 동일한 형식 정보를 공유합니다.

무명 형식은 with 식 형태로 비파괴적 변경을 지원합니다. 이로 인해 하나 이상의 속성에 새 값이 있는 무명 형식의 새 인스턴스를 만들 수 있습니다.
```C#
var apple = new { Item = "apples", Price = 1.35 };
var onSale = apple with { Price = 0.79 };
Console.WriteLine(apple);
Console.WriteLine(onSale);
```
익명 형식을 가지고 있으므로 필드, 속성, 이벤트 또는 메서드의 반환 형식은 선언할 수 없습니다. 마찬가지로, 익명 형식을 가지고 있으므로 메서드, 속성, 생성자 또는 인덱서의 정식 매개 변수는 선언할 수 없습니다. 무명 형식이나 무명 형식이 포함된 컬렉션을 메서드에 인수로 전달하려면 매개 변수를 object 형식으로 선언하면 됩니다. 그러나 무명 형식에 object를 사용하면 강력한 형식화의 목적이 무효화됩니다. 쿼리 결과를 저장하거나 메서드 경계 외부로 전달해야 하는 경우 익명 형식 대신 일반적인 명명된 구조체 또는 클래스 사용을 고려하세요.

익명 형식에 대한 Equals 및 GetHashCode 메서드는 속성의 Equals 및 GetHashCode 메서드 측면에서 정의되므로 동일한 익명 형식의 두 인스턴스는 해당 속성이 모두 동일한 경우에만 동일합니다.
```
참고

무명 형식의 접근성 수준은 internal이므로 서로 다른 어셈블리에 정의된 두 무명 형식은 동일한 형식이 아닙니다. 따라서 무명 형식의 인스턴스는 모든 속성이 같은 경우에도 서로 다른 어셈블리에 정의된 경우 서로 같을 수 없습니다.
```
무명 형식은 ToString 메서드를 재정의하여 중괄호로 둘러싸인 모든 속성의 이름과 ToString 출력을 연결합니다.
```C#
var v = new { Title = "Hello", Age = 24 };

Console.WriteLine(v.ToString()); // "{ Title = Hello, Age = 24 }"
```

---
## C#의 클래스, 구조체 및 레코드 개요

C#에서 형식(클래스, 구조체 또는 레코드)의 정의는 형식이 수행할 수 있는 작업을 지정하는 청사진과 같습니다. 개체는 기본적으로 청사진에 따라 구성 및 할당된 메모리 블록입니다. 이 문서에서는 이러한 청사진과 해당 기능에 대한 개요를 제공합니다. 이 시리즈의 다음 문서에서는 개체를 소개합니다.

### 캡슐화
캡슐화는 경우에 따라 개체 지향 프로그래밍의 첫 번째 pillar 또는 원리로 인식됩니다. 클래스 또는 구조체는 클래스 또는 구조체 외부의 코드에 각 멤버가 액세스하는 방법을 지정할 수 있습니다. 클래스 또는 어셈블리 외부에서 사용하지 않으려는 메서드 및 변수를 숨겨 코딩 오류 또는 악의적인 악용 가능성을 제한할 수 있습니다. 자세한 내용은 [개체 지향 프로그래밍](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/tutorials/oop) 자습서를 참조하세요.

### 멤버
형식의 ‘멤버’는 모든 메서드, 필드, 상수, 속성, 이벤트를 포함합니다. 다른 언어에는 있지만 C#에는 전역 변수 또는 메서드가 없습니다. 프로그램의 진입점인 Main 메서드까지도 클래스나 구조체 내에 선언되어야 합니다(최상위 문을 사용하는 경우 암시적으로).

다음 목록은 클래스, 구조체 또는 레코드에서 선언될 수 있는 모든 다양한 종류의 멤버입니다.

 - 필드
 - 상수
 - 속성
 - 메서드
 - 생성자
 - 이벤트
 - 종료자
 - 인덱서
 - 연산자
 - 중첩 형식

자세한 내용은 [멤버](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/members)를 참조하세요.

### 접근성
일부 메서드 및 속성은 클라이언트 코드라고 하는 클래스 또는 구조체 외부의 코드에서 호출하거나 액세스할 수 있습니다. 다른 메서드 및 속성은 클래스 또는 구조체 자체에서만 사용할 수 있습니다. 의도된 클라이언트 코드에서만 연결될 수 있도록 코드의 액세스 가능성을 제한하는 것이 중요합니다. 어떻게 형식 및 해당 멤버가 다음 액세스 한정자를 사용하여 클라이언트 코드에 액세스할 수 있는지 지정합니다.

 - public
 - protected
 - internal
 - protected internal
 - private
 - private protected

기본 액세스 가능성은 private입니다.

### 상속
클래스(구조체는 아님)는 상속 개념을 지원합니다. 다른 클래스(‘기본 클래스’라고 함)에서 파생되는 클래스는 생성자와 종료자를 제외하고 기본 클래스의 모든 public, protected, internal 멤버를 자동으로 포함합니다.

클래스를 abstract로 선언할 수도 있습니다. 즉, 하나 이상의 해당 메서드에 구현이 없는 상태를 의미합니다. 추상 클래스는 직접 인스턴스화할 수 없지만 누락된 구현을 제공하는 다른 클래스에 대한 기본 클래스로 사용될 수 있습니다. 다른 클래스가 이 클래스에서 상속 받지 못하게 하려면 클래스를 sealed로 선언할 수도 있습니다.

자세한 내용은 [상속](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/object-oriented/inheritance) 및 [다형성](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/object-oriented/polymorphism)을 참조하세요.

### 인터페이스
클래스, 구조체, 레코드는 여러 인터페이스를 구현할 수 있습니다. 인터페이스에서 구현하는 것은 형식이 해당 인터페이스에 정의된 모든 메서드를 구현한다는 의미입니다. 자세한 내용은 [인터페이스](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/interfaces)를 참조하세요.

### 제네릭 형식
클래스, 구조체 및 레코드는 하나 이상의 형식 매개 변수로 정의할 수 있습니다. 클라이언트 코드는 형식의 인스턴스를 만들 때 형식을 제공합니다. 예를 들어 System.Collections.Generic 네임스페이스의 List<T> 클래스는 하나의 형식 매개 변수로 정의됩니다. 클라이언트 코드는 List<string> 또는 List<int>의 인스턴스를 만들어 목록에 포함될 형식을 지정합니다. 자세한 내용은 [제네릭](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/generics)을 참조하세요.

### 정적 형식
클래스(구조체나 레코드는 아님)를 static(으)로 선언할 수 있습니다. static 클래스는 static 멤버만 포함할 수 있고 new 키워드로 인스턴스화할 수 없습니다. 프로그램이 로드될 때 클래스의 단일 복사본만 메모리에 로드되고 해당 멤버는 클래스 이름을 통해 액세스됩니다. 클래스, 구조체 및 레코드에는 static 멤버가 포함될 수 있습니다. 자세한 내용은 [정적 클래스 및 정적 클래스 멤버](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)를 참조하세요.

### 중첩 형식
클래스, 구조체 또는 레코드는 다른 클래스, 구조체 또는 레코드 내에 중첩될 수 있습니다. 자세한 내용은 [중첩 형식](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/nested-types)을 참조하세요.

### 부분 형식(Partial Type)
하나의 코드 파일 및 별도 코드 파일의 다른 부분에서 클래스, 구조체 또는 메서드의 부분을 정의할 수 있습니다. 자세한 내용은 참조 [Partial 클래스 및 메서드](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)합니다.

### 개체 이니셜라이저
해당 속성에 값을 할당하여 클래스 또는 구조체 개체와 개체 컬렉션을 인스턴스화하고 초기화할 수 있습니다. 자세한 내용은 [개체 이니셜라이저를 사용하여 개체를 초기화하는 방법](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer)을 참조하세요.

### 익명 형식
명명된 클래스를 만드는 것이 불편하거나 필요하지 않은 상황에서는 무명 형식을 사용합니다. 무명 형식은 명명된 데이터 멤버로 정의됩니다. 자세한 내용은 [무명 형식](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/anonymous-types)을 참조하세요.

### 확장명 메서드
별도의 형식을 만들어 파생 클래스를 만들지 않고도 클래스를 “확장”할 수 있습니다. 해당 형식에는 원래 형식에 속한 것처럼 호출할 수 있는 메서드가 포함됩니다. 자세한 내용은 [확장 메서드](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)를 참조하세요.

### 암시적 형식 지역 변수
클래스 또는 구조체 메서드 내에서 암시적 형식 지정을 사용하여 컴파일러가 컴파일 시간에 변수의 형식을 결정하도록 할 수 있습니다. 자세한 내용은 [var(C# 참조)](https://learn.microsoft.com/ko-kr/dotnet/csharp/language-reference/statements/declarations#implicitly-typed-local-variables)을 참조하세요.

### 레코드
클래스 또는 구조체에 record 한정자를 추가할 수 있습니다. 레코드는 값 기반 같음을 위한 기본 제공 동작이 있는 형식입니다. 레코드(record class 또는 record struct)는 다음과 같은 기능을 제공합니다.

 - 변경할 수 없는 속성을 사용하여 참조 형식을 만드는 간결한 구문
 - 값 같음 레코드 종류의 두 변수는 레코드 종류가 동일한 경우와 모든 필드에 대해 두 레코드의 값이 같은 경우에 같습니다. 클래스는 참조 같음을 사용합니다. 한 클래스 형식의 두 변수가 같은 개체를 참조하면 두 변수가 동일합니다.
 - 비파괴적 변형을 위한 간결한 구문 with 식을 사용하면 기존 인스턴스의 복사본이지만 지정된 속성 값이 변경된 새 레코드 인스턴스를 만들 수 있습니다.
 - 표시를 위한 기본 제공 형식 ToString 메서드는 레코드 형식 이름과 퍼블릭 속성의 이름 및 값을 출력합니다.
 - 레코드 클래스의 상속 계층 구조에 대한 지원. 레코드 클래스는 상속을 지원합니다. 레코드 구조체는 상속을 지원하지 않습니다.

자세한 내용은 [레코드](https://learn.microsoft.com/ko-kr/dotnet/csharp/language-reference/builtin-types/record)를 참조하세요.

---
## 개체 - 형식의 인스턴스 만들기

클래스 또는 구조체 정의는 형식이 수행할 수 있는 작업을 지정하는 청사진과 비슷합니다. 개체는 기본적으로 청사진에 따라 구성 및 할당된 메모리 블록입니다. 프로그램에서 동일한 클래스의 많은 개체를 만들 수 있습니다. 개체를 인스턴스라고도 하며, 명명된 변수나 배열 또는 컬렉션에 저장할 수 있습니다. 클라이언트 코드는 이러한 변수를 사용하여 메서드를 호출하고 개체의 공용 속성에 액세스하는 코드입니다. C#과 같은 개체 지향 언어에서 일반적인 프로그램은 동적으로 상호 작용하는 여러 개체로 구성됩니다.

```
참고

정적 형식은 여기에 설명된 것과 다르게 동작합니다. 자세한 내용은 static 클래스 및 static 클래스 멤버를 참조하세요.
```

### 구조체 인스턴스 및 클래스 인스턴스
클래스는 참조 형식이므로 클래스 개체의 변수는 관리되는 힙의 개체 주소에 대한 참조를 포함합니다. 동일한 형식의 두 번째 변수가 첫 번째 변수에 할당된 경우 두 변수 모두 해당 주소의 개체를 참조합니다. 이 점은 이 문서의 뒷부분에서 자세히 설명합니다.

클래스 인스턴스는 new 연산자를 사용하여 생성됩니다. 다음 예제에서 Person은 형식이고 person1 및 person2는 해당 형식의 인스턴스 또는 개체입니다.
```C#
using System;

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
    // Other properties, methods, events...
}

class Program
{
    static void Main()
    {
        Person person1 = new Person("Leopold", 6);
        Console.WriteLine("person1 Name = {0} Age = {1}", person1.Name, person1.Age);

        // Declare new person, assign person1 to it.
        Person person2 = person1;

        // Change the name of person2, and person1 also changes.
        person2.Name = "Molly";
        person2.Age = 16;

        Console.WriteLine("person2 Name = {0} Age = {1}", person2.Name, person2.Age);
        Console.WriteLine("person1 Name = {0} Age = {1}", person1.Name, person1.Age);
    }
}
/*
    Output:
    person1 Name = Leopold Age = 6
    person2 Name = Molly Age = 16
    person1 Name = Molly Age = 16
*/
```
구조체는 값 형식이므로 구조체 개체의 변수는 전체 개체의 복사본을 포함합니다. 다음 예제와 같이 new 연산자를 사용하여 구조체 인스턴스를 만들 수도 있지만 필수는 아닙니다.

```C#
using System;

namespace Example
{
    public struct Person
    {
        public string Name;
        public int Age;
        public Person(string name, int age)
        {
            Name = name;
            Age = age;
        }
    }

    public class Application
    {
        static void Main()
        {
            // Create  struct instance and initialize by using "new".
            // Memory is allocated on thread stack.
            Person p1 = new Person("Alex", 9);
            Console.WriteLine("p1 Name = {0} Age = {1}", p1.Name, p1.Age);

            // Create  new struct object. Note that  struct can be initialized
            // without using "new".
            Person p2 = p1;

            // Assign values to p2 members.
            p2.Name = "Spencer";
            p2.Age = 7;
            Console.WriteLine("p2 Name = {0} Age = {1}", p2.Name, p2.Age);

            // p1 values remain unchanged because p2 is  copy.
            Console.WriteLine("p1 Name = {0} Age = {1}", p1.Name, p1.Age);
        }
    }
    /*
        Output:
        p1 Name = Alex Age = 9
        p2 Name = Spencer Age = 7
        p1 Name = Alex Age = 9
    */
}
```

p1 및 p2 둘 다에 대한 메모리가 스레드 스택에서 할당됩니다. 해당 메모리는 선언된 형식 또는 메서드와 함께 회수됩니다. 이는 할당 시 구조체가 복사되는 이유 중 하나입니다. 반면, 클래스 인스턴스에 할당된 메모리는 개체에 대한 모든 참조가 범위를 벗어날 때 공용 언어 런타임에 의해 자동으로 회수(가비지 수집)됩니다. C++에서처럼 클래스 개체를 결정적으로 삭제할 수는 없습니다. .NET의 가비지 수집에 대한 자세한 내용은 가비지 수집을 참조하세요.

```
참고

관리되는 힙의 메모리 할당 및 할당 취소는 공용 언어 런타임에서 고도로 최적화되어 있습니다. 대부분의 경우 힙에서 클래스 인스턴스를 할당하는 경우와 스택에서 구조체 인스턴스를 할당하는 경우의 성능 차이는 크지 않습니다.
```

### 개체 ID와 값 같음 비교
두 개체가 같은지를 비교하는 경우 먼저 두 변수가 메모리에서 동일한 개체를 나타내는지 또는 해당 필드 값이 하나 이상 같은지를 알고 싶은 것인지 구분해야 합니다. 값을 비교하려는 경우 개체가 값 형식(구조체) 또는 참조 형식(클래스, 대리자, 배열)의 인스턴스인지 고려해야 합니다.

 - 두 클래스 인스턴스가 메모리의 동일한 위치를 참조하는지 확인하려면(즉, ID가 같음) 정적 Object.Equals 메서드를 사용합니다. System.Object은 사용자 정의 구조체 및 클래스를 포함하여 모든 값 형식 및 참조 형식에 대한 암시적 기본 클래스입니다.
 - 두 구조체 인스턴스의 인스턴스 필드 값이 같은지 확인하려면 ValueType.Equals 메서드를 사용합니다. 모든 구조체가 System.ValueType에서 암시적으로 상속하기 때문에 다음 예제와 같이 개체에서 직접 메서드를 호출합니다.
```C#
// Person is defined in the previous example.

//public struct Person
//{
//    public string Name;
//    public int Age;
//    public Person(string name, int age)
//    {
//        Name = name;
//        Age = age;
//    }
//}

Person p1 = new Person("Wallace", 75);
Person p2 = new Person("", 42);
p2.Name = "Wallace";
p2.Age = 75;

if (p2.Equals(p1))
    Console.WriteLine("p2 and p1 have the same values.");

// Output: p2 and p1 have the same values.
``` 
Equals의 System.ValueType 구현에서는 경우에 따라 boxing 및 리플렉션을 사용합니다. 형식에 따라 효율적인 같음 알고리즘을 제공하는 방법에 대한 자세한 내용은 형식의 값 같음을 정의하는 방법을 참조하세요. 레코드는 같음을 위해 값 의미 체계를 사용하는 참조 형식입니다.
 - 두 클래스 인스턴스의 필드 값이 같은지 확인하기 위해 Equals 메서드 또는 == 연산자를 사용할 수 있습니다. 그러나 클래스가 해당 형식의 개체에 대해 "같음"이 무엇을 의미하는지의 사용자 지정 정의를 제공하도록 재정의 또는 오버로드한 경우에만 사용합니다. 클래스는 IEquatable<T> 인터페이스 또는 IEqualityComparer<T> 인터페이스도 구현할 수 있습니다. 두 인터페이스 모두 값이 같은지를 테스트하는 데 사용할 수 있는 메서드를 제공합니다. Equals을 재정의하는 고유한 클래스를 디자인하는 경우 형식의 값 같음을 정의하는 방법 및 Object.Equals(Object)에 명시된 지침을 따라야 합니다.

---
## 상속 - 형식을 파생하여 보다 전문화된 동작을 만듭니다.

캡슐화 및 다형성과 함께 상속은 개체 지향 프로그래밍의 세 가지 주요 특징 중 하나입니다. 상속을 사용하면 다른 클래스에 정의된 동작을 다시 사용, 확장 및 수정하는 새 클래스를 만들 수 있습니다. 멤버가 상속되는 클래스를 기본 클래스라고 하고 해당 멤버를 상속하는 클래스를 파생 클래스라고 합니다. 파생 클래스에는 직접적인 기본 클래스가 하나만 있을 수 있습니다. 그러나 상속은 전이됩니다. ClassC가 ClassB에서 파생된 클래스이고 ClassB가 ClassA에서 파생된 클래스이면 ClassC는 ClassB와 ClassA에서 선언된 멤버를 상속합니다.
```
참고

구조체는 상속을 지원하지 않지만 인터페이스를 구현할 수 있습니다.
```
파생 클래스는 개념적 측면에서 기본 클래스의 특수화입니다. 예를 들어 기본 클래스 Animal이 있는 경우 Mammal이라는 하나의 파생 클래스와 Reptile이라는 다른 파생 클래스가 있을 수 있습니다. Mammal은 Animal이고 Reptile은 Animal이지만 각 파생 클래스는 기본 클래스의 서로 다른 특수화를 나타냅니다.

인터페이스 선언은 그 멤버의 기본 구현을 정의할 수 있습니다. 이러한 구현은 파생된 인터페이스에 의해, 그리고 해당 인터페이스를 구현하는 클래스에 의해 상속됩니다. 기본 인터페이스 메서드에 대한 자세한 내용은 인터페이스 문서를 참조하세요.

다른 클래스에서 파생할 클래스를 정의하는 경우 파생 클래스는 해당 생성자와 종료자를 제외하고 기본 클래스의 모든 멤버를 암시적으로 얻게 됩니다. 파생 클래스는 기본 클래스에서 코드를 다시 구현하지 않고 다시 사용합니다. 파생 클래스에서 더 많은 멤버를 추가할 수 있습니다. 파생 클래스는 기본 클래스의 기능을 확장합니다.

다음 그림은 일부 비즈니스 프로세스의 작업 항목을 나타내는 WorkItem 클래스를 보여 줍니다. 모든 클래스와 마찬가지로, System.Object에서 파생되고 해당 메서드를 모두 상속합니다. WorkItem은 자체 멤버 6개를 추가합니다. 생성자는 상속되지 않으므로 이러한 멤버에는 생성자도 포함됩니다. ChangeRequest 클래스는 WorkItem에서 상속되며 특정 종류의 작업 항목을 나타냅니다. ChangeRequest는 WorkItem 및 Object에서 상속하는 멤버에 둘 이상의 멤버를 추가합니다. 고유한 생성자를 추가해야 하며, originalItemID도 추가합니다. originalItemID 속성을 사용하면 ChangeRequest 인스턴스를 변경 요청이 적용되는 원래 WorkItem에 연결할 수 있습니다.

![](../img/07_CSharp_기초/class-inheritance-diagram.png)

다음 예제에서는 앞의 그림에서 보여 주는 클래스 관계가 C#에서 어떻게 표현되는지를 보여 줍니다. 또한 이 예제에서 WorkItem은 가상 메서드 Object.ToString을 재정의하는 방법과 ChangeRequest 클래스가 메서드의 WorkItem 구현을 상속하는 방법을 보여 줍니다. 첫 번째 블록은 클래스를 정의합니다.

```C#
// WorkItem implicitly inherits from the Object class.
public class WorkItem
{
    // Static field currentID stores the job ID of the last WorkItem that
    // has been created.
    private static int currentID;

    //Properties.
    protected int ID { get; set; }
    protected string Title { get; set; }
    protected string Description { get; set; }
    protected TimeSpan jobLength { get; set; }

    // Default constructor. If a derived class does not invoke a base-
    // class constructor explicitly, the default constructor is called
    // implicitly.
    public WorkItem()
    {
        ID = 0;
        Title = "Default title";
        Description = "Default description.";
        jobLength = new TimeSpan();
    }

    // Instance constructor that has three parameters.
    public WorkItem(string title, string desc, TimeSpan joblen)
    {
        this.ID = GetNextID();
        this.Title = title;
        this.Description = desc;
        this.jobLength = joblen;
    }

    // Static constructor to initialize the static member, currentID. This
    // constructor is called one time, automatically, before any instance
    // of WorkItem or ChangeRequest is created, or currentID is referenced.
    static WorkItem() => currentID = 0;

    // currentID is a static field. It is incremented each time a new
    // instance of WorkItem is created.
    protected int GetNextID() => ++currentID;

    // Method Update enables you to update the title and job length of an
    // existing WorkItem object.
    public void Update(string title, TimeSpan joblen)
    {
        this.Title = title;
        this.jobLength = joblen;
    }

    // Virtual method override of the ToString method that is inherited
    // from System.Object.
    public override string ToString() =>
        $"{this.ID} - {this.Title}";
}

// ChangeRequest derives from WorkItem and adds a property (originalItemID)
// and two constructors.
public class ChangeRequest : WorkItem
{
    protected int originalItemID { get; set; }

    // Constructors. Because neither constructor calls a base-class
    // constructor explicitly, the default constructor in the base class
    // is called implicitly. The base class must contain a default
    // constructor.

    // Default constructor for the derived class.
    public ChangeRequest() { }

    // Instance constructor that has four parameters.
    public ChangeRequest(string title, string desc, TimeSpan jobLen,
                         int originalID)
    {
        // The following properties and the GetNexID method are inherited
        // from WorkItem.
        this.ID = GetNextID();
        this.Title = title;
        this.Description = desc;
        this.jobLength = jobLen;

        // Property originalItemID is a member of ChangeRequest, but not
        // of WorkItem.
        this.originalItemID = originalID;
    }
}
```
다음 블록은 기본 클래스와 파생 클래스를 사용하는 방법을 보여 줍니다.

```C#
// Create an instance of WorkItem by using the constructor in the
// base class that takes three arguments.
WorkItem item = new WorkItem("Fix Bugs",
                            "Fix all bugs in my code branch",
                            new TimeSpan(3, 4, 0, 0));

// Create an instance of ChangeRequest by using the constructor in
// the derived class that takes four arguments.
ChangeRequest change = new ChangeRequest("Change Base Class Design",
                                        "Add members to the class",
                                        new TimeSpan(4, 0, 0),
                                        1);

// Use the ToString method defined in WorkItem.
Console.WriteLine(item.ToString());

// Use the inherited Update method to change the title of the
// ChangeRequest object.
change.Update("Change the Design of the Base Class",
    new TimeSpan(4, 0, 0));

// ChangeRequest inherits WorkItem's override of ToString.
Console.WriteLine(change.ToString());
/* Output:
    1 - Fix Bugs
    2 - Change the Design of the Base Class
*/
```

### 추상 메서드와 가상 메서드
기본 클래스가 메서드를 virtual로 선언하는 경우 파생 클래스가 자체 구현으로 메서드를 override할 수 있습니다. 기본 클래스가 멤버를 abstract로 선언하는 경우 해당 클래스에서 직접 상속되는 모든 비추상 클래스에서 메서드를 재정의해야 합니다. 파생 클래스 자체가 abstract인 경우 직접 구현하지 않고 추상 멤버를 상속합니다. 추상 멤버 및 가상 멤버는 개체 지향 프로그래밍의 두 번째 주요 특징인 다형성의 기초가 됩니다. 자세한 내용은 다형성을 참조하세요.

### 추상 기본 클래스
new 연산자를 사용한 직접 인스턴스화를 방지하려는 경우 클래스를 abstract로 선언할 수 있습니다. 추상 클래스는 해당 클래스에서 새 클래스가 파생되는 경우에만 사용할 수 있습니다. 추상 클래스에는 그 자체가 abstract로 선언된 메서드 시그니처가 하나 이상 포함될 수 있습니다. 이러한 시그니처는 매개 변수와 반환 값을 지정하지만 구현(메서드 본문)이 없습니다. 추상 클래스는 추상 멤버를 포함하지 않아도 됩니다. 그러나 클래스에 추상 멤버가 포함되지 않은 경우 클래스 자체를 abstract로 선언해야 합니다. 그 자체가 추상이 아닌 파생 클래스는 추상 기본 클래스에서 모든 추상 메서드에 대한 구현을 제공해야 합니다.

### 인터페이스
‘인터페이스’는 멤버 집합을 정의하는 참조 형식입니다. 인터페이스를 구현하는 모든 클래스와 구조체는 해당 멤버 집합을 구현해야 합니다. 인터페이스는 임의 또는 모든 구성원에 대한 기본 구현을 정의할 수 있습니다. 하나의 직접 기본 클래스에서만 파생할 수 있는 경우에도 클래스에서 여러 인터페이스를 구현할 수 있습니다.

인터페이스는 “is a” 관계가 없을 수도 있는 클래스에 대해 특정 기능을 정의하는 데 사용됩니다. 예를 들어 System.IEquatable<T> 인터페이스는 모든 클래스 또는 구조체에 의해 구현되어 해당 형식의 두 개체가 동일한지 여부를(해당 형식에서 정의하는 동일성 기준에 따라) 확인할 수 있습니다. IEquatable<T>은 기본 클래스와 파생 클래스 간에 존재하는 것과 같은 “is a” 관계(예: Mammal is an Animal)를 암시하지 않습니다. 자세한 내용은 인터페이스를 참조하세요.

### 추가 파생 방지
클래스는 자신이나 멤버를 sealed로 선언하여 다른 클래스가 해당 클래스나 그 멤버에서 상속할 수 없도록 할 수 있습니다.

### 파생 클래스의 기본 클래스 멤버 숨기기
파생 클래스는 동일한 이름과 시그니처로 멤버를 선언하여 기본 클래스 멤버를 숨길 수 있습니다. new 한정자를 사용하여 멤버가 기본 멤버를 재정의하지 않음을 명시적으로 나타낼 수 있습니다. new의 사용은 필수가 아니지만 new를 사용하지 않을 경우 컴파일러 경고가 생성됩니다. 자세한 내용은 Override 및 New 키워드를 사용하여 버전 관리 및 Override 및 New 키워드를 사용해야 하는 경우를 참조하세요.

---
## 다형성

다형성은 흔히 캡슐화와 상속의 뒤를 이어 개체 지향 프로그래밍의 세 번째 특징으로 일컬어집니다. 다형성은 "여러 형태"를 의미하는 그리스어 단어이며 다음과 같은 두 가지 고유한 측면을 가집니다.

 - 런타임에 파생 클래스의 개체가 메서드 매개 변수 및 컬렉션 또는 배열과 같은 위치에서 기본 클래스의 개체로 처리될 수 있습니다. 이러한 다형성이 발생하면 개체의 선언된 형식이 더 이상 해당 런타임 형식과 같지 않습니다.
 - 기본 클래스는 가상메서드를 정의 및 구현할 수 있으며, 파생 클래스는 이러한 가상 메서드를 재정의할 수 있습니다. 즉, 파생 클래스는 고유한 정의 및 구현을 제공합니다. 런타임에 클라이언트 코드에서 메서드를 호출하면 CLR은 개체의 런타임 형식을 조회하고 가상 메서드의 해당 재정의를 호출합니다. 소스 코드에서 기본 클래스에 대해 메서드를 호출하여 메서드의 파생 클래스 버전이 실행되도록 할 수 있습니다.

가상 메서드를 사용하면 동일한 방식으로 관련 개체 그룹에 대한 작업을 수행할 수 있습니다. 예를 들어, 사용자가 그리기 화면에서 다양한 종류의 도형을 만들 수 있는 그리기 애플리케이션이 있다고 가정합니다. 컴파일 시간에는 사용자가 어떤 특정한 유형의 도형을 만들 것인지 알 수 없습니다. 그러나 애플리케이션은 만들어지는 다양한 모든 형식의 도형을 추적해야 하며, 사용자의 마우스 작업에 따라 이러한 도형을 업데이트해야 합니다. 다음과 같은 기본 두 단계로 다형성을 사용하여 이 문제를 해결할 수 있습니다.

 1. 각 특정 도형 클래스가 공통 기본 클래스에서 파생되는 클래스 계층 구조를 만듭니다.
 2. 가상 메서드를 사용하여 기본 클래스 메서드에 대한 단일 호출을 통해 모든 파생 클래스에 대해 적절한 메서드를 호출합니다.

먼저, Shape라는 기본 클래스를 만들고 Rectangle, Circle 및 Triangle과 같은 파생 클래스를 만듭니다. Shape 클래스에 Draw라는 가상 메서드를 제공하고, 각 파생 클래스에서 이를 재정의하여 클래스가 나타내는 특정 도형을 그립니다. List<Shape> 개체를 만들고 이 개체에 Circle, Triangle및 Rectangle을 추가합니다.

```C#
public class Shape
{
    // A few example members
    public int X { get; private set; }
    public int Y { get; private set; }
    public int Height { get; set; }
    public int Width { get; set; }

    // Virtual method
    public virtual void Draw()
    {
        Console.WriteLine("Performing base class drawing tasks");
    }
}

public class Circle : Shape
{
    public override void Draw()
    {
        // Code to draw a circle...
        Console.WriteLine("Drawing a circle");
        base.Draw();
    }
}
public class Rectangle : Shape
{
    public override void Draw()
    {
        // Code to draw a rectangle...
        Console.WriteLine("Drawing a rectangle");
        base.Draw();
    }
}
public class Triangle : Shape
{
    public override void Draw()
    {
        // Code to draw a triangle...
        Console.WriteLine("Drawing a triangle");
        base.Draw();
    }
}
```
그리기 화면을 업데이트하려면 foreach 루프를 사용하여 목록을 반복하고 목록의 각 Shape 개체에 대해 Draw 메서드를 호출합니다. 목록의 각 개체에 선언된 형식 Shape가 있더라도 이는 호출될 런타임 형식(각 파생 클래스에 있는 메서드의 재정의된 버전)입니다.
```C#
// Polymorphism at work #1: a Rectangle, Triangle and Circle
// can all be used wherever a Shape is expected. No cast is
// required because an implicit conversion exists from a derived
// class to its base class.
var shapes = new List<Shape>
{
    new Rectangle(),
    new Triangle(),
    new Circle()
};

// Polymorphism at work #2: the virtual method Draw is
// invoked on each of the derived classes, not the base class.
foreach (var shape in shapes)
{
    shape.Draw();
}
/* Output:
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
*/
```

C#에서 모든 형식은 사용자 정의 형식을 포함한 모든 형식이 Object에서 파생되므로 다형 형식입니다.


### 다형성 개요
#### 가상 멤버
파생 클래스가 기본 클래스에서 상속되는 경우 기본 클래스의 모든 멤버가 포함됩니다. 기본 클래스에 선언된 모든 동작은 파생 클래스의 일부입니다. 이로써 파생 클래스의 개체를 기본 클래스의 개체로 처리할 수 있습니다. 액세스 한정자(public, protected, private 등)는 파생 클래스 구현에서 해당 멤버에 액세스할 수 있는지 여부를 결정합니다. 가상 메서드는 디자이너에게 파생 클래스의 동작에 대한 다양한 선택권을 제공합니다.

 - 파생 클래스가 기본 클래스의 가상 멤버를 재정의하여 새로운 동작을 정의할 수 있습니다.
 - 파생 클래스는 재정의하지 않고 가장 가까운 기본 클래스 메서드를 상속할 수 있어 기존 동작을 유지하지만 추가 파생 클래스가 메서드를 재정의할 수 있습니다.
 - 파생 클래스가 기본 클래스 구현을 숨기는 멤버의 새로운 비가상 구현을 정의할 수 있습니다.

파생 클래스는 기본 클래스 멤버가 virtual 또는 abstract로 선언된 경우에만 기본 클래스 멤버를 재정의할 수 있습니다. 파생 멤버는 override 키워드를 사용하여 메서드가 가상 호출에 참여하도록 되어 있음을 명시적으로 나타내야 합니다. 다음 코드는 예제를 제공합니다.

```C#
public class BaseClass
{
    public virtual void DoWork() { }
    public virtual int WorkProperty
    {
        get { return 0; }
    }
}
public class DerivedClass : BaseClass
{
    public override void DoWork() { }
    public override int WorkProperty
    {
        get { return 0; }
    }
}
```
필드는 가상일 수 없습니다. 메서드, 속성, 이벤트, 인덱서만 가상일 수 있습니다. 파생 클래스가 가상 멤버를 재정의하면 해당 멤버는 해당 클래스의 인스턴스가 기본 클래스의 인스턴스로 액세스되는 경우에도 호출됩니다. 다음 코드는 예제를 제공합니다.

```C#
DerivedClass B = new DerivedClass();
B.DoWork();  // Calls the new method.

BaseClass A = B;
A.DoWork();  // Also calls the new method.
```
가상 메서드 및 속성을 통해 파생 클래스는 메서드의 기본 클래스 구현을 사용할 필요 없이 기본 클래스를 확장할 수 있습니다. 자세한 내용은 Override 및 New 키워드를 사용하여 버전 관리를 참조하세요. 인터페이스는 구현이 파생 클래스에 남겨진 메서드 또는 메서드 집합을 정의하는 또 다른 방법을 제공합니다.

#### 새 멤버로 기본 클래스 멤버 숨기기
파생 클래스가 기본 클래스의 멤버와 동일한 이름을 갖는 멤버를 갖도록 하려면 new 키워드를 사용하여 기본 클래스 멤버를 숨길 수 있습니다. new 키워드는 바꿀 클래스 멤버의 반환 형식 앞에 배치됩니다. 다음 코드는 예제를 제공합니다.

```C#
public class BaseClass
{
    public void DoWork() { WorkField++; }
    public int WorkField;
    public int WorkProperty
    {
        get { return 0; }
    }
}

public class DerivedClass : BaseClass
{
    public new void DoWork() { WorkField++; }
    public new int WorkField;
    public new int WorkProperty
    {
        get { return 0; }
    }
}
```
파생 클래스의 인스턴스를 기본 클래스의 인스턴스로 캐스팅하여 숨겨진 기본 클래스 멤버를 클라이언트 코드에서 액세스할 수 있습니다. 예시:

```C#
DerivedClass B = new DerivedClass();
B.DoWork();  // Calls the new method.

BaseClass A = (BaseClass)B;
A.DoWork();  // Calls the old method.
```
#### 파생 클래스가 가상 멤버를 재정의하지 못하도록 설정
가상 멤버는 가상 멤버와 원래 가상 멤버를 선언한 클래스에서 선언된 클래스의 개수와 관계없이 가상으로 유지됩니다. 클래스 A가 가상 멤버를 선언하고, 클래스 B가 A에서 파생되며, 클래스 C가 B에서 파생되면 클래스 C는 클래스 B가 해당 멤버에 대한 재정의를 선언했는지 여부와 관계없이 가상 멤버를 상속하며, 해당 가상 멤버를 재정의할 수 있습니다. 다음 코드는 예제를 제공합니다.
```C#
public class A
{
    public virtual void DoWork() { }
}
public class B : A
{
    public override void DoWork() { }
}
```
파생 클래스는 재정의를 sealed로 선언하여 가상 상속을 중지할 수 있습니다. 가상 상속을 중지하려면 클래스 멤버 선언에서 override 키워드 앞에 sealed 키워드를 배치해야 합니다. 다음 코드는 예제를 제공합니다.

```C#
public class C : B
{
    public sealed override void DoWork() { }
}
```
앞의 예제에서 DoWork 메서드는 C에서 파생된 모든 클래스에 대해 더 이상 가상이 아닙니다. 그러나 이 메서드는 C의 인스턴스가 형식 B 또는 형식 A로 캐스팅되더라도 여전히 C의 인스턴스에 대해서는 가상입니다. sealed 메서드는 다음 예제에서처럼 new 키워드를 사용하여 파생 클래스로 바꿀 수 있습니다.

```C#
public class D : C
{
    public new void DoWork() { }
}
```
이 경우 형식 D 변수를 사용하여 D에 대해 DoWork을 호출하면 새 DoWork가 호출됩니다. 형식 C, B 또는 A 변수를 사용하여 D의 인스턴스에 액세스하면 DoWork에 대한 호출은 가상 상속의 규칙을 따라 해당 호출을 클래스 C에 대한 DoWork의 구현으로 라우팅합니다.

#### 파생 클래스에서 기본 클래스 가상 멤버에 액세스
메서드 또는 속성을 바꾸었거나 재정의한 파생 클래스는 계속해서 base 키워드를 사용하여 기본 클래스에 대한 메서드 또는 속성에 액세스할 수 있습니다. 다음 코드는 예제를 제공합니다.

```C#
public class Base
{
    public virtual void DoWork() {/*...*/ }
}
public class Derived : Base
{
    public override void DoWork()
    {
        //Perform Derived's work here
        //...
        // Call DoWork on base class
        base.DoWork();
    }
}
```
자세한 내용은 base를 참조하세요.

```
참고

가상 멤버는 base를 사용하여 자체 구현에서 해당 멤버의 기본 클래스 구현을 호출하는 것이 좋습니다. 기본 클래스 동작이 발생하도록 하면 파생 클래스가 파생 클래스에 대한 동작 구현에 집중할 수 있습니다. 기본 클래스 구현이 호출되지 않는 경우 해당 동작이 기본 클래스의 동작과 호환되도록 하는 것은 파생 클래스의 책임입니다.
```

---
## 패턴 일치 개요


‘패턴 일치’는 식에 특정 특징이 있는지 확인하기 위해 테스트하는 기법입니다. C# 패턴 일치는 식을 테스트하고 식이 일치하는 경우 작업을 수행하기 위한 보다 간결한 구문을 제공합니다. "is expression"은 패턴 일치를 지원하여 식을 테스트하고 해당 식의 결과에 새 변수를 조건부로 선언합니다. “switch 식”을 사용하면 식의 처음 일치 패턴을 기준으로 작업을 수행할 수 있습니다. 이 두 식은 다양한 ‘패턴’ 어휘를 지원합니다.

이 문서에서는 패턴 일치를 사용할 수 있는 시나리오를 살펴봅니다. 이러한 기법은 코드의 가독성과 정확성을 향상하는 데 사용할 수 있습니다. 적용할 수 있는 모든 패턴에 대해 알아보려면 언어 참조에서 [패턴](https://learn.microsoft.com/ko-kr/dotnet/csharp/language-reference/operators/patterns)에 관한 문서를 살펴보세요.

### null 검사

패턴 일치에서 가장 널리 사용되는 시나리오는 값이 null이 아닌지 확인하는 것입니다. 다음 예제를 사용하여 null이 아닌지를 테스트할 때 null 허용 값 형식을 테스트하고 기본 형식으로 변환할 수 있습니다.

```C#
int? maybe = 12;

if (maybe is int number)
{
    Console.WriteLine($"The nullable int 'maybe' has the value {number}");
}
else
{
    Console.WriteLine("The nullable int 'maybe' doesn't hold a value");
}
```

위 코드는 변수의 형식을 테스트하고 여기에 새 값을 할당하는 ‘선언 패턴’입니다. 이 언어의 규칙 덕분에 다른 언어보다 이 기법을 더 안전하게 사용할 수 있습니다. 변수 number는 액세스만 가능하며 if 절의 실제 부분에 할당됩니다. else 절에서나 if 블록 뒤에서 등 다른 곳에서 액세스하려고 하면 컴파일러가 오류를 발생시킵니다. 이 패턴은 == 연산자를 사용하지 않으므로 형식이 == 연산자를 오버로드하는 경우에도 작동합니다. 따라서 이것은 not 패턴을 추가하여 null 참조를 확인하는 이상적인 방법이 됩니다.

```C#
string? message = ReadMessageOrDefault();

if (message is not null)
{
    Console.WriteLine(message);
}
```

앞에 나온 예제에서는 ‘상수 패턴’을 사용하여 변수를 null에 비교했습니다. not은 부정된 패턴이 일치하지 않는 경우 일치하는 ‘논리 패턴’입니다.

### 형식 테스트

패턴 일치를 위해 사용되는 또 다른 일반적인 방법은 변수가 지정된 형식과 일치하는지 테스트하는 것입니다. 예를 들어, 다음 코드는 변수가 null이 아닌 값인지 테스트하며 System.Collections.Generic.IList<T> 인터페이스를 구현합니다. 이 경우 해당 목록의 ICollection<T>.Count 속성을 사용하여 중간 인덱스 찾기를 수행합니다. 선언 패턴은 변수의 컴파일 시간 형식과 관계없이 null 값과 일치하지 않습니다. 아래 코드는 IList을 구현하지 않는 형식으로부터 보호하는 것 외에도 null로부터 보호합니다.

```C#
public static T MidPoint<T>(IEnumerable<T> sequence)
{
    if (sequence is IList<T> list)
    {
        return list[list.Count / 2];
    }
    else if (sequence is null)
    {
        throw new ArgumentNullException(nameof(sequence), "Sequence can't be null.");
    }
    else
    {
        int halfLength = sequence.Count() / 2 - 1;
        if (halfLength < 0) halfLength = 0;
        return sequence.Skip(halfLength).First();
    }
}
```

switch 식에 동일한 테스트를 적용하여 변수를 여러 형식에 대해 테스트할 수 있습니다. 이 정보는 특정 런타임 형식을 기반으로 더 나은 알고리즘을 만드는 데 사용할 수 있습니다.

### 불연속 값 비교

변수를 테스트하여 특정 값에 대한 일치 항목을 찾을 수도 있습니다. 다음 코드는 열거형에서 선언된 모든 가능한 값에 대해 값을 테스트하는 예를 보여 줍니다.

```C#
public State PerformOperation(Operation command) =>
   command switch
   {
       Operation.SystemTest => RunDiagnostics(),
       Operation.Start => StartSystem(),
       Operation.Stop => StopSystem(),
       Operation.Reset => ResetToReady(),
       _ => throw new ArgumentException("Invalid enum value for command", nameof(command)),
   };
```
위의 예제에서는 열거형의 값을 기준으로 디스패치된 메서드를 보여 주었습니다. 마지막 _ 케이스는 모든 값과 일치하는 ‘무시 패턴’입니다. 이 케이스는 값이 정의된 enum 값 중 어느 것과도 일치하지 않는 경우의 오류 조건을 처리합니다. 해당 스위치 암을 생략하면 컴파일러는 패턴 식이 가능한 모든 입력 값을 처리하지 않는다고 경고합니다. 런타임에는 검사 대상 개체가 switch 암(arm) 중 어느 것과도 일치하지 않는 경우 switch 식이 예외를 throw합니다. 일련의 열거형 값 대신 숫자형 상수를 사용할 수 있습니다. 명령을 나타내는 상수 문자열에 대해서도 이와 비슷한 기법을 사용할 수 있습니다.

```C#
public State PerformOperation(string command) =>
   command switch
   {
       "SystemTest" => RunDiagnostics(),
       "Start" => StartSystem(),
       "Stop" => StopSystem(),
       "Reset" => ResetToReady(),
       _ => throw new ArgumentException("Invalid string value for command", nameof(command)),
   };
```
위의 예제에서는 동일한 알고리즘을 보여 주지만 열거형 대신 문자열 값을 사용합니다. 이 시나리오는 애플리케이션이 일반적인 데이터 형식이 아닌 텍스트 명령에 응답하는 경우에 사용할 수 있습니다. C# 11부터 다음 샘플과 같이 Span<char> 또는 ReadOnlySpan<char>을(를) 사용하여 상수 문자열 값을 테스트할 수도 있습니다.

```C#
public State PerformOperation(ReadOnlySpan<char> command) =>
   command switch
   {
       "SystemTest" => RunDiagnostics(),
       "Start" => StartSystem(),
       "Stop" => StopSystem(),
       "Reset" => ResetToReady(),
       _ => throw new ArgumentException("Invalid string value for command", nameof(command)),
   };
```
위의 모든 예제에서 ‘무시 패턴’으로 모든 입력이 처리되었는지 확인할 수 있습니다. 컴파일러는 모든 가능한 입력값이 처리되었는지 확인함으로써 이 작업을 도와줍니다.

### 관계형 패턴

‘관계형 패턴’을 사용하여 값이 상수와 비교되는 방식을 테스트할 수 있습니다. 예를 들어, 다음 코드는 화씨 온도를 기준으로 물의 상태를 반환합니다.

```C#
string WaterState(int tempInFahrenheit) =>
    tempInFahrenheit switch
    {
        (> 32) and (< 212) => "liquid",
        < 32 => "solid",
        > 212 => "gas",
        32 => "solid/liquid transition",
        212 => "liquid / gas transition",
    };
```

위 코드는 두 관계형 패턴이 모두 일치하는지 확인하는 결합 and논리 패턴도 보여 줍니다. 분리 or 패턴을 사용하여 둘 중 어느 패턴이 일치하는지 확인할 수도 있습니다. 두 관계형 패턴은 괄호로 묶여 있습니다. 어떤 패턴도 명확성을 위해 괄호로 묶을 수 있습니다. 마지막 두 개의 switch 암(arm)은 녹는점 케이스와 끓는점 케이스를 처리합니다. 이 두 암(arm)이 없으면 모든 가능한 입력이 처리되지 않았다는 경고가 발생합니다.

앞의 코드는 또한 컴파일러가 패턴 일치 식에 대해 제공하는 또 다른 중요한 기능을 보여 줍니다. 모든 입력 값을 처리하지 않으면 컴파일러가 경고합니다. 또한 스위치 암에 대한 패턴이 이전 패턴에서 적용되는 경우에도 컴파일러에서 경고를 발생합니다. 이를 통해 스위치 식을 자유롭게 리팩터링하고 순서를 조정할 수 있습니다. 동일한 식을 작성하는 또 다른 방법은 다음과 같습니다.

```C#
string WaterState2(int tempInFahrenheit) =>
    tempInFahrenheit switch
    {
        < 32 => "solid",
        32 => "solid/liquid transition",
        < 212 => "liquid",
        212 => "liquid / gas transition",
        _ => "gas",
};
```

이전 샘플의 주요 단원과 다른 리팩터링 또는 다시 정렬은 컴파일러가 코드가 가능한 모든 입력을 처리하는지 유효성을 검사한다는 것입니다.

### 여러 입력

지금까지 다룬 모든 패턴은 하나의 입력을 검사. 개체의 여러 속성을 검사하는 패턴을 작성할 수도 있습니다. 다음 Order 레코드를 살펴보겠습니다.

```C#
public record Order(int Items, decimal Cost);
```
위의 위치 지정 레코드 형식은 명시적 위치에 두 개의 멤버를 선언합니다. 먼저 Items가 표시되고 그다음에 주문의 Cost가 표시됩니다. 자세한 내용은 레코드를 참조하세요.

다음 코드는 품목의 개수와 주문의 금액을 검사하여 할인 가격을 계산합니다.
```C#
public decimal CalculateDiscount(Order order) =>
    order switch
    {
        { Items: > 10, Cost: > 1000.00m } => 0.10m,
        { Items: > 5, Cost: > 500.00m } => 0.05m,
        { Cost: > 250.00m } => 0.02m,
        null => throw new ArgumentNullException(nameof(order), "Can't calculate discount on null order"),
        var someObject => 0m,
    };
```
처음 두 개의 암(arm)은 Order의 두 속성을 검사합니다. 세 번째 암(arm)은 비용만 검사합니다. 그다음 암(arm)은 null을 검사하고 마지막 암(arm)은 다른 모든 값의 일치 여부를 확인합니다. Order 형식이 적합한 Deconstruct 메서드를 정의하는 경우, 패턴에서 속성 이름을 생략하고 분해를 사용하여 속성을 검사할 수 있습니다.

```C#
public decimal CalculateDiscount(Order order) =>
    order switch
    {
        ( > 10,  > 1000.00m) => 0.10m,
        ( > 5, > 50.00m) => 0.05m,
        { Cost: > 250.00m } => 0.02m,
        null => throw new ArgumentNullException(nameof(order), "Can't calculate discount on null order"),
        var someObject => 0m,
    };
```

위의 코드는 속성이 식에 대해 분해되는 ‘위치 지정 패턴’을 보여 줍니다.

### 목록 패턴

목록 패턴을 사용하여 목록 또는 배열의 요소를 확인할 수 있습니다. 목록 패턴은 시퀀스의 모든 요소에 패턴을 적용하는 방법을 제공합니다. 또한 무시 항목 패턴(_)을 적용하여 모든 요소와 일치시키거나 슬라이스 패턴을 적용하여 0개 이상의 요소와 일치시킬 수 있습니다.

목록 패턴은 데이터가 일반 구조를 따르지 않는 경우 유용한 도구입니다. 패턴 일치를 사용하여 개체 집합으로 변환하는 대신 데이터의 셰이프와 값을 테스트할 수 있습니다.

은행 거래가 포함된 텍스트 파일에서 발췌한 다음을 고려합니다.

```
출력

04-01-2020, DEPOSIT,    Initial deposit,            2250.00
04-15-2020, DEPOSIT,    Refund,                      125.65
04-18-2020, DEPOSIT,    Paycheck,                    825.65
04-22-2020, WITHDRAWAL, Debit,           Groceries,  255.73
05-01-2020, WITHDRAWAL, #1102,           Rent, apt, 2100.00
05-02-2020, INTEREST,                                  0.65
05-07-2020, WITHDRAWAL, Debit,           Movies,      12.57
04-15-2020, FEE,                                       5.55
```

CSV 형식이지만 일부 행에는 다른 행보다 더 많은 열이 있습니다. 처리의 경우 더 나쁜 경우 형식의 WITHDRAWAL 한 열에 사용자가 생성한 텍스트가 포함되며 텍스트에 쉼표가 포함될 수 있습니다. 값 프로세스 데이터를 이 형식으로 캡처하기 위한 dis카드 패턴, 상수 패턴 및 var 패턴을 포함하는 목록 패턴입니다.

```C#
decimal balance = 0m;
foreach (string[] transaction in ReadRecords())
{
    balance += transaction switch
    {
        [_, "DEPOSIT", _, var amount]     => decimal.Parse(amount),
        [_, "WITHDRAWAL", .., var amount] => -decimal.Parse(amount),
        [_, "INTEREST", var amount]       => decimal.Parse(amount),
        [_, "FEE", var fee]               => -decimal.Parse(fee),
        _                                 => throw new InvalidOperationException($"Record {string.Join(", ", transaction)} is not in the expected format!"),
    };
    Console.WriteLine($"Record: {string.Join(", ", transaction)}, New balance: {balance:C}");
}
```

앞의 예제에서는 각 요소가 행의 한 필드인 문자열 배열을 가져옵니다. 두 번째 필드의 switch 식 키로, 트랜잭션의 종류와 나머지 열 수를 결정합니다. 각 행은 데이터가 올바른 형식인지 확인합니다. 취소 패턴(_)은 트랜잭션 날짜와 함께 첫 번째 필드를 건너뜁니다. 두 번째 필드는 트랜잭션 형식과 일치합니다. 나머지 요소 일치 항목은 크기가 있는 필드로 건너뜁니다. 마지막 일치 항목은 var 패턴을 사용하여 양의 문자열 표현을 캡처합니다. 식은 잔액을 추가하거나 빼는 양을 계산합니다.

목록 패턴을 사용하면 데이터 요소 시퀀스의 모양과 일치시킬 수 있습니다. 요소의 위치와 일치하도록 무시 항목 및 조각 패턴을 사용합니다. 다른 패턴을 사용하여 개별 요소에 대한 특성을 일치시킬 수 있습니다.

이 문서에서는 C#의 패턴 일치를 사용하여 작성할 수 있는 여러 종류의 코드를 살펴보았습니다. 다음 문서에서는 시나리오에서 패턴을 사용하는 더 많은 예제와 사용할 수 있는 패턴의 전체 어휘를 보여 줍니다.

---
## 무시 항목 - C# 기본 사항


무시 항목은 애플리케이션 코드에서 의도적으로 사용을 하지 않는 자리 표시자입니다. 무시 항목은 할당되지 않은 변수에 해당하므로 값을 가지지 않습니다. 무시 항목은 식의 결과를 무시하려고 한 사용자 의도를 사용자 코드를 읽는 다른 사용자와 컴파일러에 전달합니다. 식의 결과, 하나 이상의 튜플 식 멤버, 메서드에 대한 out 매개 변수 또는 패턴 일치 식의 대상을 무시해야 할 수 있습니다.

무시 항목은 코드의 의도를 명확하게 합니다. 무시 항목은 코드에서 변수를 사용하지 않는다는 것을 나타냅니다. 또한 코드의 가독성 및 유지 관리를 향상시킵니다.

변수가 무시 항목임을 지정하려면 변수에 밑줄(_)을 이름으로 할당합니다. 예를 들어 다음 메서드 호출은 첫 번째 및 두 번째 값이 무시 항목인 튜플을 반환합니다. area는 이전에 선언된 변수로, GetCityInformation에서 반환된 세 번째 구성 요소로 설정됩니다.
```C#
(_, _, area) = city.GetCityInformation(cityName);
```
무시 항목을 사용하여 람다 식의 사용하지 않는 입력 매개 변수를 지정할 수 있습니다. 자세한 내용은 람다 식 문서의 람다 식 입력 매개 변수 섹션을 참조하세요.

_이(가) 유효한 무시 항목인 경우, 이 값을 검색하거나 할당 작업에서 사용하려고 하면 “이름 '_' 이 현재 컨텍스트에 없습니다”라는 컴파일러 오류 CS0103이 생성됩니다. 이 오류는 _에 값이 할당되어 있지 않고 스토리지 위치도 할당되어 있지 않을 수 있기 때문입니다. 실제 변수인 경우에는 이전 예제에서처럼 2개 이상의 값을 무시할 수 없습니다.

### 튜플 및 개체 분해

무시 항목은 튜플을 작업할 때 애플리케이션 코드에 튜플 요소 중 일부만 사용하고 일부는 무시하는 경우에 유용합니다. 예를 들어, 다음 QueryCityDataForYears 메서드는 도시의 이름, 도시의 면적, 연도, 해당 연도의 도시 인구, 두 번째 연도, 해당 두 번째 연도의 도구 인구를 포함하는 튜플을 반환합니다. 이 예제는 이러한 두 연도 사이의 인구 변화를 보여 줍니다. 튜플에서 사용 가능한 데이터 중 도시 면적에는 관심이 없고 디자인 타임에 도시 이름과 두 날짜를 알고 있습니다. 따라서 튜플에 저장된 두 가지 인구 값에만 관심이 있고 나머지 값은 무시 항목으로 처리할 수 있습니다.

```C#
var (_, _, _, pop1, _, pop2) = QueryCityDataForYears("New York City", 1960, 2010);

Console.WriteLine($"Population change, 1960 to 2010: {pop2 - pop1:N0}");

static (string, double, int, int, int, int) QueryCityDataForYears(string name, int year1, int year2)
{
    int population1 = 0, population2 = 0;
    double area = 0;

    if (name == "New York City")
    {
        area = 468.48;
        if (year1 == 1960)
        {
            population1 = 7781984;
        }
        if (year2 == 2010)
        {
            population2 = 8175133;
        }
        return (name, area, year1, population1, year2, population2);
    }

    return ("", 0, 0, 0, 0, 0);
}
// The example displays the following output:
//      Population change, 1960 to 2010: 393,149
```

무시 항목을 사용한 튜플 분해에 대한 자세한 내용은 튜플 및 기타 형식 분해를 참조하세요.

클래스, 구조체 또는 인터페이스의 Deconstruct 메서드로도 개체에서 특정 데이터 집합을 검색 및 분해할 수 있습니다. 분해된 값의 하위 집합만으로 작업하려는 경우 무시 항목을 사용할 수 있습니다. 다음 예제에서는 Person 개체를 4개의 문자열(이름, 성, 도시 및 주)로 분해하지만 성과 주는 무시합니다.

```C#
using System;

namespace Discards
{
    public class Person
    {
        public string FirstName { get; set; }
        public string MiddleName { get; set; }
        public string LastName { get; set; }
        public string City { get; set; }
        public string State { get; set; }

        public Person(string fname, string mname, string lname,
                      string cityName, string stateName)
        {
            FirstName = fname;
            MiddleName = mname;
            LastName = lname;
            City = cityName;
            State = stateName;
        }

        // Return the first and last name.
        public void Deconstruct(out string fname, out string lname)
        {
            fname = FirstName;
            lname = LastName;
        }

        public void Deconstruct(out string fname, out string mname, out string lname)
        {
            fname = FirstName;
            mname = MiddleName;
            lname = LastName;
        }

        public void Deconstruct(out string fname, out string lname,
                                out string city, out string state)
        {
            fname = FirstName;
            lname = LastName;
            city = City;
            state = State;
        }
    }
    class Example
    {
        public static void Main()
        {
            var p = new Person("John", "Quincy", "Adams", "Boston", "MA");

            // Deconstruct the person object.
            var (fName, _, city, _) = p;
            Console.WriteLine($"Hello {fName} of {city}!");
            // The example displays the following output:
            //      Hello John of Boston!
        }
    }
}
```

무시 항목을 사용한 사용자 정의 형식 분해에 대한 자세한 내용은 튜플 및 기타 형식 분해를 참조하세요.

### switch를 사용한 패턴 일치

‘무시 패턴’은 switch 식을 사용한 패턴 일치에서 사용할 수 있습니다. null을 포함한 모든 식은 무시 패턴과 항상 일치합니다.

다음 예제에서는 switch 식을 사용하여 개체가 IFormatProvider 구현을 제공하고 개체가 null인지 테스트하는지를 결정하는 ProvidesFormatInfo 메서드를 정의합니다. 또한 무시 패턴을 사용하여 다른 형식의 null이 아닌 개체도 처리합니다.

```C#
object?[] objects = [CultureInfo.CurrentCulture,
                   CultureInfo.CurrentCulture.DateTimeFormat,
                   CultureInfo.CurrentCulture.NumberFormat,
                   new ArgumentException(), null];
foreach (var obj in objects)
    ProvidesFormatInfo(obj);

static void ProvidesFormatInfo(object? obj) =>
    Console.WriteLine(obj switch
    {
        IFormatProvider fmt => $"{fmt.GetType()} object",
        null => "A null object reference: Its use could result in a NullReferenceException",
        _ => "Some object type without format information"
    });
// The example displays the following output:
//    System.Globalization.CultureInfo object
//    System.Globalization.DateTimeFormatInfo object
//    System.Globalization.NumberFormatInfo object
//    Some object type without format information
//    A null object reference: Its use could result in a NullReferenceException
```

### out 매개 변수를 사용한 메서드 호출

Deconstruct 메서드를 호출하여 사용자 정의 형식(클래스, 구조체 또는 인터페이스의 인스턴스)를 분해할 때 개별 out 인수의 값을 무시할 수 있습니다. 하지만 어느 메서드든 out 매개 변수를 사용하여 호출할 때 out 인수의 값을 무시할 수도 있습니다.

다음 예제에서는 DateTime.TryParse(String, out DateTime) 메서드를 호출하여 날짜의 문자열 표현이 현재 문화권에 유효한지 확인합니다. 이 예제에서는 날짜 문자열의 유효성 검사에만 관심이 있고 이 문자열의 구문 검사를 통한 날짜 추출에는 관심이 없으므로 메서드의 out 인수는 무시 항목입니다.

```C#
string[] dateStrings = ["05/01/2018 14:57:32.8", "2018-05-01 14:57:32.8",
                      "2018-05-01T14:57:32.8375298-04:00", "5/01/2018",
                      "5/01/2018 14:57:32.80 -07:00",
                      "1 May 2018 2:57:32.8 PM", "16-05-2018 1:00:32 PM",
                      "Fri, 15 May 2018 20:10:57 GMT"];
foreach (string dateString in dateStrings)
{
    if (DateTime.TryParse(dateString, out _))
        Console.WriteLine($"'{dateString}': valid");
    else
        Console.WriteLine($"'{dateString}': invalid");
}
// The example displays output like the following:
//       '05/01/2018 14:57:32.8': valid
//       '2018-05-01 14:57:32.8': valid
//       '2018-05-01T14:57:32.8375298-04:00': valid
//       '5/01/2018': valid
//       '5/01/2018 14:57:32.80 -07:00': valid
//       '1 May 2018 2:57:32.8 PM': valid
//       '16-05-2018 1:00:32 PM': invalid
//       'Fri, 15 May 2018 20:10:57 GMT': invalid
```

### 독립 실행형 무시 항목

독립 실행형 무시 항목을 사용하여 무시할 변수를 지정할 수 있습니다. 한 가지 일반적인 용도는 인수가 null이 아니도록 할당을 사용하는 것입니다. 다음 코드에서는 무시 항목을 사용하여 할당을 적용합니다. 할당의 오른쪽은 null 병합 연산자를 사용하여 인수가 null일 때 System.ArgumentNullException을 throw합니다. 코드에 할당 결과가 필요하지 않으므로 할당이 무시됩니다. 식에서 null 검사를 강제로 수행합니다. 무시 항목은 할당 결과가 필요하지 않거나 사용되지 않는다는 의도를 명확하게 합니다.

```C#
public static void Method(string arg)
{
    _ = arg ?? throw new ArgumentNullException(paramName: nameof(arg), message: "arg can't be null");

    // Do work with arg.
}
```

다음 예제에서는 독립 실행형 무시 항목을 사용하여 비동기 작업에서 반환되는 Task개체를 무시합니다. 작업을 할당하면 작업이 완료되려고 할 때 throw되는 예외가 표시되지 않습니다. Task을(를) 무시하고 해당 비동기 작업에서 생성되는 모든 오류를 무시하려고 하는 의도가 명확히 드러납니다.

```C#
private static async Task ExecuteAsyncMethods()
{
    Console.WriteLine("About to launch a task...");
    _ = Task.Run(() =>
    {
        var iterations = 0;
        for (int ctr = 0; ctr < int.MaxValue; ctr++)
            iterations++;
        Console.WriteLine("Completed looping operation...");
        throw new InvalidOperationException();
    });
    await Task.Delay(5000);
    Console.WriteLine("Exiting after 5 second delay");
}
// The example displays output like the following:
//       About to launch a task...
//       Completed looping operation...
//       Exiting after 5 second delay
```
작업을 무시 항목에 할당하지 않으면 다음 코드는 컴파일러 경고를 생성합니다.

```C#
private static async Task ExecuteAsyncMethods()
{
    Console.WriteLine("About to launch a task...");
    // CS4014: Because this call is not awaited, execution of the current method continues before the call is completed.
    // Consider applying the 'await' operator to the result of the call.
    Task.Run(() =>
    {
        var iterations = 0;
        for (int ctr = 0; ctr < int.MaxValue; ctr++)
            iterations++;
        Console.WriteLine("Completed looping operation...");
        throw new InvalidOperationException();
    });
    await Task.Delay(5000);
    Console.WriteLine("Exiting after 5 second delay");
```

```
참고

디버거를 사용하여 위의 두 샘플 중 하나를 실행하면 예외가 throw될 때 디버거가 프로그램을 중지합니다. 연결된 디버거가 없으면 두 경우 모두 예외가 자동으로 무시됩니다.
```

_은 유효한 식별자이기도 합니다. 지원되는 컨텍스트 외부에서 사용하면 _은 무시 항목이 아니라 유효한 변수로 처리됩니다. _이라는 식별자가 이미 범위 내에 있는 경우 _을 독립 실행형 무시 항목으로 사용하면 다음과 같은 결과가 발생할 수 있습니다.

 - 범위 내 _ 변수 값을 실수로 수정하여 의도한 무시 항목의 값 할당. 예시:
```C#
private static void ShowValue(int _)
{
   byte[] arr = [0, 0, 1, 2];
   _ = BitConverter.ToInt32(arr, 0);
   Console.WriteLine(_);
}
 // The example displays the following output:
 //       33619968
 ```
  - 형식 안전성 위반으로 인한 컴파일러 오류. 예시:
```C#
private static bool RoundTrips(int _)
{
   string value = _.ToString();
   int newValue = 0;
   _ = Int32.TryParse(value, out newValue);
   return _ == newValue;
}
// The example displays the following compiler error:
//      error CS0029: Cannot implicitly convert type 'bool' to 'int'
```
 - 컴파일러 오류 CS0136, “이름이 ‘_’인 지역 또는 매개 변수는 이 범위에서 선언될 수 없습니다. 해당 이름이 지역 또는 매개 변수를 정의하기 위해 바깥쪽 지역 범위에서 사용되었습니다.” 예를 들어:
```C#
public void DoSomething(int _)
{
 var _ = GetValue(); // Error: cannot declare local _ when one is already in scope
}
// The example displays the following compiler error:
// error CS0136:
//       A local or parameter named '_' cannot be declared in this scope
//       because that name is used in an enclosing local scope
//       to define a local or parameter
```
---
## 튜플 및 기타 형식 분해

튜플은 메서드 호출에서 여러 값을 검색할 수 있는 간단한 방법을 제공합니다. 하지만 튜플을 검색한 후 튜플의 개별 요소를 처리해야 합니다. 다음 예에서 볼 수 있듯이 요소별로 작업하는 것은 번거롭습니다. QueryCityData 메서드는 3개의 튜플을 반환하고 각 요소는 별도의 작업을 통해 변수에 할당됩니다.

```C#
public class Example
{
    public static void Main()
    {
        var result = QueryCityData("New York City");

        var city = result.Item1;
        var pop = result.Item2;
        var size = result.Item3;

         // Do something with the data.
    }

    private static (string, int, double) QueryCityData(string name)
    {
        if (name == "New York City")
            return (name, 8175133, 468.48);

        return ("", 0, 0);
    }
}
```
개체에서 여러 필드 및 속성 값을 검색하는 작업도 똑같이 번거로울 수 있습니다. 멤버별로 변수에 필드 또는 속성 값을 할당해야 하기 때문입니다.

단일 분해 작업으로 튜플에서 여러 요소를 검색하거나 개체에서 여러 필드, 속성 및 계산된 값을 검색할 수 있습니다. 튜플을 분해하려면 해당 요소를 개별 변수에 할당합니다. 개체를 분해할 때는 선택한 값을 개별 변수에 할당합니다.

### 튜플

C#에서는 튜플 분해를 기본적으로 지원하므로 한 작업에서 튜플의 모든 항목을 패키지 해제할 수 있습니다. 튜플을 분해하는 일반 구문은 정의하는 구문과 유사합니다. 즉, 대입문 왼쪽에서 각 요소가 할당되는 변수를 괄호로 묶습니다. 예를 들어, 다음 문은 4-튜플의 요소를 4개의 개별 변수에 할당합니다.

```C#
var (name, address, city, zip) = contact.GetAddressInfo();
```

다음과 같은 세 가지 방법으로 튜플을 분해합니다.

 - 괄호 안에 각 필드의 형식을 명시적으로 선언할 수 있습니다. 다음 예에서는 이 방법을 사용하여 QueryCityData 메서드에서 반환된 3-튜플을 분해합니다.
```C#
  public static void Main()
{
    (string city, int population, double area) = QueryCityData("New York City");

    // Do something with the data.
}
```
 - C#에서 각 변수의 형식을 유추하도록 var 키워드를 사용할 수 있습니다. var 키워드는 괄호 밖에 놓습니다. 다음 예에서는 QueryCityData 메서드에서 반환된 3-튜플을 분해할 때 형식 유추를 사용합니다.
```C#
public static void Main()
{
    var (city, population, area) = QueryCityData("New York City");

    // Do something with the data.
}
```
 - 괄호 안에 일부 또는 모든 변수 선언에 var 키워드를 개별적으로 사용할 수도 있습니다.
```C#
public static void Main()
{
    (string city, var population, var area) = QueryCityData("New York City");

    // Do something with the data.
}
```

 - 마지막으로, 튜플을 이미 선언된 변수로 분해할 수 있습니다.
```C#
public static void Main()
{
    string city = "Raleigh";
    int population = 458880;
    double area = 144.8;

    (city, population, area) = QueryCityData("New York City");

    // Do something with the data.
}
```
 - C# 10부터 분해 시 변수 선언과 할당을 혼합할 수 있습니다.
```C#
public static void Main()
{
    string city = "Raleigh";
    int population = 458880;

    (city, population, double area) = QueryCityData("New York City");

    // Do something with the data.
}
```
튜플의 모든 필드가 동일한 형식을 가지더라도 괄호 외부에 특정 형식을 지정할 수 없습니다. 그렇게 하면 컴파일러 오류 CS8136, "'var (...)' 형식 분해는 'var'에 대한 특정 형식을 허용하지 않습니다."가 생성됩니다.

튜플의 각 요소를 변수에 할당해야 합니다. 요소를 생략하면 컴파일러에서 오류 CS8132, "'x' 요소의 튜플을 'y' 변수로 분해할 수 없습니다."를 생성합니다.

### 무시 항목이 있는 튜플 요소

튜플을 분해할 때 일부 요소 값에만 관심이 있는 경우가 종종 있습니다. 값을 무시하도록 선택한 쓰기 전용 변수인 무시 항목에 대한 C#의 지원을 활용할 수 있습니다. 무시 항목은 할당에서 밑줄 문자("_")로 선택됩니다. 원하는 수의 값을 모두 하나의 무시 항목 _로 표시하여 무시할 수 있습니다.

다음 예제에서는 무시 항목과 함께 튜플을 사용하는 방법을 보여 줍니다. QueryCityDataForYears 메서드는 도시 이름, 지역, 연도, 해당 연도의 도시 모집단, 두 번째 해, 두 번째 해의 도시 모집단이 포함된 6개의 튜플을 반환합니다. 이 예제는 이러한 두 연도 사이의 인구 변화를 보여 줍니다. 튜플에서 사용 가능한 데이터 중 도시 면적에는 관심이 없고 디자인 타임에 도시 이름과 두 날짜를 알고 있습니다. 따라서 튜플에 저장된 두 가지 인구 값에만 관심이 있고 나머지 값은 무시 항목으로 처리할 수 있습니다.

```C#
using System;

public class ExampleDiscard
{
    public static void Main()
    {
        var (_, _, _, pop1, _, pop2) = QueryCityDataForYears("New York City", 1960, 2010);

        Console.WriteLine($"Population change, 1960 to 2010: {pop2 - pop1:N0}");
    }

    private static (string, double, int, int, int, int) QueryCityDataForYears(string name, int year1, int year2)
    {
        int population1 = 0, population2 = 0;
        double area = 0;

        if (name == "New York City")
        {
            area = 468.48;
            if (year1 == 1960)
            {
                population1 = 7781984;
            }
            if (year2 == 2010)
            {
                population2 = 8175133;
            }
            return (name, area, year1, population1, year2, population2);
        }

        return ("", 0, 0, 0, 0, 0);
    }
}
// The example displays the following output:
//      Population change, 1960 to 2010: 393,149
```
### 사용자 정의 형식

C#은 record 및 DictionaryEntry 형식 이외의 튜플이 아닌 형식을 분해하기 위한 기본 지원을 제공하지 않습니다. 그러나 클래스, 구조체 또는 인터페이스의 만든 이는 하나 이상의 Deconstruct 메서드를 구현하여 형식의 인스턴스를 분해하도록 허용할 수 있습니다. 이 메서드는 void를 반환하며 분해할 각 값은 메서드 시그니처에서 out 매개 변수로 표시됩니다. 예를 들어 다음 Person 클래스의 Deconstruct 메서드는 이름, 중간 이름 및 성을 반환합니다.

```C#
public void Deconstruct(out string fname, out string mname, out string lname)
```
그리고 다음 코드와 같은 할당을 사용하여 p라는 Person 클래스의 인스턴스를 분해할 수 있습니다.
```C#
var (fName, mName, lName) = p;
```

다음 예제에서는 Deconstruct 메서드를 오버로드하여 Person 개체의 속성을 다양한 조합으로 반환합니다. 개별 오버로드는 다음을 반환합니다.

 - 이름 및 성
 - 성, 중간 이름, 성
 - 이름, 성, 도시 이름 및 주 이름

```C#
using System;

public class Person
{
    public string FirstName { get; set; }
    public string MiddleName { get; set; }
    public string LastName { get; set; }
    public string City { get; set; }
    public string State { get; set; }

    public Person(string fname, string mname, string lname,
                  string cityName, string stateName)
    {
        FirstName = fname;
        MiddleName = mname;
        LastName = lname;
        City = cityName;
        State = stateName;
    }

    // Return the first and last name.
    public void Deconstruct(out string fname, out string lname)
    {
        fname = FirstName;
        lname = LastName;
    }

    public void Deconstruct(out string fname, out string mname, out string lname)
    {
        fname = FirstName;
        mname = MiddleName;
        lname = LastName;
    }

    public void Deconstruct(out string fname, out string lname,
                            out string city, out string state)
    {
        fname = FirstName;
        lname = LastName;
        city = City;
        state = State;
    }
}

public class ExampleClassDeconstruction
{
    public static void Main()
    {
        var p = new Person("John", "Quincy", "Adams", "Boston", "MA");

        // Deconstruct the person object.
        var (fName, lName, city, state) = p;
        Console.WriteLine($"Hello {fName} {lName} of {city}, {state}!");
    }
}
// The example displays the following output:
//    Hello John Adams of Boston, MA!
```

매개 변수 수가 같은 여러 Deconstruct 메서드는 모호합니다. 매개 변수 수, 즉 "인자"가 다른 Deconstruct 메서드를 정의하도록 주의해야 합니다. 오버로드 확인 중에 동일한 수의 매개 변수를 가진 Deconstruct 메서드를 구분할 수 없습니다.

### 무시 항목이 포함된 사용자 정의 형식

튜플에서와 마찬가지로 무시 항목을 사용하여 Deconstruct 메서드에서 반환된 항목 중 선택한 항목을 무시할 수 있습니다. 각 무시 항목은 “_”라는 변수로 정의하며 단일 분해 작업에 여러 무시 항목을 포함할 수 있습니다.

다음 예제에서는 Person 개체를 4개의 문자열(이름, 성, 도시 및 주)로 분해하지만 성과 주는 무시합니다.

```C#
// Deconstruct the person object.
var (fName, _, city, _) = p;
Console.WriteLine($"Hello {fName} of {city}!");
// The example displays the following output:
//      Hello John of Boston!
```

### 사용자 정의 형식의 확장 메서드

클래스, 구조체 또는 인터페이스의 만든 이가 아니더라도 하나 이상의 Deconstruct확장 메서드 구현을 통해 해당 형식의 개체를 분해하여 관심 있는 값을 반환할 수 있습니다.

다음 예제에서는 System.Reflection.PropertyInfo 클래스에 대한 두 개의 Deconstruct 확장 메서드를 정의합니다. 첫 번째 메서드는 속성의 형식, 정적 속성인지 인스턴스 속성인지 여부, 읽기 전용인지 여부, 인덱싱되었는지 여부 등 속성의 특성을 나타내는 값 집합을 반환합니다. 두 번째 메서드는 속성의 접근성을 나타냅니다. get 및 set 접근자의 접근성이 다를 수 있으므로 부울 값은 속성에 별도의 get 및 set 접근자가 있는지 여부와 있는 경우 접근성이 동일한지 여부를 나타냅니다. 접근자가 하나만 있거나 get 및 set 접근자 모두 동일한 접근성을 갖는 경우 access 변수는 속성의 접근성을 전체적으로 나타냅니다. 그러지 않으면 get 및 set 접근자의 접근성이 getAccess 및 setAccess 변수로 표시됩니다.

```C#
using System;
using System.Collections.Generic;
using System.Reflection;

public static class ReflectionExtensions
{
    public static void Deconstruct(this PropertyInfo p, out bool isStatic,
                                   out bool isReadOnly, out bool isIndexed,
                                   out Type propertyType)
    {
        var getter = p.GetMethod;

        // Is the property read-only?
        isReadOnly = ! p.CanWrite;

        // Is the property instance or static?
        isStatic = getter.IsStatic;

        // Is the property indexed?
        isIndexed = p.GetIndexParameters().Length > 0;

        // Get the property type.
        propertyType = p.PropertyType;
    }

    public static void Deconstruct(this PropertyInfo p, out bool hasGetAndSet,
                                   out bool sameAccess, out string access,
                                   out string getAccess, out string setAccess)
    {
        hasGetAndSet = sameAccess = false;
        string getAccessTemp = null;
        string setAccessTemp = null;

        MethodInfo getter = null;
        if (p.CanRead)
            getter = p.GetMethod;

        MethodInfo setter = null;
        if (p.CanWrite)
            setter = p.SetMethod;

        if (setter != null && getter != null)
            hasGetAndSet = true;

        if (getter != null)
        {
            if (getter.IsPublic)
                getAccessTemp = "public";
            else if (getter.IsPrivate)
                getAccessTemp = "private";
            else if (getter.IsAssembly)
                getAccessTemp = "internal";
            else if (getter.IsFamily)
                getAccessTemp = "protected";
            else if (getter.IsFamilyOrAssembly)
                getAccessTemp = "protected internal";
        }

        if (setter != null)
        {
            if (setter.IsPublic)
                setAccessTemp = "public";
            else if (setter.IsPrivate)
                setAccessTemp = "private";
            else if (setter.IsAssembly)
                setAccessTemp = "internal";
            else if (setter.IsFamily)
                setAccessTemp = "protected";
            else if (setter.IsFamilyOrAssembly)
                setAccessTemp = "protected internal";
        }

        // Are the accessibility of the getter and setter the same?
        if (setAccessTemp == getAccessTemp)
        {
            sameAccess = true;
            access = getAccessTemp;
            getAccess = setAccess = String.Empty;
        }
        else
        {
            access = null;
            getAccess = getAccessTemp;
            setAccess = setAccessTemp;
        }
    }
}

public class ExampleExtension
{
    public static void Main()
    {
        Type dateType = typeof(DateTime);
        PropertyInfo prop = dateType.GetProperty("Now");
        var (isStatic, isRO, isIndexed, propType) = prop;
        Console.WriteLine($"\nThe {dateType.FullName}.{prop.Name} property:");
        Console.WriteLine($"   PropertyType: {propType.Name}");
        Console.WriteLine($"   Static:       {isStatic}");
        Console.WriteLine($"   Read-only:    {isRO}");
        Console.WriteLine($"   Indexed:      {isIndexed}");

        Type listType = typeof(List<>);
        prop = listType.GetProperty("Item",
                                    BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.Instance | BindingFlags.Static);
        var (hasGetAndSet, sameAccess, accessibility, getAccessibility, setAccessibility) = prop;
        Console.Write($"\nAccessibility of the {listType.FullName}.{prop.Name} property: ");

        if (!hasGetAndSet | sameAccess)
        {
            Console.WriteLine(accessibility);
        }
        else
        {
            Console.WriteLine($"\n   The get accessor: {getAccessibility}");
            Console.WriteLine($"   The set accessor: {setAccessibility}");
        }
    }
}
// The example displays the following output:
//       The System.DateTime.Now property:
//          PropertyType: DateTime
//          Static:       True
//          Read-only:    True
//          Indexed:      False
//
//       Accessibility of the System.Collections.Generic.List`1.Item property: public
```

### 시스템 형식의 확장 메서드

일부 시스템 형식은 편의를 위해 Deconstruct 메서드를 제공합니다. 예를 들어, System.Collections.Generic.KeyValuePair<TKey,TValue> 형식은 이 기능을 제공합니다. System.Collections.Generic.Dictionary<TKey,TValue>를 반복할 때 각 요소는 KeyValuePair<TKey, TValue>이며 분해될 수 있습니다. 다음 예제를 참조하세요.

```C#
Dictionary<string, int> snapshotCommitMap = new(StringComparer.OrdinalIgnoreCase)
{
    ["https://github.com/dotnet/docs"] = 16_465,
    ["https://github.com/dotnet/runtime"] = 114_223,
    ["https://github.com/dotnet/installer"] = 22_436,
    ["https://github.com/dotnet/roslyn"] = 79_484,
    ["https://github.com/dotnet/aspnetcore"] = 48_386
};

foreach (var (repo, commitCount) in snapshotCommitMap)
{
    Console.WriteLine(
        $"The {repo} repository had {commitCount:N0} commits as of November 10th, 2021.");
}
```

Deconstruct 메서드가 없는 시스템 형식에 추가할 수 있습니다. 다음 확장 메서드를 고려합니다.

```C#
public static class NullableExtensions
{
    public static void Deconstruct<T>(
        this T? nullable,
        out bool hasValue,
        out T value) where T : struct
    {
        hasValue = nullable.HasValue;
        value = nullable.GetValueOrDefault();
    }
}
```

이 확장 메서드를 사용하면 모든 Nullable<T> 형식을 (bool hasValue, T value)의 튜플로 분해할 수 있습니다. 다음 예에서는 이 확장 메서드를 사용하는 코드를 보여 줍니다.

```C#
DateTime? questionableDateTime = default;
var (hasValue, value) = questionableDateTime;
Console.WriteLine(
    $"{{ HasValue = {hasValue}, Value = {value} }}");

questionableDateTime = DateTime.Now;
(hasValue, value) = questionableDateTime;
Console.WriteLine(
    $"{{ HasValue = {hasValue}, Value = {value} }}");

// Example outputs:
// { HasValue = False, Value = 1/1/0001 12:00:00 AM }
// { HasValue = True, Value = 11/10/2021 6:11:45 PM }
```
### record 형식

둘 이상의 위치 매개 변수를 사용하여 record 형식을 선언하는 경우 컴파일러는 record 선언의 각 위치 매개 변수에 대해 out 매개 변수를 사용하여 Deconstruct 메서드를 만듭니다. 자세한 내용은 속성 정의의 위치 구문 및 파생 레코드의 분해자 동작을 참조하세요.

---
## 예외 및 예외 처리

---
C# 언어의 예외 처리 기능은 프로그램이 실행 중일 때 발생하는 예기치 않은 문제나 예외 상황을 처리하는 데 도움이 됩니다. 예외 처리는 try, catch 및 finally 키워드를 사용하여 실패했을 수 있는 작업을 시도하고, 실패를 처리하는 것이 적절하다고 판단될 때 처리하고, 리소스를 정리합니다. 예외는 CLR(공용 언어 런타임), .NET, 타사 라이브러리 또는 애플리케이션 코드에서 생성될 수 있습니다. 예외는 throw 키워드를 사용하여 생성됩니다.

대부분의 경우 코드에서 직접 호출한 메서드가 아니라 호출 스택에서 추가로 작동 중단된 다른 메서드에 의해 예외가 throw될 수 있습니다. 예외가 throw되는 경우 CLR은 스택을 해제하고 특정 예외 형식에 대해 catch 블록이 있는 메서드를 찾으며 해당하는 첫 번째 catch 블록을 실행합니다. 호출 스택에서 적절한 catch 블록을 찾지 못하면 프로세스를 종료하고 사용자에게 메시지를 표시합니다.

이 예제에서 메서드는 0으로 나누기를 테스트하고 오류를 catch합니다. 예외 처리를 사용하지 않을 경우 이 프로그램은 DivideByZeroException이(가) 처리되지 않았습니다. 오류를 나타내며 종료됩니다.

```C#
public class ExceptionTest
{
    static double SafeDivision(double x, double y)
    {
        if (y == 0)
            throw new DivideByZeroException();
        return x / y;
    }

    public static void Main()
    {
        // Input for test purposes. Change the values to see
        // exception handling behavior.
        double a = 98, b = 0;
        double result;

        try
        {
            result = SafeDivision(a, b);
            Console.WriteLine("{0} divided by {1} = {2}", a, b, result);
        }
        catch (DivideByZeroException)
        {
            Console.WriteLine("Attempted divide by zero.");
        }
    }
}
```

### 예외 개요

예외는 다음과 같은 속성을 갖습니다.

 - 모든 예외는 궁극적으로 System.Exception에서 파생되는 형식입니다.
 - 예외를 throw할 수 있는 문 주위에 try 블록을 사용합니다.
 - try 블록에서 예외가 발생하면 제어 흐름이 호출 스택에 있는 첫 번째 관련 예외 처리기로 이동됩니다. C#에서 catch 키워드는 예외 처리기를 정의하는 데 사용됩니다.
 - 지정된 예외에 대한 예외 처리기가 없으면 프로그램은 오류 메시지를 나타내며 실행을 중지합니다.
 - 예외를 처리하고 애플리케이션을 알려진 상태로 둘 수 없으면 예외를 catch하지 마세요. System.Exception을 catch하는 경우 catch 블록 끝에서 throw 키워드를 사용하여 다시 throw하세요.
 - catch 블록이 예외 변수를 정의하는 경우 이 변수를 사용하여 발생한 예외 형식에 대한 추가 정보를 얻을 수 있습니다.
 - throw 키워드를 사용하여 프로그램에서 명시적으로 예외를 생성할 수 있습니다.
 - 예외 개체는 호출 스택의 상태 및 오류에 대한 텍스트 설명 같은 오류에 대한 자세한 정보를 포함합니다.
 - finally 블록의 코드는 예외가 throw되는지와 상관없이 실행됩니다. finally 블록을 사용하여 try 블록에서 열려 있는 스트림이나 파일을 닫는 것처럼 리소스를 해제합니다.
 - .NET의 관리되는 예외는 Win32 구조적 예외 처리 메커니즘을 토대로 구현됩니다. 자세한 내용은 구조적 예외 처리(C/C++) 및 Win32 구조적 예외 처리에 대한 집중 과정을 참조하세요.

---
## 예외 사용


C#에서는 런타임 시 프로그램의 오류가 예외라는 메커니즘을 사용하여 프로그램 전체에 전파됩니다. 오류가 발생하는 코드에서 예외를 throw하고, 오류를 수정할 수 있는 코드에서 예외를 catch합니다. .NET 런타임이나 프로그램의 코드에서 예외를 throw할 수 있습니다. 예외가 throw되면 예외에 대한 catch 문이 발견될 때까지 호출 스택이 전파됩니다. Catch되지 않은 예외는 대화 상자를 표시하는 시스템에서 제공하는 제네릭 예외 처리기에 의해 처리됩니다.

예외는 Exception에서 파생된 클래스로 표현됩니다. 이 클래스는 예외의 형식을 식별하며 예외에 대한 세부 정보가 들어 있는 속성을 포함합니다. 예외를 throw하는 것에는 예외에서 파생된 클래스의 인스턴스를 만드는 것, 선택적으로 예외의 속성을 구성하는 것, 그리고 throw 키워드를 사용하여 개체를 throw하는 것이 포함됩니다. 예시:
```C#
class CustomException : Exception
{
    public CustomException(string message)
    {
    }
}
private static void TestThrow()
{
    throw new CustomException("Custom exception in TestThrow()");
}
```
예외가 throw되면 런타임은 현재 문을 확인하여 try 블록 내에 있는지 알아봅니다. 있는 경우, try 블록과 연결된 catch 블록을 확인하여 예외를 catch할 수 있는지 알아봅니다. Catch 블록은 일반적으로 예외 형식을 지정합니다. catch 블록의 형식이 예외와 동일한 형식이거나 예외의 기본 클래스인 경우 catch 블록이 메서드를 처리할 수 있습니다. 예시:
```C#
try
{
    TestThrow();
}
catch (CustomException ex)
{
    System.Console.WriteLine(ex.ToString());
}
```
예외를 throw하는 문이 try 블록 내에 없거나 이를 감싸는 try 블록에 일치하는 catch 블록이 없는 경우 런타임은 호출 메서드에 try 문과 catch 블록이 있는지 확인합니다. 런타임은 호출 스택까지 계속 확인하여 호환되는 catch 블록을 검색합니다. catch 블록을 찾아서 실행한 후에는 해당 catch 블록 다음의 문으로 제어가 전달됩니다.

try 문은 catch 블록을 둘 이상 포함할 수 있습니다. 예외를 처리할 수 있는 첫 번째 catch 문이 실행됩니다. 그 뒤의 catch 문은 호환되더라도 무시됩니다. 가장 구체적인(또는 가장 많이 파생된) 예외부터 가장 덜 구체적인 예외 순으로 catch 블록 순서를 지정합니다. 예시:
```C#
using System;
using System.IO;

namespace Exceptions
{
    public class CatchOrder
    {
        public static void Main()
        {
            try
            {
                using (var sw = new StreamWriter("./test.txt"))
                {
                    sw.WriteLine("Hello");
                }
            }
            // Put the more specific exceptions first.
            catch (DirectoryNotFoundException ex)
            {
                Console.WriteLine(ex);
            }
            catch (FileNotFoundException ex)
            {
                Console.WriteLine(ex);
            }
            // Put the least specific exception last.
            catch (IOException ex)
            {
                Console.WriteLine(ex);
            }
            Console.WriteLine("Done");
        }
    }
}
```
catch 블록이 실행되기 전에 런타임은 finally 블록을 확인합니다. 프로그래머는 Finally 블록을 사용해 중단된 try 블록으로부터 남겨질 수 있는 모호한 상태를 정리하거나, 런타임 시 가비지 수집기를 기다리지 않은 채 외부 리소스(예: 그래픽 핸들, 데이터베이스 연결 또는 파일 스트림)를 해제하여 개체를 마무리할 수 있습니다. 예시:

```C#
static void TestFinally()
{
    FileStream? file = null;
    //Change the path to something that works on your machine.
    FileInfo fileInfo = new System.IO.FileInfo("./file.txt");

    try
    {
        file = fileInfo.OpenWrite();
        file.WriteByte(0xF);
    }
    finally
    {
        // Closing the file allows you to reopen it immediately - otherwise IOException is thrown.
        file?.Close();
    }

    try
    {
        file = fileInfo.OpenWrite();
        Console.WriteLine("OpenWrite() succeeded");
    }
    catch (IOException)
    {
        Console.WriteLine("OpenWrite() failed");
    }
}
```
WriteByte()에서 예외를 throw한 경우, file.Close()가 호출되지 않으면 파일을 다시 열려고 시도하는 두 번째 try 블록이 실패하고 파일이 잠긴 상태로 유지됩니다. finally 블록은 예외가 throw되도 실행되므로, 이전 예제의 finally 블록을 통해 파일을 정확히 닫고 오류를 방지할 수 있습니다.

예외가 throw된 후 호출 스택에서 호환되는 catch 블록을 찾지 못하면 다음 세 가지 중 하나가 발생합니다.
 - 예외가 종료자 내부에 있으면 종료자가 중단되고 기본 종료자(있는 경우)가 호출됩니다.
 - 호출 스택에 정적 생성자 또는 정적 필드 이니셜라이저가 포함된 경우 새 예외의 InnerException 속성에 할당된 원래 예외와 함께 TypeInitializationException이 throw됩니다.
 - 스레드의 시작에 도달하면 스레드가 종료됩니다.
---
## 예외 처리(C# 프로그래밍 가이드)

try 블록은 C# 프로그래머가 예외의 영향을 받을 수 있는 코드를 분할하는 데 사용됩니다. 연결된 catch 블록은 결과 예외를 처리하는 데 사용됩니다. finally 블록에는 try 블록에서 할당되는 리소스 해제와 같이 try 블록에서 예외가 throw되는지 여부와 관계없이 실행되는 코드가 포함됩니다. try 블록에는 하나 이상의 연결된 catch 블록, finally 블록 또는 둘 다가 필요합니다.

다음 예제에서는 try-catch 문, try-finally 문 및 try-catch-finally 문을 보여 줍니다.
```C#
try
{
    // Code to try goes here.
}
catch (SomeSpecificException ex)
{
    // Code to handle the exception goes here.
    // Only catch exceptions that you know how to handle.
    // Never catch base class System.Exception without
    // rethrowing it at the end of the catch block.
}
```
```C#
try
{
    // Code to try goes here.
}
finally
{
    // Code to execute after the try block goes here.
}
```
```C#
try
{
    // Code to try goes here.
}
catch (SomeSpecificException ex)
{
    // Code to handle the exception goes here.
}
finally
{
    // Code to execute after the try (and possibly catch) blocks
    // goes here.
}
```
try 블록에 catch 또는 finally 블록이 없으면 컴파일러 오류가 발생합니다.

### catch 블록

catch 블록에서는 catch할 예외의 형식을 지정할 수 있습니다. 형식 사양을 예외 필터라고 합니다. 예외 형식은 Exception에서 파생되어야 합니다. 일반적으로 Exception 블록에서 throw될 수 있는 모든 예외를 처리하는 방법을 알고 있거나 try 블록의 끝에 throw 문을 포함한 경우가 아니라면 catch를 예외 필터로 지정하지 마세요.

다른 예외 클래스를 사용하는 여러 catch 블록을 함께 연결할 수 있습니다. catch 블록은 코드의 위에서 아래로 계산되지만 throw되는 각 예외에 대해 하나의 catch 블록만 실행됩니다. throw된 예외의 정확한 형식이나 기본 클래스를 지정하는 첫 번째 catch 블록이 실행됩니다. catch 블록에서 일치하는 예외 클래스를 지정하지 않으면 catch 블록이 문에 있는 경우 어느 형식도 없는 블록이 선택됩니다. 먼저 가장 구체적인(즉, 최다 파생) 예외 클래스를 사용하여 catch 블록을 배치해야 합니다.

다음 조건을 충족하는 경우 예외를 catch합니다.

 - 예외가 throw되는 이유를 충분히 이해하고 있으면 FileNotFoundException 개체를 catch할 때 새 파일 이름을 입력하라는 메시지를 사용자에게 표시하는 경우처럼 구체적인 복구를 구현할 수 있습니다.
 - 보다 구체적인 새 예외를 생성하고 throw할 수 있습니다
```C#
int GetInt(int[] array, int index)
{
    try
    {
        return array[index];
    }
    catch (IndexOutOfRangeException e)
    {
        throw new ArgumentOutOfRangeException(
            "Parameter index is out of range.", e);
    }
}
```
 - 추가 처리를 위해 예외를 전달하기 전에 예외를 부분적으로 처리하려고 합니다. 다음 예제에서 catch 블록은 예외를 다시 throw하기 전에 오류 로그에 항목을 추가하는 데 사용됩니다.
```C#
try
{
    // Try to access a resource.
}
catch (UnauthorizedAccessException e)
{
    // Call a custom error logging procedure.
    LogError(e);
    // Re-throw the error.
    throw;
}
```

‘예외 필터’를 지정하여 catch 절에 부울 식을 추가할 수도 있습니다. 예외 필터는 해당 조건이 true인 경우에만 특정 catch 절이 일치함을 나타냅니다. 다음 예에서는 두 catch 절 모두 동일한 예외 클래스를 사용하지만 다른 오류 메시지를 만들기 위해 추가 조건을 확인합니다.

```C#
int GetInt(int[] array, int index)
{
    try
    {
        return array[index];
    }
    catch (IndexOutOfRangeException e) when (index < 0) 
    {
        throw new ArgumentOutOfRangeException(
            "Parameter index cannot be negative.", e);
    }
    catch (IndexOutOfRangeException e)
    {
        throw new ArgumentOutOfRangeException(
            "Parameter index cannot be greater than the array size.", e);
    }
}
```
항상 false를 반환하는 예외 필터를 사용하여 모든 예외를 검사하지만 처리하지는 않을 수 있습니다. 일반적인 용도는 예외를 기록하는 것입니다.

```C#
public class ExceptionFilter
{
    public static void Main()
    {
        try
        {
            string? s = null;
            Console.WriteLine(s.Length);
        }
        catch (Exception e) when (LogException(e))
        {
        }
        Console.WriteLine("Exception must have been handled");
    }

    private static bool LogException(Exception e)
    {
        Console.WriteLine($"\tIn the log routine. Caught {e.GetType()}");
        Console.WriteLine($"\tMessage: {e.Message}");
        return false;
    }
}
```
LogException 메서드는 항상 false를 반환하므로 이 예외 필터를 사용하는 catch 절 중 어느 것도 일치하지 않습니다. catch 절은 System.Exception을 사용하는 범용일 수 있으며 이후 절이 더 구체적인 예외 클래스를 처리할 수 있습니다.

### Finally 블록

finally 블록에서는 try 블록에서 수행된 작업을 정리할 수 있습니다. finally 블록이 있는 경우 try 블록 및 일치하는 모든 catch 블록 다음에 마지막으로 실행됩니다. finally 블록은 예외가 throw되었는지 또는 예외 형식과 일치하는 catch 블록이 있는지와 관계없이 항상 실행됩니다.

finally 블록은 런타임의 가비지 수집기가 개체를 종료할 때까지 기다리지 않고 파일 스트림, 데이터베이스 연결, 그래픽 핸들 등의 리소스를 해제하는 데 사용됩니다.

다음 예제에서는 finally 블록을 사용하여 try 블록에서 연 파일을 닫습니다. 파일을 닫기 전에 파일 핸들의 상태를 확인해야 합니다. try 블록에서 파일을 열 수 없는 경우 파일 핸들은 값이 null이며 finally 블록은 파일을 닫지 않습니다. 대신 try 블록에서 파일을 연 경우 finally 블록에서 열려 있는 파일을 닫습니다.

```C#
FileStream? file = null;
FileInfo fileinfo = new System.IO.FileInfo("./file.txt");
try
{
    file = fileinfo.OpenWrite();
    file.WriteByte(0xF);
}
finally
{
    // Check for null because OpenWrite might have failed.
    file?.Close();
}
```
---
## 예외 만들기 및 throw

예외는 프로그램을 실행하는 동안 오류가 발생했음을 나타내는 데 사용됩니다. 오류를 설명하는 예외 개체가 만들어지고 throw 문 또는 식을 통해 throw됩니다. 그런 다음 런타임에 가장 호환성이 높은 예외 처리기를 검색합니다.

프로그래머는 다음 조건 중 하나 이상에 해당할 경우 예외를 throw해야 합니다.

 - 메서드가 정의된 기능을 완료할 수 없는 경우. 예를 들어 메서드에 대한 매개 변수에 잘못된 값이 포함된 경우입니다.
```C#
static void CopyObject(SampleClass original)
{
    _ = original ?? throw new ArgumentException("Parameter cannot be null", nameof(original));
}
```
 - 개체 상태에 따라 개체에 대한 부적절한 호출이 이루어진 경우. 한 가지 예는 읽기 전용 파일에 쓰려고 시도하는 경우입니다. 개체 상태가 작업을 허용하지 않을 경우 이 클래스의 파생에 따라 InvalidOperationException의 인스턴스 또는 개체를 throw합니다. 다음 코드는 InvalidOperationException 개체를 throw 하는 메서드의 예제입니다.
```C#
public class ProgramLog
{
    FileStream logFile = null!;
    public void OpenLog(FileInfo fileName, FileMode mode) { }

    public void WriteLog()
    {
        if (!logFile.CanWrite)
        {
            throw new InvalidOperationException("Logfile cannot be read-only");
        }
        // Else write data to the log and return.
    }
}
```
 - 메서드에 대한 인수가 예외를 일으키는 경우. 이 경우 원래 예외가 catch되고 ArgumentException 인스턴스가 만들어져야 합니다. 원래 예외를 ArgumentException의 생성자에 InnerException 매개 변수로 전달해야 합니다.
```C#
static int GetValueFromArray(int[] array, int index)
{
    try
    {
        return array[index];
    }
    catch (IndexOutOfRangeException e)
    {
        throw new ArgumentOutOfRangeException(
            "Parameter index is out of range.", e);
    }
}
```
```
참고

앞의 예제는 InnerException 속성을 사용하는 방법을 보여줍니다. 이 예제는 의도적으로 간소화되었습니다. 실제로는 인덱스를 사용하기 전에 인덱스가 범위 내에 있는지 확인해야 합니다. 매개 변수의 멤버가 멤버를 호출하기 전에 예상할 수 없는 예외를 throw할 때 예외를 래핑하는 이 기법을 사용할 수 있습니다.
```

예외에 이름이 StackTrace인 속성이 포함되어 있습니다. 이 문자열에는 현재 콜 스택에 대한 메서드의 이름과 각 메서드에 대해 예외가 throw된 파일 이름 및 줄 번호가 포함됩니다. StackTrace 개체는 throw 문의 지점에서 CLR(공용 언어 런타임)에 의해 자동으로 만들어지므로 해당 예외는 스택 추적이 시작되는 지점에서 throw되어야 합니다.

모든 예외에 이름이 Message인 속성이 포함되어 있습니다. 예외의 이유를 설명하려면 이 문자열을 설정해야 합니다. 보안이 중요한 정보는 메시지 텍스트에 넣으면 안 됩니다. Message 외에 ArgumentException에는 예외를 throw한 인수의 이름으로 설정해야 하는 ParamName 속성이 포함되어 있습니다. 속성 setter에서는 ParamName을 value로 설정해야 합니다.

public 및 protected 메서드는 의도한 함수를 완료할 수 없을 때마다 예외를 throw합니다. throw된 예외 클래스는 오류 조건에 맞을 수 있는 가장 구체적인 예외입니다. 이러한 예외는 클래스 기능의 일부로 문서화해야 하고 파생 클래스 또는 원래 클래스의 업데이트는 이전 버전과의 호환성을 위해 같은 동작을 유지해야 합니다.

### 예외를 throw할 때 피해야 하는 작업

다음 목록은 예외를 throw할 때 피해야 할 사례를 나타냅니다.

 - 프로그램의 흐름을 일반 실행의 일부로 변경하는 데는 예외를 사용하지 마세요. 오류 조건을 보고하고 처리하는 데 예외를 사용합니다.
 - 예외는 throw하는 대신 반환 값 또는 매개 변수로 반환하면 안 됩니다.
 - 고유한 소스 코드에서 의도적으로 System.Exception, System.SystemException, System.NullReferenceException 또는 System.IndexOutOfRangeException을 throw하지 마세요.
 - 릴리스 모드가 아닌 디버그 모드에서 throw될 수 있는 예외를 만들지 마세요. 개발 단계에서 런타임 오류를 식별하려면 대신 디버그 어설션을 사용하세요.

### 작업 반환 메서드의 예외

async 한정자를 사용하여 선언된 메서드에는 예외와 관련하여 몇 가지 특별한 고려 사항이 있습니다. async 메서드에서 throw된 예외는 반환된 작업에 저장되며 예컨데 작업이 대기될 때까지 나타나지 않습니다. 저장된 예외에 대한 자세한 내용은 비동기 예외를 참조하세요.

메서드의 비동기 부분을 입력하기 전에 인수의 유효성을 검사하고 해당하는 예외(예: ArgumentException 및 ArgumentNullException)를 throw하는 것이 좋습니다. 즉, 이러한 유효성 검사 예외는 작업이 시작되기 전에 동기적으로 나타나야 합니다. 다음 코드 조각은 예외가 throw되면 ArgumentException 예외가 동기적으로 나타나는 반면 InvalidOperationException은 반환된 작업에 저장되는 예를 보여줍니다.

```C#
// Non-async, task-returning method.
// Within this method (but outside of the local function),
// any thrown exceptions emerge synchronously.
public static Task<Toast> ToastBreadAsync(int slices, int toastTime)
{
    if (slices is < 1 or > 4)
    {
        throw new ArgumentException(
            "You must specify between 1 and 4 slices of bread.",
            nameof(slices));
    }

    if (toastTime < 1)
    {
        throw new ArgumentException(
            "Toast time is too short.", nameof(toastTime));
    }

    return ToastBreadAsyncCore(slices, toastTime);

    // Local async function.
    // Within this function, any thrown exceptions are stored in the task.
    static async Task<Toast> ToastBreadAsyncCore(int slices, int time)
    {
        for (int slice = 0; slice < slices; slice++)
        {
            Console.WriteLine("Putting a slice of bread in the toaster");
        }
        // Start toasting.
        await Task.Delay(time);

        if (time > 2_000)
        {
            throw new InvalidOperationException("The toaster is on fire!");
        }

        Console.WriteLine("Toast is ready!");

        return new Toast();
    }
}
```
### 예외 클래스 정의

프로그램에서는 System 네임스페이스의 미리 정의된 예외 클래스를 throw하거나(이전에 언급한 위치 제외) Exception에서 파생시켜 자체 예외 클래스를 만들 수 있습니다. 파생 클래스는 최소 세 개의 생성자, 즉 매개 변수 없는 생성자, 메시지 속성을 설정하는 생성자, Message 및 InnerException 속성을 모두 설정하는 생성자를 정의해야 합니다. 예시:
```C#
[Serializable]
public class InvalidDepartmentException : Exception
{
    public InvalidDepartmentException() : base() { }
    public InvalidDepartmentException(string message) : base(message) { }
    public InvalidDepartmentException(string message, Exception inner) : base(message, inner) { }
}
```
새로운 속성이 제공하는 데이터가 예외 확인에 유용할 경우 해당 속성을 예외 클래스에 추가합니다. 새 속성이 파생 예외 클래스에 추가되면 추가된 정보를 반환하기 위해 ToString()을 재정의해야 합니다.

---
## 컴파일러 생성 예외

기본 작업이 실패하면 .NET 런타임에 의해 자동으로 일부 예외가 throw됩니다. 이러한 예외와 관련 오류 조건이 다음 표에 나와 있습니다.

| 예외                          | 설명                                                                                        |
|-----------------------------|-------------------------------------------------------------------------------------------|
| ArithmeticException         | DivideByZeroException, OverflowException 등의 산술 연산 중에 발생하는 예외에 대한 기본 클래스입니다.               |
| ArrayTypeMismatchException  | 제공된 요소의 실제 형식이 배열의 실제 형식과 호환되지 않아 배열이 요소를 저장할 수 없는 경우 throw됩니다.                           |
| DivideByZeroException       | 정수 값을 0으로 나누려고 시도할 경우 throw됩니다.                                                           |
| IndexOutOfRangeException    | 인덱스가 0보다 작거나 배열 경계를 벗어날 때 배열을 인덱싱하려고 시도할 경우 throw됩니다.                                     |
| InvalidCastException        | 기본 형식에서 인터페이스 또는 파생 형식으로의 명시적 변환이 런타임에 실패할 경우 throw됩니다.                                   |
| NullReferenceException      | 값이 null인 개체를 참조하려고 시도할 경우 throw됩니다.                                                       |
| OutOfMemoryException        | new 연산자를 사용한 메모리 할당 시도가 실패할 경우 throw됩니다. 이 예외는 공용 언어 런타임에 사용할 수 있는 메모리가 모두 사용되었음을 나타냅니다.  |
| OverflowException           | checked 컨텍스트의 산술 연산이 오버플로될 경우 throw됩니다.                                                   |
| StackOverflowException      | 보류 중인 메서드 호출이 너무 많아 실행 스택이 모두 사용될 경우 throw됩니다. 대개 매우 깊은 재귀나 무한 재귀를 나타냅니다.                 |
| TypeInitializationException | 정적 생성자가 예외를 throw하고 이 예외를 catch할 수 있는 호환되는 catch 절이 없는 경우 throw됩니다.                       |

---
## C# 식별자 명명 규칙 및 규칙

---
식별자는 형식(클래스, 인터페이스, 구조체, 대리자 또는 열거형), 멤버, 변수 또는 네임스페이스에 할당하는 이름입니다.

### 이름 지정 규칙

유효한 식별자는 다음 규칙을 따라야 합니다. C# 컴파일러는 다음 규칙을 따르지 않는 식별자에 대해 오류를 생성합니다.

 - 식별자는 문자나 밑줄(_)로 시작해야 합니다.
 - 식별자에는 유니코드 문자, 10진수 문자, 유니코드 연결 문자, 유니코드 조합 문자 또는 유니코드 형식 문자가 포함될 수 있습니다. 유니코드 범주에 대한 자세한 내용은 유니코드 범주 데이터베이스를 참조하세요.

식별자의 @ 접두사를 사용하여 C# 키워드와 일치하는 식별자를 선언할 수 있습니다. @은 식별자 이름의 일부가 아닙니다. 예를 들어 @if는 if라는 식별자를 선언합니다. 이러한 verbatim 식별자는 주로 다른 언어로 선언된 식별자와의 상호 운용성을 위한 것입니다.

```
중요

C# 언어 사양에서는 문자(Lu, Ll, Lt, Lm, Lo 또는 Nl), 숫자(Nd), 연결(Pc), 결합(Mn 또는 Mc) 및 서식(Cf) 범주만 허용합니다. 외부의 모든 항목은 _을 사용하여 자동으로 바뀝니다. 이는 특정 유니코드 문자에 영향을 미칠 수 있습니다.
```

### 명명 규칙

규칙 외에도 식별자 이름에 대한 규칙이 .NET API 전체에서 사용됩니다. 이러한 규칙은 이름에 대한 일관성을 제공하지만 컴파일러는 이를 강제하지 않습니다. 프로젝트에서 다양한 규칙을 자유롭게 사용할 수 있습니다.

규칙에 따라 C# 프로그램은 형식 이름, 네임스페이스 및 모든 공용 멤버에 PascalCase를 사용합니다. 또한 dotnet/docs 팀은 .NET 런타임 팀의 코딩 스타일에서 채택한 다음 규칙을 사용합니다.

 - 인터페이스 이름은 대문자 I로 시작합니다.
 - 특성 유형은 Attribute 단어로 끝납니다.
 - 열거형 형식은 플래그가 아닌 경우에는 단수 명사를 사용하고 플래그인 경우에는 복수 명사를 사용합니다.
 - 식별자에는 두 개의 연속된 밑줄(_) 문자가 포함될 수 없습니다. 이러한 이름은 컴파일러 생성 식별자용으로 예약되어 있습니다.
 - 변수, 메서드, 클래스에 의미 있고 설명이 포함된 이름을 사용합니다.
 - 간결함보다 명확성이 더 중요합니다.
 - 클래스 이름과 메서드 이름에는 PascalCase를 사용합니다.
 - 메서드 매개 변수 및 지역 변수에 camelCase를 사용합니다.
 - 필드와 지역 상수 모두 상수 이름에 PascalCase를 사용합니다.
 - 프라이빗 인스턴스 필드는 밑줄(_)로 시작하고 다시 기본 텍스트는 camelCased입니다.
 - 정적 필드는 s_로 시작합니다. 이 규칙은 기본 Visual Studio 동작도 아니고 프레임워크 디자인 지침의 일부도 아니지만 editorconfig에서 구성할 수 있습니다.
 - 널리 알려지고 인정되는 약어를 제외하고 이름에 약어나 머리글자어를 사용하지 마세요.
 - 역방향 도메인 이름 표기법에 따라 의미 있고 설명이 포함된 네임스페이스를 사용합니다.
 - 어셈블리의 기본 목적을 나타내는 어셈블리 이름을 선택합니다.
 - 간단한 루프 카운터를 제외하고 단일 문자 이름을 사용하지 마세요. 또한 C# 구문(construct)의 구문(syntax)을 설명하는 구문(syntax) 예에서는 C# 언어 사양에 사용된 규칙과 일치하는 다음과 같은 단일 문자 이름을 사용하는 경우가 많습니다. 구문 예는 규칙의 예외입니다.
     - 구조체에는 S를 사용하고 클래스에는 C를 사용합니다.
     - 메서드에는 M을 사용합니다.
     - 변수에는 v을, 매개 변수에는 p를 사용합니다.
     - ref 매개 변수에는 r을 사용합니다.

```
 팁

코드 스타일 명명 규칙을 사용하여 대문자, 접두사, 접미사 및 단어 구분 기호와 관련된 명명 규칙을 적용할 수 있습니다.
```

다음 예에서 public으로 표시된 요소와 관련된 지침은 protected 및 protected internal 요소로 작업할 때도 적용 가능하며, 이 요소는 모두 외부 호출자에게 표시됩니다.

### 파스칼식 대/소문자

class, interface, struct 또는 delegate 형식의 이름을 지정할 때 파스칼식 대/소문자("PascalCasing")를 사용합니다.

```C#
public class DataService
{
}
```
```C#
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```
```C#
public struct ValueCoordinate
{
}
```
```C#
public delegate void DelegateType(string message);
```
interface 이름을 지정할 때는 이름 앞에 I 접두사를 적용하고 파스칼식 대/소문자를 사용합니다. 이 접두사는 해당 항목이 interface임을 소비자에게 분명히 나타냅니다.
```C#
public interface IWorkerQueue
{
}
```
필드, 속성, 이벤트 등 형식의 public 멤버 이름을 지정할 때 파스칼식 대/소문자를 사용합니다. 또한 모든 메서드와 로컬 함수에 대해 파스칼식 대/소문자 구분을 사용합니다.
```C#
public class ExampleEvents
{
    // A public field, these should be used sparingly
    public bool IsValid;

    // An init-only property
    public IWorkerQueue WorkerQueue { get; init; }

    // An event
    public event Action EventProcessing;

    // Method
    public void StartEventProcessing()
    {
        // Local function
        static int CountQueueItems() => WorkerQueue.Count;
        // ...
    }
}
```
위치 레코드를 작성할 때는 레코드의 public 속성인 매개 변수에 파스칼식 대/소문자를 사용합니다.

```C#
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```

### 카멜식 대/소문자

private 또는 internal 필드 이름을 지정할 때 카멜식 대/소문자("camelCasing")를 사용하고 앞에 _을 붙입니다. 대리자 형식의 인스턴스를 포함하여 지역 변수의 이름을 지정할 때 카멜식 대/소문자를 사용합니다.

```C#
public class DataService
{
    private IWorkerQueue _workerQueue;
}
```
```
팁

문 완성을 지원하는 IDE에서 이러한 명명 규칙을 따르는 C# 코드를 편집할 때 _을 입력하면 개체 범위 멤버가 모두 표시됩니다.
```
private 또는 internal인 static 필드를 사용할 때는 s_ 접두사를 사용하고 스레드 정적인 경우 t_을 사용합니다.

```C#
public class DataService
{
    private static IWorkerQueue s_workerQueue;

    [ThreadStatic]
    private static TimeSpan t_timeSpan;
}
```
메서드 매개 변수를 작성할 때 카멜식 대/소문자를 사용합니다.

```C#
public T SomeMethod<T>(int someNumber, bool isValid)
{
}
```

### 형식 매개 변수 명명 지침

다음 지침은 제네릭 형식 매개 변수의 형식 매개 변수에 적용됩니다. 형식 매개 변수는 제네릭 형식 또는 제네릭 메서드의 인수에 대한 자리 표시자입니다. C# 프로그래밍 가이드에서 제네릭 형식 매개 변수에 대해 자세히 알아볼 수 있습니다.

 - 필수적 단일 문자 이름으로도 자체 설명이 가능하여 설명적인 이름을 굳이 사용할 필요가 없는 경우가 아니면 제네릭 형식 매개 변수 이름을 설명적인 이름으로 지정하세요.
```C#
public interface ISessionChannel<TSession> { /*...*/ }
public delegate TOutput Converter<TInput, TOutput>(TInput from);
public class List<T> { /*...*/ }
```
 - 선택적 단일 문자 형식 매개 변수를 사용하는 형식에는 형식 매개 변수 이름으로 T를 사용해 보세요.
```C#
public int IComparer<T>() { return 0; }
public delegate bool Predicate<T>(T item);
public struct Nullable<T> where T : struct { /*...*/ }
```
 - 필수적 설명적인 형식 매개 변수 이름 앞에 “T”를 붙이세요.
```C#
public interface ISessionChannel<TSession>
{
    TSession Session { get; }
}
```
 - 선택적 매개 변수 이름 안에 형식 매개 변수에 적용되는 제약 조건을 나타내 보세요. 예를 들어, ISession으로 제한된 매개 변수는 TSession이라고 불릴 수 있습니다.

코드 분석 규칙 CA1715를 사용하여 형식 매개 변수의 이름이 적절하게 지정되었는지 확인할 수 있습니다.

### 추가 명명 규칙
 - using 지시문이 포함되지 않는 예제에서는 네임스페이스 한정을 사용합니다. 프로젝트에서 네임스페이스를 기본적으로 가져오는 경우에는 해당 네임스페이스의 이름을 정규화할 필요가 없습니다. 정규화된 이름은 한 줄에 표시하기가 너무 길면 다음 예에 나와 있는 것처럼 점(.)으로 분할할 수 있습니다.
```C#
var currentPerformanceCounterCategory = new System.Diagnostics.
    PerformanceCounterCategory();
```
 - 다른 지침에 맞도록 조정하기 위해 Visual Studio 디자이너 도구를 사용하여 만든 개체 이름을 변경할 필요는 없습니다.

---
## Common C# code conventions

코드 표준은 개발 팀 내에서 코드 가독성, 일관성, 협업을 유지하는 데 필수적입니다. 산업 관행과 정립된 지침을 따르는 코드는 이해하고, 유지보수하고, 확장하기가 더 쉽습니다. 대부분의 프로젝트는 코드 규칙을 통해 일관된 스타일을 강제합니다. dotnet/docs 및 dotnet/samples 프로젝트도 예외는 아닙니다. 이 일련의 기사에서는 우리의 코딩 규칙과 이를 강제하는 도구를 배우게 됩니다. 여러분은 우리의 규칙을 그대로 사용하거나, 팀의 필요에 맞게 수정할 수 있습니다.

우리는 다음 목표를 바탕으로 규칙을 선택했습니다:

1. 정확성: 우리의 샘플은 여러분의 애플리케이션에 복사하여 붙여넣습니다. 우리는 그것을 기대하며, 여러 번의 편집 후에도 견고하고 정확한 코드를 만들어야 합니다.
2. 교육: 우리의 샘플의 목적은 .NET과 C#의 모든 것을 가르치는 것입니다. 그래서 우리는 어떤 언어 기능이나 API에도 제한을 두지 않습니다. 대신, 그 샘플들은 기능이 좋은 선택인 경우를 가르칩니다.
3. 일관성: 독자들은 우리의 콘텐츠 전반에 걸쳐 일관된 경험을 기대합니다. 모든 샘플은 동일한 스타일을 따라야 합니다.
4. 채택: 우리는 새로운 언어 기능을 사용하도록 샘플을 적극적으로 업데이트합니다. 이러한 실천은 새로운 기능에 대한 인식을 높이고, 모든 C# 개발자들에게 더 익숙하게 만듭니다.

```
중요
이 지침은 Microsoft가 샘플과 문서를 개발할 때 사용됩니다. 이들은 .NET 런타임, C# 코딩 스타일 및 C# 컴파일러(roslyn) 지침에서 채택되었습니다. 우리는 이러한 지침이 오픈 소스 개발의 여러 해 동안 테스트되었기 때문에 선택했습니다. 이 지침들은 커뮤니티 구성원들이 런타임 및 컴파일러 프로젝트에 참여하는 데 도움을 주었습니다. 이들은 일반적인 C# 규칙의 예시일 뿐이며, 권위 있는 목록이 아닙니다(그에 대한 내용은 Framework Design Guidelines을 참조하십시오).

교육 및 채택 목표 때문에 문서의 코딩 규칙은 런타임 및 컴파일러 규칙과 다릅니다. 런타임 및 컴파일러는 핫 경로에 대해 엄격한 성능 지표를 가지고 있습니다. 많은 다른 애플리케이션들은 그렇지 않습니다. 우리의 교육 목표는 어떤 구문도 금지하지 않는 것을 규정합니다. 대신, 샘플은 언제 구문을 사용해야 하는지를 보여줍니다. 우리는 대부분의 프로덕션 애플리케이션보다 샘플을 더 적극적으로 업데이트합니다. 우리의 채택 목표는 작년에 작성된 코드가 변경할 필요가 없더라도, 오늘 작성해야 할 코드를 보여주도록 규정합니다.
```

이 글에서는 우리의 지침을 설명합니다. 이 지침은 시간이 지나면서 발전해왔으며, 지침을 따르지 않는 샘플도 있습니다. 우리는 이러한 샘플을 준수하도록 수정하는 PR(풀 리퀘스트)이나, 업데이트해야 할 샘플에 대한 주의를 환기하는 이슈를 환영합니다. 우리의 지침은 오픈 소스이며 PR과 이슈를 환영합니다. 하지만, 만약 여러분의 제출물이 이 권장 사항을 변경할 것이라면 먼저 논의를 위한 이슈를 열어주세요. 여러분은 우리의 지침을 그대로 사용하거나, 필요에 맞게 수정할 수 있습니다.

### Tools and analyzers

도구는 팀이 표준을 강제하도록 도울 수 있습니다. 선호하는 규칙을 강제하기 위해 코드 분석을 활성화할 수 있습니다. 또한, Visual Studio가 스타일 지침을 자동으로 적용하도록 editorconfig를 만들 수 있습니다. 시작점으로, dotnet/docs 저장소의 파일을 복사하여 우리의 스타일을 사용할 수 있습니다.

이 도구들은 팀이 선호하는 지침을 채택하는 것을 더 쉽게 만들어줍니다. Visual Studio는 코드 형식을 맞추기 위해 범위 내의 모든 .editorconfig 파일에 있는 규칙을 적용합니다. 여러 구성을 사용하여 기업 전체 표준, 팀 표준, 심지어 세부적인 프로젝트 표준까지 강제할 수 있습니다.

코드 분석은 활성화된 규칙이 위반될 때 경고와 진단을 생성합니다. 프로젝트에 적용하고 싶은 규칙을 설정합니다. 그런 다음, 각 CI 빌드는 개발자에게 규칙을 위반했을 때 알립니다.

#### Diagnostic IDs

자체 분석기를 만들 때 적절한 진단 ID를 선택하십시오.

### Language guidelines

다음 섹션에서는 .NET 문서 팀이 코드 예제와 샘플을 준비할 때 따르는 관행을 설명합니다. 일반적으로, 다음 관행을 따르세요:

- 가능한 한 최신 언어 기능과 C# 버전을 활용하세요.
- 사용되지 않거나 구식의 언어 구문은 피하세요.
- 제대로 처리할 수 있는 예외만 잡고, 일반적인 예외는 잡지 마세요.
- 의미 있는 오류 메시지를 제공하기 위해 특정 예외 유형을 사용하세요.
- 코드 가독성을 높이기 위해 컬렉션 조작에는 LINQ 쿼리와 메서드를 사용하세요.
- I/O 바운드 작업에는 비동기 프로그래밍(async 및 await)을 사용하세요.
- 교착 상태를 주의하고 적절할 때 Task.ConfigureAwait를 사용하세요.
- 런타임 타입 대신 데이터 타입에 대한 언어 키워드를 사용하세요. 예를 들어, System.String 대신 string을, System.Int32 대신 int를 사용하세요.
- unsigned 타입 대신 int를 사용하세요. int의 사용은 C# 전반에 걸쳐 일반적이며, 다른 라이브러리와 상호 작용할 때 더 쉽습니다. unsigned 데이터 타입에 특정한 문서의 경우는 예외입니다.
- 표현식에서 타입을 유추할 수 있을 때만 var를 사용하세요. 독자들은 문서 플랫폼에서 우리의 샘플을 봅니다. 그들은 변수의 타입을 표시하는 호버나 툴팁을 사용할 수 없습니다.
- 명확성과 단순성을 염두에 두고 코드를 작성하세요.
- 지나치게 복잡하고 얽힌 코드 로직은 피하세요.

더 구체적인 지침은 다음과 같습니다.

#### String data

 - 짧은 문자열을 연결할 때는 다음 코드와 같이 문자열 보간(string interpolation)을 사용하세요.
    ```C#
    string displayName = $"{nameList[n].LastName}, {nameList[n].FirstName}";
    ```
 - 반복문에서 문자열을 추가할 때, 특히 대량의 텍스트를 다룰 경우, System.Text.StringBuilder 객체를 사용하세요.
    ```C#
    var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
    var manyPhrases = new StringBuilder();
    for (var i = 0; i < 10000; i++)
    {
        manyPhrases.Append(phrase);
    }
    //Console.WriteLine("tra" + manyPhrases);
    ```
#### Arrays
 - 배열을 선언 라인에서 초기화할 때 간결한 구문을 사용하세요. 다음 예제에서, string[] 대신 var를 사용할 수 없습니다.
    ```C#
    string[] vowels1 = { "a", "e", "i", "o", "u" };
    ```
 - 명시적 인스턴스화를 사용하는 경우, var를 사용할 수 있습니다.
    ```C#
    var vowels2 = new string[] { "a", "e", "i", "o", "u" };
    ```

#### Delegates

 - 대리자(delegate) 타입을 정의하는 대신 Func<>와 Action<>을 사용하세요. 클래스 내에서는 대리자 메서드를 정의합니다.

    ```csharp
    Action<string> actionExample1 = x => Console.WriteLine($"x is: {x}");

    Action<string, string> actionExample2 = (x, y) =>
        Console.WriteLine($"x is: {x}, y is {y}");

    Func<string, int> funcExample1 = x => Convert.ToInt32(x);

    Func<int, int, int> funcExample2 = (x, y) => x + y;
    ```

 - Func<> 또는 Action<> 대리자로 정의된 시그니처를 사용하여 메서드를 호출하세요.

    ```csharp
    actionExample1("string for x");

    actionExample2("string for x", "string for y");

    Console.WriteLine($"The value is {funcExample1("1")}");

    Console.WriteLine($"The sum is {funcExample2(1, 2)}");
    ```

 - 대리자 타입의 인스턴스를 생성할 때는 간결한 구문을 사용하세요. 클래스 내에서 대리자 타입과 일치하는 시그니처를 가진 메서드를 정의합니다.

    ```csharp
    public delegate void Del(string message);

    public static void DelMethod(string str)
    {
        Console.WriteLine("DelMethod argument: {0}", str);
    }
    ```

 - 대리자 타입의 인스턴스를 생성하고 호출합니다. 다음 선언은 간결한 구문을 보여줍니다.

    ```csharp
    Del exampleDel2 = DelMethod;
    exampleDel2("Hey");
    ```

- 다음 선언은 전체 구문을 사용합니다.

    ```csharp
    Del exampleDel1 = new Del(DelMethod);
    exampleDel1("Hey");
    ```

#### `try-catch` and `using` statements in exception handling

 - 대부분의 예외 처리를 위해 try-catch 문을 사용하세요.
    ```csharp
    static double ComputeDistance(double x1, double y1, double x2, double y2)
    {
        try
        {
            return Math.Sqrt((x1 - x2) * (x1 - x2) + (y1 - y2) * (y1 - y2));
        }
        catch (System.ArithmeticException ex)
        {
            Console.WriteLine($"Arithmetic overflow or underflow: {ex}");
            throw;
        }
    }
    ```
 - C# using 문을 사용하여 코드를 간소화하세요. finally 블록에서 Dispose 메서드만 호출하는 try-finally 문이 있는 경우, 대신 using 문을 사용하세요.
    다음 예제에서, try-finally 문은 finally 블록에서 Dispose만 호출합니다.
    ```csharp
    Font bodyStyle = new Font("Arial", 10.0f);
    try
    {
        byte charset = bodyStyle.GdiCharSet;
    }
    finally
    {
        if (bodyStyle != null)
        {
            ((IDisposable)bodyStyle).Dispose();
        }
    }
    ```
    using 문을 사용하여 동일한 작업을 수행할 수 있습니다.
    ```csharp
    using (Font arial = new Font("Arial", 10.0f))
    {
        byte charset2 = arial.GdiCharSet;
    }
    ```
    중괄호가 필요 없는 새로운 using 문법을 사용하세요:
    ```csharp
    using Font normalStyle = new Font("Arial", 10.0f);
    byte charset3 = normalStyle.GdiCharSet;
    ```

#### `&&` and `||` operators

 - 비교를 수행할 때는 & 대신 &&, | 대신 ||를 사용하세요. 다음 예제와 같이 사용합니다.
    ```csharp
    Console.Write("Enter a dividend: ");
    int dividend = Convert.ToInt32(Console.ReadLine());

    Console.Write("Enter a divisor: ");
    int divisor = Convert.ToInt32(Console.ReadLine());

    if ((divisor != 0) && (dividend / divisor) is var result)
    {
        Console.WriteLine("Quotient: {0}", result);
    }
    else
    {
        Console.WriteLine("Attempted division by 0 ends up here.");
    }
    ```

제수가 0인 경우, if 문에서 두 번째 절은 런타임 오류를 일으킵니다. 하지만 && 연산자는 첫 번째 표현식이 false일 때 단락 평가(short-circuit)합니다. 즉, 두 번째 표현식을 평가하지 않습니다. & 연산자는 둘 다 평가하여 제수가 0일 때 런타임 오류를 발생시킵니다.

#### `new` operator

 - 다음 선언과 같이 간결한 형태의 객체 인스턴스화를 사용하세요.
    ```csharp
    var firstExample = new ExampleClass();
    ```
    ```csharp
    ExampleClass instance2 = new();
    ```
    위의 선언은 다음 선언과 동일합니다.
    ```csharp
    ExampleClass secondExample = new ExampleClass();
    ```

 - 다음 예제와 같이 객체 생성 시 객체 이니셜라이저를 사용하여 코드를 간소화하세요.
    ```csharp
    var thirdExample = new ExampleClass 
    { 
        Name = "Desktop", 
        ID = 37414,
        Location = "Redmond", 
        Age = 2.3 
    };
    ```
    다음 예제는 이니셜라이저를 사용하지 않고 앞의 예제와 동일한 속성을 설정합니다.
    ```csharp
    var fourthExample = new ExampleClass();
    fourthExample.Name = "Desktop";
    fourthExample.ID = 37414;
    fourthExample.Location = "Redmond";
    fourthExample.Age = 2.3;
    ```

#### Event handling

 - 제거할 필요가 없는 이벤트 핸들러를 정의할 때는 람다 식을 사용하세요:
    ```csharp
    public Form2()
    {
        this.Click += (s, e) =>
            {
                MessageBox.Show(
                    ((MouseEventArgs)e).Location.ToString());
            };
    }
    ```
    람다 식은 다음 전통적인 정의를 간소화합니다.
    ```csharp
    public Form1()
    {
        this.Click += new EventHandler(Form1_Click);
    }

    void Form1_Click(object? sender, EventArgs e)
    {
        MessageBox.Show(((MouseEventArgs)e).Location.ToString());
    }
    ```

#### Static members

정적 멤버를 호출할 때는 클래스 이름을 사용하세요: `ClassName.StaticMember`. 이 방식은 정적 접근을 명확히 하여 코드 가독성을 높입니다. 파생 클래스의 이름으로 기본 클래스에 정의된 정적 멤버를 수식하지 마세요. 그 코드는 컴파일되지만, 코드 가독성을 저하시킬 뿐만 아니라, 동일한 이름의 정적 멤버를 파생 클래스에 추가하면 코드가 오류를 일으킬 수 있습니다.

#### LINQ queries

 - 쿼리 변수에 의미 있는 이름을 사용하세요. 다음 예제는 시애틀에 있는 고객들을 위해 `seattleCustomers`를 사용합니다.
    ```csharp
    var seattleCustomers = from customer in customers
                        where customer.City == "Seattle"
                        select customer.Name;
    ```
 - 익명 타입의 속성 이름이 Pascal 표기법을 사용하여 올바르게 대문자로 표시되도록 별칭을 사용하세요.
    ```csharp
    var localDistributors =
        from customer in customers
        join distributor in distributors on customer.City equals distributor.City
        select new { Customer = customer, Distributor = distributor };
    ```
 - 결과의 속성 이름이 모호할 때는 속성 이름을 변경하세요. 예를 들어, 쿼리가 고객 이름과 배급사 ID를 반환하는 경우, 결과에 이름을 `Name`과 `ID`로 남겨두는 대신, 고객의 이름은 `CustomerName`, 배급사의 ID는 `DistributorID`로 명확히 하세요.
    ```csharp
    var localDistributors2 =
        from customer in customers
        join distributor in distributors on customer.City equals distributor.City
        select new { CustomerName = customer.Name, DistributorID = distributor.ID };
    ```
 - 쿼리 변수와 범위 변수 선언에서 암시적 타입을 사용하세요. LINQ 쿼리에서의 암시적 타입 사용 지침은 일반적인 암시적 타입 로컬 변수에 대한 규칙을 재정의합니다. LINQ 쿼리는 종종 익명 타입을 생성하는 프로젝션을 사용합니다. 다른 쿼리 표현식은 중첩된 제네릭 타입으로 결과를 생성합니다. 암시적 타입 변수는 종종 더 읽기 쉽습니다.
    ```csharp
    var seattleCustomers = from customer in customers
                        where customer.City == "Seattle"
                        select customer.Name;
    ```
 - 쿼리 절은 `from` 절 아래에 정렬하세요. 위 예제와 같이 하세요.
 = `where` 절을 다른 쿼리 절 앞에 사용하여 나중의 쿼리 절이 필터링된 데이터 집합에서 작동하도록 하세요.
    ```csharp
    var seattleCustomers2 = from customer in customers
                            where customer.City == "Seattle"
                            orderby customer.Name
                            select customer;
    ```
 - 내부 컬렉션에 접근하기 위해 `join` 절 대신 여러 개의 `from` 절을 사용하세요. 예를 들어, 각 학생 객체의 컬렉션에는 시험 점수 컬렉션이 있을 수 있습니다. 다음 쿼리가 실행되면, 90점 이상의 점수와 해당 점수를 받은 학생의 성을 반환합니다.
    ```csharp
    var scoreQuery = from student in students
                    from score in student.Scores!
                    where score > 90
                    select new { Last = student.LastName, score };
    ```

#### Implicitly typed local variables

 -  변수의 타입이 할당의 오른쪽에서 명확할 때 지역 변수에 대해 암시적 타입을 사용하세요.
    ```csharp
    var message = "This is clearly a string.";
    var currentTemperature = 27;
    ```
 - 타입이 할당의 오른쪽에서 명확하지 않을 때는 `var`를 사용하지 마세요. 메서드 이름만 보고 타입이 명확하다고 가정하지 마세요. `new` 연산자, 명시적 캐스트, 또는 리터럴 값 할당일 때 타입이 명확하다고 간주합니다.
    ```csharp
    int numberOfIterations = Convert.ToInt32(Console.ReadLine());
    int currentMaximum = ExampleClass.ResultSoFar();
    ```
 - 변수 타입을 지정하기 위해 변수 이름을 사용하지 마세요. 이는 정확하지 않을 수 있습니다. 대신, 타입을 지정하고 변수 이름을 통해 변수의 의미를 나타내세요. 다음 예제는 타입으로 `string`을 사용하고, 콘솔에서 읽은 정보를 의미하는 이름으로 `iterations`와 같은 것을 사용해야 합니다.
    ```csharp
    var inputInt = Console.ReadLine();
    Console.WriteLine(inputInt);
    ```
 - `var`를 `dynamic` 대신 사용하는 것을 피하세요. 런타임 타입 추론이 필요할 때는 `dynamic`을 사용하세요. 자세한 내용은 [Using type dynamic (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/interop/using-type-dynamic) 문서를 참조하세요.
 - for 루프의 루프 변수에는 암시적 타입을 사용하세요.
    다음 예제는 for 문에서 암시적 타입을 사용합니다.
    ```csharp
    var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
    var manyPhrases = new StringBuilder();
    for (var i = 0; i < 10000; i++)
    {
        manyPhrases.Append(phrase);
    }
    // Console.WriteLine("tra" + manyPhrases);
    ```
 - foreach 루프에서 루프 변수의 타입을 결정하기 위해 암시적 타입을 사용하지 마세요. 대부분의 경우 컬렉션의 요소 타입이 즉시 명확하지 않습니다. 컬렉션의 이름만으로 요소의 타입을 유추해서는 안 됩니다.
    다음 예제는 `foreach` 문에서 명시적 타입을 사용합니다.
    ```csharp
    foreach (char ch in laugh)
    {
        if (ch == 'h')
            Console.Write("H");
        else
            Console.Write(ch);
    }
    Console.WriteLine();
    ```
 - LINQ 쿼리의 결과 시퀀스에는 암시적 타입을 사용하세요. LINQ 관련 섹션에서는 많은 LINQ 쿼리가 암시적 타입을 사용해야 하는 익명 타입을 생성한다고 설명합니다. 다른 쿼리는 중첩된 제네릭 타입을 생성하므로 `var`가 더 읽기 쉽습니다.
    ```
    주의
    반복 가능한 컬렉션의 요소 타입을 실수로 변경하지 않도록 주의하세요. 예를 들어, foreach 문에서 `System.Linq.IQueryable`에서 `System.Collections.IEnumerable`로 전환하면 쿼리 실행 방식이 변경됩니다.
    ```
일부 샘플은 표현식의 자연 타입을 설명합니다. 이러한 샘플은 컴파일러가 자연 타입을 선택하도록 `var`를 사용해야 합니다. 이러한 예제는 덜 명확하더라도, 샘플에서는 `var` 사용이 필요합니다. 텍스트에서 해당 동작을 설명해야 합니다.

#### Place the using directives outside the namespace declaration

using 지시문이 네임스페이스 선언 외부에 있을 때, 해당 네임스페이스는 완전히 정규화된 이름으로 임포트됩니다. 완전히 정규화된 이름이 더 명확합니다. using 지시문이 네임스페이스 내부에 있을 때는 해당 네임스페이스에 상대적이거나 완전히 정규화된 이름일 수 있습니다.

```csharp
using Azure;

namespace CoolStuff.AwesomeFeature
{
    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
```

WaitUntil 클래스에 대한 참조(직접 또는 간접)가 있다고 가정합니다.

이제 약간 변경해봅시다:

```csharp
namespace CoolStuff.AwesomeFeature
{
    using Azure;

    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
```

이 코드는 오늘도, 내일도 컴파일됩니다. 하지만 다음 주 어느 시점에 이 이전(수정되지 않은) 코드는 두 가지 오류로 실패합니다:

- 오류 CS0246: 'WaitUntil' 유형 또는 네임스페이스 이름을 찾을 수 없습니다. (using 지시문이나 어셈블리 참조가 누락되었습니까?)
- 오류 CS0103: 현재 컨텍스트에 'WaitUntil'이라는 이름이 존재하지 않습니다.

의존성 중 하나가 .Azure로 끝나는 네임스페이스에 이 클래스를 도입했습니다:

```csharp
namespace CoolStuff.Azure
{
    public class SecretsManagement
    {
        public string FetchFromKeyVault(string vaultId, string secretId) { return null; }
    }
}
```

네임스페이스 내부에 배치된 using 지시문은 컨텍스트에 민감하며 이름 해석을 복잡하게 만듭니다. 이 예제에서는 첫 번째로 발견되는 네임스페이스입니다.

- CoolStuff.AwesomeFeature.Azure
- CoolStuff.Azure
- Azure

CoolStuff.Azure 또는 CoolStuff.AwesomeFeature.Azure와 일치하는 새 네임스페이스를 추가하면 글로벌 Azure 네임스페이스보다 먼저 일치합니다. using 선언에 global:: 수정자를 추가하여 이를 해결할 수 있습니다. 하지만, using 선언을 네임스페이스 외부에 배치하는 것이 더 쉽습니다.

```csharp
namespace CoolStuff.AwesomeFeature
{
    using global::Azure;

    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
```

### Style guidelines

일반적으로, 코드 샘플에는 다음 형식을 사용하세요:

- 들여쓰기는 네 칸의 공백을 사용하세요. 탭을 사용하지 마세요.
- 코드 정렬을 일관되게 하여 가독성을 높이세요.
- 문서에서 코드 가독성을 높이기 위해 줄 길이를 65자로 제한하세요, 특히 모바일 화면에서.
- 긴 문장은 여러 줄로 나누어 명확성을 높이세요.
- 중괄호는 "Allman" 스타일을 사용하세요: 여는 중괄호와 닫는 중괄호는 각각 새로운 줄에 위치시킵니다. 중괄호는 현재 들여쓰기 수준에 맞춥니다.
- 필요하다면 이항 연산자 앞에서 줄 바꿈을 하세요.

#### Comment style

 - 간단한 설명에는 한 줄 주석(//)을 사용하세요.
 - 긴 설명에는 여러 줄 주석(/* */)을 피하세요. 주석은 현지화되지 않습니다. 대신, 긴 설명은 동반 기사에 포함됩니다.
 - 메서드, 클래스, 필드 및 모든 공개 멤버를 설명할 때는 XML 주석을 사용하세요.
 - 주석은 코드 줄 끝이 아닌 별도의 줄에 배치하세요.
 - 주석 텍스트는 대문자로 시작하세요.
 - 주석 텍스트는 마침표로 끝내세요.
 - 주석 구분자(//)와 주석 텍스트 사이에 공백 하나를 삽입하세요, 다음 예제와 같이.
    ```csharp
    // The following declaration creates a query. It does not run
    // the query.
    ```

#### Layout conventions

좋은 레이아웃은 코드의 구조를 강조하고 코드를 더 읽기 쉽게 만드는 형식을 사용합니다. Microsoft 예제 및 샘플은 다음 규칙을 준수합니다:

- 기본 코드 편집기 설정(스마트 들여쓰기, 네 문자 들여쓰기, 공백으로 저장된 탭)을 사용하세요. 자세한 내용은 옵션, 텍스트 편집기, C#, 서식을 참조하세요.
- 한 줄에 하나의 문장만 작성하세요.
- 한 줄에 하나의 선언만 작성하세요.
- 연속 줄이 자동으로 들여쓰기가 되지 않으면, 한 탭 스톱(네 칸 공백) 들여쓰기 하세요.
- 메서드 정의와 속성 정의 사이에 적어도 한 줄의 공백을 추가하세요.
- 표현식에서 절이 명확히 드러나도록 괄호를 사용하세요, 다음 코드와 같이.
    ```csharp
    if ((startX > endX) && (startX > previousX))
    {
        // Take appropriate action.
    }
    ```
예외는 연산자나 표현식의 우선순위를 설명하는 샘플일 때입니다.

---
## How to display command-line arguments

명령줄에서 실행 파일에 제공된 인수는 최상위 문 또는 Main에 대한 선택적 매개 변수를 통해 액세스할 수 있습니다. 인수는 문자열 배열의 형태로 제공됩니다. 배열의 각 요소에는 하나의 인수가 포함되어 있습니다. 인수 사이의 공백은 제거됩니다. 예를 들어 명령줄에서 다음과 같이 가상 실행 파일을 호출한다고 가정합니다.

| 령줄 입력                          | Main에 전달되는 문자열 배열  |
|--------------------------------|--------------------|
| executable.exe a b c           | "a"<br>"b"<br>"c"  |
| executable.exe one two         | "one"<br>"two"     |
| executable.exe "one two" three | "one two"<br>"three"|

### Example

이 예제에서는 명령줄 애플리케이션에 전달된 명령줄 인수를 표시합니다. 위의 표에서 첫 번째 항목에 대한 출력이 표시됩니다.

```C#
// The Length property provides the number of array elements.
Console.WriteLine($"parameter count = {args.Length}");

for (int i = 0; i < args.Length; i++)
{
    Console.WriteLine($"Arg[{i}] = [{args[i]}]");
}

/* Output (assumes 3 cmd line args):
    parameter count = 3
    Arg[0] = [a]
    Arg[1] = [b]
    Arg[2] = [c]
*/
```

---
## Explore object oriented programming with classes and objects

이 자습서에서는 콘솔 애플리케이션을 빌드하고 C# 언어의 일부인 기본 개체 지향 기능을 확인합니다.

### Create your application

터미널 창을 사용하여 Classes라는 디렉터리를 만듭니다. 이 디렉터리에서 애플리케이션을 빌드할 것입니다. 해당 디렉터리로 이동하여 콘솔 창에 `dotnet new console`을 입력하세요. 이 명령어는 애플리케이션을 생성합니다. `Program.cs` 파일을 엽니다. 다음과 같이 보일 것입니다:

```csharp
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

이 튜토리얼에서는 은행 계좌를 나타내는 새로운 타입을 생성할 것입니다. 일반적으로 개발자는 각 클래스를 다른 텍스트 파일에 정의합니다. 이렇게 하면 프로그램이 커질 때 관리가 더 쉬워집니다. Classes 디렉터리에 `BankAccount.cs`라는 새 파일을 만드세요.

이 파일은 은행 계좌의 정의를 포함할 것입니다. 객체 지향 프로그래밍은 클래스를 형태로 타입을 만들어 코드를 구성합니다. 이러한 클래스는 특정 엔티티를 나타내는 코드를 포함합니다. `BankAccount` 클래스는 은행 계좌를 나타냅니다. 이 코드는 메서드와 속성을 통해 특정 작업을 구현합니다. 이 튜토리얼에서 은행 계좌는 다음과 같은 기능을 지원합니다:

- 은행 계좌를 고유하게 식별하는 10자리 번호가 있습니다.
- 소유자 이름을 저장하는 문자열이 있습니다.
- 잔액을 조회할 수 있습니다.
- 예금을 수락합니다.
- 인출을 수락합니다.
- 초기 잔액은 양수여야 합니다.
- 인출은 잔액을 음수로 만들 수 없습니다.

### Define the bank account type

클래스의 기본 동작을 정의하는 기본 요소를 생성하는 것으로 시작할 수 있습니다. File:New 명령을 사용하여 새 파일을 만듭니다. 파일 이름을 `BankAccount.cs`로 지정하세요. `BankAccount.cs` 파일에 다음 코드를 추가하세요:

```csharp
namespace Classes;

public class BankAccount
{
    public string Number { get; }
    public string Owner { get; set; }
    public decimal Balance { get; }

    public void MakeDeposit(decimal amount, DateTime date, string note)
    {
    }

    public void MakeWithdrawal(decimal amount, DateTime date, string note)
    {
    }
}
```

계속하기 전에, 지금까지 만든 것을 살펴봅시다. 네임스페이스 선언은 코드를 논리적으로 조직하는 방법을 제공합니다. 이 튜토리얼은 비교적 작기 때문에 모든 코드를 하나의 네임스페이스에 넣을 것입니다.

`public class BankAccount`는 생성할 클래스 또는 타입을 정의합니다. 클래스 선언 다음의 `{`와 `}` 내부에 있는 모든 것은 클래스의 상태와 동작을 정의합니다. `BankAccount` 클래스에는 다섯 개의 멤버가 있습니다. 처음 세 개는 속성입니다. 속성은 데이터 요소이며 유효성 검사나 기타 규칙을 강제하는 코드를 가질 수 있습니다. 마지막 두 개는 메서드입니다. 메서드는 단일 기능을 수행하는 코드 블록입니다. 각 멤버의 이름을 읽으면 클래스가 무엇을 하는지에 대해 충분한 정보를 제공해야 합니다.

### Open a new account

구현할 첫 번째 기능은 은행 계좌를 여는 것입니다. 고객이 계좌를 열 때는 초기 잔액과 그 계좌의 소유자 정보가 필요합니다.

BankAccount 타입의 새 객체를 생성하려면, 이러한 값을 할당하는 생성자를 정의해야 합니다. 생성자는 클래스와 동일한 이름을 가지며, 해당 클래스 타입의 객체를 초기화하는 데 사용됩니다. BankAccount 타입에 다음 생성자를 추가하세요. MakeDeposit 선언 위에 다음 코드를 추가하세요:

```csharp
public BankAccount(string name, decimal initialBalance)
{
    this.Owner = name;
    this.Balance = initialBalance;
}
```

위의 코드는 `this` 한정자를 포함하여 생성되는 객체의 속성을 식별합니다. 이 한정자는 보통 선택 사항이며 생략할 수 있습니다. 다음과 같이 작성할 수도 있습니다:

```csharp
public BankAccount(string name, decimal initialBalance)
{
    Owner = name;
    Balance = initialBalance;
}
```

`this` 한정자는 로컬 변수나 매개변수가 해당 필드나 속성과 동일한 이름을 가질 때만 필요합니다. 이 기사 전체에서는 필요하지 않는 한 `this` 한정자를 생략합니다.

생성자는 `new`를 사용하여 객체를 생성할 때 호출됩니다. `Program.cs`에서 `Console.WriteLine("Hello World!");` 줄을 다음 코드로 교체하세요 ( `<name>`을 자신의 이름으로 대체):

```csharp
using Classes;

var account = new BankAccount("<name>", 1000);
Console.WriteLine($"Account {account.Number} was created for {account.Owner} with {account.Balance} initial balance.");
```

지금까지 만든 것을 실행해 봅시다. Visual Studio를 사용하는 경우, 디버그 메뉴에서 "디버그하지 않고 시작"을 선택하세요. 명령줄을 사용하는 경우, 프로젝트를 생성한 디렉터리에서 `dotnet run`을 입력하세요.

계좌 번호가 비어 있는 것을 확인했습니까? 이를 수정할 때입니다. 계좌 번호는 객체가 생성될 때 할당되어야 합니다. 그러나 호출자가 이를 생성하는 책임을 지지 않아야 합니다. BankAccount 클래스 코드가 새로운 계좌 번호를 할당하는 방법을 알아야 합니다. 간단한 방법은 10자리 숫자로 시작하여 각 새로운 계좌가 생성될 때마다 증가시키는 것입니다. 마지막으로, 객체가 생성될 때 현재 계좌 번호를 저장합니다.

BankAccount 클래스에 멤버 선언을 추가하세요. BankAccount 클래스의 시작 부분에서 여는 중괄호 `{` 다음에 다음 코드를 추가하세요:

```csharp
private static int s_accountNumberSeed = 1234567890;
```

accountNumberSeed는 데이터 멤버입니다. 이는 private으로, BankAccount 클래스 내부의 코드에서만 접근할 수 있습니다. 이는 공용 책임(계좌 번호를 갖는 것)과 비공용 구현(계좌 번호가 생성되는 방법)을 분리하는 방법입니다. 또한 static으로, 모든 BankAccount 객체에 의해 공유됩니다. 비정적 변수의 값은 각 BankAccount 객체 인스턴스마다 고유합니다. accountNumberSeed는 private static 필드이며, C# 명명 규칙에 따라 `s_` 접두사를 가집니다. `s`는 static을, `_`는 private 필드를 나타냅니다. 생성자에 다음 두 줄을 추가하여 계좌 번호를 할당하세요. `this.Balance = initialBalance;` 줄 다음에 배치하세요:

```csharp
Number = s_accountNumberSeed.ToString();
s_accountNumberSeed++;
```

`dotnet run`을 입력하여 결과를 확인하세요.

### Create deposits and withdrawals

귀하의 은행 계좌 클래스는 올바르게 작동하기 위해 예금과 인출을 수락해야 합니다. 예금과 인출을 구현하기 위해 계좌의 모든 거래를 기록하는 저널을 만듭니다. 각 거래를 추적하는 것은 단순히 잔액을 업데이트하는 것보다 몇 가지 장점이 있습니다. 거래 기록은 모든 거래를 감사하고 일일 잔액을 관리하는 데 사용할 수 있습니다. 필요할 때 모든 거래의 기록에서 잔액을 계산하면 단일 거래에서 발생한 오류가 수정될 경우 다음 계산 시 잔액에 올바르게 반영됩니다.

우선 거래를 나타내는 새 타입을 만듭니다. 거래는 몇 가지 속성을 가진 단순한 타입입니다. `Transaction.cs`라는 새 파일을 만드세요. 다음 코드를 추가하세요:

```csharp
namespace Classes;

public class Transaction
{
    public decimal Amount { get; }
    public DateTime Date { get; }
    public string Notes { get; }

    public Transaction(decimal amount, DateTime date, string note)
    {
        Amount = amount;
        Date = date;
        Notes = note;
    }
}
```

이제 `BankAccount` 클래스에 `Transaction` 객체의 `List<T>`를 추가합니다. `BankAccount.cs` 파일의 생성자 다음에 다음 선언을 추가하세요:

```csharp
private List<Transaction> _allTransactions = new List<Transaction>();
```

이제 잔액을 올바르게 계산합니다. 현재 잔액은 모든 거래의 값을 합산하여 찾을 수 있습니다. 현재 코드로는 계좌의 초기 잔액만 가져올 수 있으므로, 잔액 속성을 업데이트해야 합니다. `BankAccount.cs`의 `public decimal Balance { get; }` 줄을 다음 코드로 교체하세요:

```csharp
public decimal Balance
{
    get
    {
        decimal balance = 0;
        foreach (var item in _allTransactions)
        {
            balance += item.Amount;
        }

        return balance;
    }
}
```

이 예제는 속성의 중요한 측면을 보여줍니다. 이제 다른 프로그래머가 값을 요청할 때 잔액을 계산합니다. 계산은 모든 거래를 열거하고 합계를 현재 잔액으로 제공합니다.

다음으로 `MakeDeposit` 및 `MakeWithdrawal` 메서드를 구현합니다. 이 메서드들은 초기 잔액이 양수여야 하며, 인출이 잔액을 음수로 만들지 않아야 한다는 두 가지 규칙을 적용합니다.

이 규칙들은 예외의 개념을 도입합니다. 메서드가 작업을 성공적으로 완료할 수 없음을 나타내는 표준 방법은 예외를 던지는 것입니다. 예외의 유형과 관련 메시지가 오류를 설명합니다. 여기에서 `MakeDeposit` 메서드는 예금 금액이 0보다 크지 않으면 예외를 던집니다. `MakeWithdrawal` 메서드는 인출 금액이 0보다 크지 않거나 인출을 적용할 때 잔액이 음수가 되면 예외를 던집니다. `_allTransactions` 목록 선언 다음에 다음 코드를 추가하세요:

```csharp
public void MakeDeposit(decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException(nameof(amount), "Amount of deposit must be positive");
    }
    var deposit = new Transaction(amount, date, note);
    _allTransactions.Add(deposit);
}

public void MakeWithdrawal(decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException(nameof(amount), "Amount of withdrawal must be positive");
    }
    if (Balance - amount < 0)
    {
        throw new InvalidOperationException("Not sufficient funds for this withdrawal");
    }
    var withdrawal = new Transaction(-amount, date, note);
    _allTransactions.Add(withdrawal);
}
```

`throw` 문은 예외를 던집니다. 현재 블록의 실행이 종료되고, 제어는 호출 스택에서 첫 번째 일치하는 `catch` 블록으로 이동합니다. 이 코드를 테스트하기 위해 나중에 `catch` 블록을 추가할 것입니다.

생성자는 잔액을 직접 업데이트하는 대신 초기 거래를 추가하도록 변경해야 합니다. 이미 `MakeDeposit` 메서드를 작성했으므로 생성자에서 이를 호출합니다. 완성된 생성자는 다음과 같습니다:

```csharp
public BankAccount(string name, decimal initialBalance)
{
    Number = s_accountNumberSeed.ToString();
    s_accountNumberSeed++;

    Owner = name;
    MakeDeposit(initialBalance, DateTime.Now, "Initial balance");
}
```

`DateTime.Now`는 현재 날짜와 시간을 반환하는 속성입니다. 새 BankAccount를 생성하는 코드 뒤에 몇 가지 예금 및 인출을 추가하여 이 코드를 테스트하세요:

```csharp
account.MakeWithdrawal(500, DateTime.Now, "Rent payment");
Console.WriteLine(account.Balance);
account.MakeDeposit(100, DateTime.Now, "Friend paid me back");
Console.WriteLine(account.Balance);
```

그 다음, 음수 잔액으로 계좌를 생성하려고 시도하여 오류 조건을 테스트합니다. 앞서 추가한 코드 다음에 다음 코드를 추가하세요:

```csharp
// 초기 잔액이 양수여야 함을 테스트합니다.
BankAccount invalidAccount;
try
{
    invalidAccount = new BankAccount("invalid", -55);
}
catch (ArgumentOutOfRangeException e)
{
    Console.WriteLine("Exception caught creating account with negative balance");
    Console.WriteLine(e.ToString());
    return;
}
```

`try-catch` 문을 사용하여 예외를 던질 수 있는 코드 블록을 표시하고 예상되는 오류를 잡습니다. 같은 기술을 사용하여 음수 잔액에 대한 예외를 던지는 코드를 테스트할 수 있습니다. `invalidAccount` 선언 앞에 다음 코드를 추가하세요:

```csharp
// 음수 잔액에 대한 테스트.
try
{
    account.MakeWithdrawal(750, DateTime.Now, "Attempt to overdraw");
}
catch (InvalidOperationException e)
{
    Console.WriteLine("Exception caught trying to overdraw");
    Console.WriteLine(e.ToString());
}
```

파일을 저장하고 `dotnet run`을 입력하여 시도해 보세요.

### Challenge - log all transactions

이 튜토리얼을 마치기 위해, 거래 내역을 위한 문자열을 생성하는 `GetAccountHistory` 메서드를 작성할 수 있습니다. 이 메서드를 `BankAccount` 타입에 추가하세요:

```csharp
public string GetAccountHistory()
{
    var report = new System.Text.StringBuilder();

    decimal balance = 0;
    report.AppendLine("Date\t\tAmount\tBalance\tNote");
    foreach (var item in _allTransactions)
    {
        balance += item.Amount;
        report.AppendLine($"{item.Date.ToShortDateString()}\t{item.Amount}\t{balance}\t{item.Notes}");
    }

    return report.ToString();
}
```

이 히스토리는 `StringBuilder` 클래스를 사용하여 각 거래에 대해 한 줄을 포함하는 문자열을 형식화합니다. 이 튜토리얼에서 문자열 형식 지정 코드를 이미 보았습니다. 새로운 문자는 `\t`입니다. 이는 출력을 형식화하기 위해 탭을 삽입합니다.

이 줄을 `Program.cs`에 추가하여 테스트하세요:

```csharp
Console.WriteLine(account.GetAccountHistory());
```

프로그램을 실행하여 결과를 확인하세요.

---
## Object-Oriented programming (C#)


---
## 출처
 - [C# 설명서>시작하기>C# 언어 둘러보기](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/)
 - [C# 설명서>시작하기>자습서>로컬 환경 설정](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/local-environment)
 - [C# 설명서>시작하기>자습서>C#에서 정수 및 부동 소수점 숫자를 사용하는 방법](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/numbers-in-csharp-local)
 - [C# 설명서>시작하기>자습서>C# if 문 및 루프 - 조건부 논리 자습서](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/branches-and-loops-local)
 - [C# 설명서>시작하기>자습서>C#에서 목록<T> 를 사용하여 데이터 수집을 관리하는 방법 알아보기](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/arrays-and-collections)
 - [C# 설명서>기본 사항>프로그램 구조>개요](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/#c-language-specification)
 - [C# 설명서>기본 사항>프로그램 구조>기본 메서드](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/main-command-line)
 - [C# 설명서>기본 사항>프로그램 구조>최상위문](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/top-level-statements)
 - [C# 설명서>기본 사항>형식 시스템>개요](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/)
 - [C# 설명서>기본 사항>형식 시스템>네임스페이스](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/namespaces)
 - [C# 설명서>기본 사항>형식 시스템>클래스](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/classes)
 - [C# 설명서>기본 사항>형식 시스템>레코드](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/records)
 - [C# 설명서>기본 사항>형식 시스템>인터페이스](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/interfaces)
 - [C# 설명서>기본 사항>형식 시스템>제너릭](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/generics)
 - [C# 설명서>기본 사항>형식 시스템>익명_형식](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/types/anonymous-types)
 - [C# 설명서>기본 사항>개체 지향 프로그래밍>클래스, 구조체, 레코드](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/object-oriented/)
 - [C# 설명서>기본 사항>개체 지향 프로그래밍>개체](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/object-oriented/objects)
 - [C# 설명서>기본 사항>개체 지향 프로그래밍>상속](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/object-oriented/inheritance)
 - [C# 설명서>기본 사항>개체 지향 프로그래밍>다형성](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/object-oriented/polymorphism)
 - [C# 설명서>기본 사항>기능 기술>패턴 일치](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/functional/pattern-matching)
 - [C# 설명서>기본 사항>기능 기술>무시 항목](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/functional/discards)
 - [C# 설명서>기본 사항>기능 기술>튜플 및 기타 형식 분해](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/functional/deconstruct)
 - [C# 설명서>기본 사항>예외 및 오류>개요](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/exceptions/)
 - [C# 설명서>기본 사항>예외 및 오류>예외 사용](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/exceptions/using-exceptions)
 - [C# 설명서>기본 사항>예외 및 오류>예외 처리](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/exceptions/exception-handling)
 - [C# 설명서>기본 사항>예외 및 오류>예외 만들기 및 throw](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/exceptions/creating-and-throwing-exceptions)
 - [C# 설명서>기본 사항>예외 및 오류>컴파일러 생성 예외](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/exceptions/compiler-generated-exceptions)
 - [C# 설명서>기본 사항>코딩 스타일>C# 식별자 이름](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/coding-style/identifier-names)
 - [C# 설명서>기본 사항>코딩 스타일>C# 코딩 규칙](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/coding-style/coding-conventions)
 - [C# 설명서>기본 사항>자습서>명령줄 인수를 표시하는 방법](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/tutorials/how-to-display-command-line-arguments)
 - [C# 설명서>기본 사항>자습서>클래스 소개](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/tutorials/classes)
 - [C# 설명서>기본 사항>자습서>개체 지향 C#](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/tutorials/oop)

---
## [다음](./05_MVC_디자인패턴_소개.md)