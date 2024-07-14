# 객체지향 프로그래밍 실습 문제

# 목차
- [객체지향 프로그래밍 실습 문제](#객체지향-프로그래밍-실습-문제)
- [목차](#목차)
  - [객체지향 프로그래밍 실습 문제](#객체지향-프로그래밍-실습-문제-1)
    - [문제 1: 간단한 클래스 생성](#문제-1-간단한-클래스-생성)
    - [문제 2: 생성자와 필드](#문제-2-생성자와-필드)
    - [문제 3: 상속과 다형성](#문제-3-상속과-다형성)
    - [문제 4: 인터페이스와 다중 상속](#문제-4-인터페이스와-다중-상속)
    - [문제 5: 컬렉션과 제네릭](#문제-5-컬렉션과-제네릭)
  - [정답 코드](#정답-코드)
    - [문제 1: 간단한 클래스 생성](#문제-1-간단한-클래스-생성-1)
    - [문제 2: 생성자와 필드](#문제-2-생성자와-필드-1)
    - [문제 3: 상속과 다형성](#문제-3-상속과-다형성-1)
    - [문제 4: 인터페이스와 다중 상속](#문제-4-인터페이스와-다중-상속-1)
    - [문제 5: 컬렉션과 제네릭](#문제-5-컬렉션과-제네릭-1)
  - [프로젝트: 도서관 관리 시스템](#프로젝트-도서관-관리-시스템)
    - [요구사항 구현 단계](#요구사항-구현-단계)
  - [다음](#다음)

## 객체지향 프로그래밍 실습 문제


### 문제 1: 간단한 클래스 생성

**목표**: 클래스와 객체의 기본 개념을 이해하기

**문제**: 학생 클래스(Student)를 작성하세요. 이 클래스는 학생의 이름(name)과 나이(age)를 저장하는 필드를 가져야 합니다. 또한, 학생의 정보를 출력하는 메서드(DisplayInfo)도 포함해야 합니다.

```csharp
// Student 클래스 작성
public class Student
{
    // 여기에 코드를 작성하세요
}

class Program
{
    static void Main(string[] args)
    {
        Student student = new Student();
        student.Name = "Alice";
        student.Age = 20;
        student.DisplayInfo();
    }
}
```

### 문제 2: 생성자와 필드

**목표**: 생성자의 개념과 필드 초기화 방법을 이해하기

**문제**: 자동차 클래스(Car)를 작성하세요. 이 클래스는 자동차의 모델명(model), 색상(color), 그리고 최대 속도(maxSpeed)를 필드로 가져야 합니다. 생성자를 통해 필드를 초기화하고, 자동차의 정보를 출력하는 메서드(DisplayInfo)를 작성하세요.

```csharp
// Car 클래스 작성
public class Car
{
    // 여기에 코드를 작성하세요
}

class Program
{
    static void Main(string[] args)
    {
        Car car = new Car("Tesla", "Red", 250);
        car.DisplayInfo();
    }
}
```

### 문제 3: 상속과 다형성

**목표**: 상속과 다형성의 개념을 이해하기

**문제**: 동물 클래스(Animal)를 작성하세요. 이 클래스는 동물의 이름(name)과 소리(sound)를 필드로 가져야 합니다. 또한, MakeSound 메서드를 통해 소리를 출력하도록 합니다. 그리고 동물 클래스를 상속받는 고양이 클래스(Cat)와 개 클래스(Dog)를 작성하고, 각각의 고유한 소리를 출력하도록 합니다.

```csharp
// Animal 클래스 작성
public class Animal
{
    // 여기에 코드를 작성하세요
}

// Cat 클래스 작성
public class Cat : Animal
{
    // 여기에 코드를 작성하세요
}

// Dog 클래스 작성
public class Dog : Animal
{
    // 여기에 코드를 작성하세요
}

class Program
{
    static void Main(string[] args)
    {
        Animal myCat = new Cat("Kitty");
        Animal myDog = new Dog("Buddy");

        myCat.MakeSound();
        myDog.MakeSound();
    }
}
```

### 문제 4: 인터페이스와 다중 상속

**목표**: 인터페이스의 개념을 이해하고 다중 상속의 역할을 이해하기

**문제**: 움직일 수 있는(Movable) 인터페이스를 작성하세요. 이 인터페이스는 Move 메서드를 가져야 합니다. 자동차 클래스(Car)와 비행기 클래스(Airplane)를 작성하여 이 인터페이스를 구현하세요. 그리고 각각의 이동 방식을 출력하도록 합니다.

```csharp
// IMovable 인터페이스 작성
public interface IMovable
{
    // 여기에 코드를 작성하세요
}

// Car 클래스 작성
public class Car : IMovable
{
    // 여기에 코드를 작성하세요
}

// Airplane 클래스 작성
public class Airplane : IMovable
{
    // 여기에 코드를 작성하세요
}

class Program
{
    static void Main(string[] args)
    {
        IMovable car = new Car();
        IMovable airplane = new Airplane();

        car.Move();
        airplane.Move();
    }
}
```

### 문제 5: 컬렉션과 제네릭

**목표**: 제네릭 컬렉션의 사용법을 이해하기

**문제**: 학생 클래스를 사용하여 학생 리스트를 관리하는 프로그램을 작성하세요. 학생들을 리스트에 추가하고, 리스트를 순회하면서 학생들의 정보를 출력하세요.

```csharp
using System;
using System.Collections.Generic;

// Student 클래스 작성
public class Student
{
    // 여기에 코드를 작성하세요
}

class Program
{
    static void Main(string[] args)
    {
        List<Student> students = new List<Student>
        {
            // 여기에 학생 추가 코드를 작성하세요
        };

        foreach (var student in students)
        {
            student.DisplayInfo();
        }
    }
}
```

---

## 정답 코드

### 문제 1: 간단한 클래스 생성

```csharp
public class Student
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}
```

### 문제 2: 생성자와 필드

```csharp
public class Car
{
    public string Model { get; set; }
    public string Color { get; set; }
    public int MaxSpeed { get; set; }

    public Car(string model, string color, int maxSpeed)
    {
        Model = model;
        Color = color;
        MaxSpeed = maxSpeed;
    }

    public void DisplayInfo()
    {
        Console.WriteLine($"Model: {Model}, Color: {Color}, Max Speed: {MaxSpeed}");
    }
}
```

### 문제 3: 상속과 다형성

```csharp
public class Animal
{
    public string Name { get; set; }
    public string Sound { get; set; }

    public Animal(string name, string sound)
    {
        Name = name;
        Sound = sound;
    }

    public virtual void MakeSound()
    {
        Console.WriteLine($"{Name} says {Sound}");
    }
}

public class Cat : Animal
{
    public Cat(string name) : base(name, "Meow")
    {
    }
}

public class Dog : Animal
{
    public Dog(string name) : base(name, "Woof")
    {
    }
}
```

### 문제 4: 인터페이스와 다중 상속

```csharp
public interface IMovable
{
    void Move();
}

public class Car : IMovable
{
    public void Move()
    {
        Console.WriteLine("The car is driving.");
    }
}

public class Airplane : IMovable
{
    public void Move()
    {
        Console.WriteLine("The airplane is flying.");
    }
}
```

### 문제 5: 컬렉션과 제네릭

```csharp
using System;
using System.Collections.Generic;

public class Student
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}
```

## 프로젝트: 도서관 관리 시스템

**목표**: 도서관의 책과 회원을 관리하는 시스템을 설계하고 구현하기

**기능 요구사항**:
1. 책(Book)
   - 책의 제목(title), 저자(author), ISBN 번호(ISBN), 출판 연도(publication year)를 관리
   - 책 대여 상태를 확인 (대여 중인지 아닌지)
2. 회원(Member)
   - 회원의 이름(name), 회원 ID(member ID), 대여 중인 책 목록을 관리
3. 대여 관리
   - 책을 대여하고 반납하는 기능
   - 대여 중인 책의 목록을 확인
   - 특정 회원이 대여 중인 책의 목록을 확인
4. 검색 기능
   - 제목, 저자, ISBN을 통해 책을 검색
5. 보고서 기능
   - 특정 기간 동안 대여된 책의 목록을 출력

**설계 가이드**:
1. **클래스 설계**
   - Book 클래스
     - 필드: Title, Author, ISBN, PublicationYear, IsBorrowed
     - 메서드: Borrow, Return, DisplayInfo
   - Member 클래스
     - 필드: Name, MemberID, BorrowedBooks (List<Book>)
     - 메서드: BorrowBook, ReturnBook, DisplayInfo
   - Library 클래스
     - 필드: Books (List<Book>), Members (List<Member>)
     - 메서드: AddBook, AddMember, BorrowBook, ReturnBook, SearchBooks, GenerateReport

2. **상속 및 인터페이스**
   - IDisplayable 인터페이스: DisplayInfo 메서드를 포함
   - Book과 Member 클래스는 IDisplayable 인터페이스를 구현

3. **예외 처리**
   - 책을 대여하거나 반납할 때 발생할 수 있는 예외 처리 (예: 대여 중인 책을 다시 대여 시도, 대여하지 않은 책을 반납 시도)

**코드 스켈레톤**:

```csharp
using System;
using System.Collections.Generic;

public interface IDisplayable
{
    void DisplayInfo();
}

public class Book : IDisplayable
{
    public string Title { get; set; }
    public string Author { get; set; }
    public string ISBN { get; set; }
    public int PublicationYear { get; set; }
    public bool IsBorrowed { get; set; }

    public void Borrow()
    {
        // 여기에 대여 로직 작성
    }

    public void Return()
    {
        // 여기에 반납 로직 작성
    }

    public void DisplayInfo()
    {
        // 책 정보 출력
    }
}

public class Member : IDisplayable
{
    public string Name { get; set; }
    public string MemberID { get; set; }
    public List<Book> BorrowedBooks { get; set; } = new List<Book>();

    public void BorrowBook(Book book)
    {
        // 여기에 대여 로직 작성
    }

    public void ReturnBook(Book book)
    {
        // 여기에 반납 로직 작성
    }

    public void DisplayInfo()
    {
        // 회원 정보 출력
    }
}

public class Library
{
    public List<Book> Books { get; set; } = new List<Book>();
    public List<Member> Members { get; set; } = new List<Member>();

    public void AddBook(Book book)
    {
        // 여기에 책 추가 로직 작성
    }

    public void AddMember(Member member)
    {
        // 여기에 회원 추가 로직 작성
    }

    public void BorrowBook(string memberId, string isbn)
    {
        // 여기에 책 대여 로직 작성
    }

    public void ReturnBook(string memberId, string isbn)
    {
        // 여기에 책 반납 로직 작성
    }

    public List<Book> SearchBooks(string query)
    {
        // 여기에 검색 로직 작성
        return new List<Book>();
    }

    public void GenerateReport(DateTime startDate, DateTime endDate)
    {
        // 여기에 보고서 생성 로직 작성
    }
}

class Program
{
    static void Main(string[] args)
    {
        // 테스트용 코드 작성
    }
}
```

### 요구사항 구현 단계

1. **기본 클래스 및 메서드 구현**: Book, Member, Library 클래스와 메서드를 작성합니다.
2. **상속 및 인터페이스 적용**: IDisplayable 인터페이스를 적용하여 DisplayInfo 메서드를 각 클래스에 구현합니다.
3. **대여/반납 로직 작성**: Book과 Member 클래스에 대여 및 반납 로직을 추가합니다.
4. **검색 및 보고서 기능 구현**: Library 클래스에 검색 및 보고서 기능을 추가합니다.
5. **예외 처리**: 적절한 예외 처리를 추가하여 시스템의 안정성을 높입니다.
6. **테스트**: 다양한 시나리오를 통해 시스템을 테스트하고, 필요한 경우 디버깅 및 수정합니다.

---
## [다음](./05_MVC_디자인패턴_소개.md)

