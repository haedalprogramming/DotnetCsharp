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
## 출처
 - [C# 설명서>시작하기>C# 언어 둘러보기](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/)
 - [C# 설명서>시작하기>자습서>로컬 환경 설정](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/local-environment)
 - [C# 설명서>시작하기>자습서>C#에서 정수 및 부동 소수점 숫자를 사용하는 방법](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/numbers-in-csharp-local)
 - [C# 설명서>시작하기>자습서>C# if 문 및 루프 - 조건부 논리 자습서](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/branches-and-loops-local)
 - [C# 설명서>시작하기>자습서>C#에서 목록<T> 를 사용하여 데이터 수집을 관리하는 방법 알아보기](https://learn.microsoft.com/ko-kr/dotnet/csharp/tour-of-csharp/tutorials/arrays-and-collections)
 - [C# 설명서>기본 사항>프로그램 구조>개요](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/#c-language-specification)
 - [C# 설명서>기본 사항>프로그램 구조>기본 메서드](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/main-command-line)
 - [C# 설명서>기본 사항>프로그램 구조>최상위문](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/top-level-statements)
---
## [다음](./08_환경설정.md)