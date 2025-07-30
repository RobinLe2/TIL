
# TIL — `java.lang` 패키지와 `Object` 클래스 핵심 정리

## java.lang 패키지 소개
- 자바 언어의 가장 기본이 되는 라이브러리(클래스 묶음)  
- `lang`은 **Language**의 줄임말  
- java.lang 패키지는 **자동 임포트**되므로 `import` 구문 없이 사용 가능  
- 자주 쓰이는 대표 클래스들:
  - `Object` : 모든 자바 객체의 최상위 부모 클래스  
  - `String` : 문자열 처리  
  - `Integer`, `Long`, `Double` : 기본형을 객체로 감싸는 래퍼 타입  
  - `Class` : 클래스의 메타 정보 제공  
  - `System` : 시스템 관련 기본 기능 제공  

## import 생략 가능 예시
```java
package lang;
import java.lang.System;  // 생략 가능
public class LangMain {
    public static void main(String[] args) {
        System.out.println("hello java");
    }
}
```
```java
package lang;
public class LangMain {
    public static void main(String[] args) {
        System.out.println("hello java");  // import 없이도 동작
    }
}
```

---

## Object 클래스

### 기본 상속 구조
모든 클래스는 명시적 부모가 없을 경우 **묵시적으로 `Object`를 상속**받는다.
```java
public class Parent {
    public void parentMethod() {
        System.out.println("Parent.parentMethod");
    }
}
```
는 다음과 동일합니다:
```java
public class Parent extends Object {
    // ...
}
```

### `toString()` 호출 흐름
```java
Child child = new Child();
child.childMethod();
child.parentMethod();
String info = child.toString();
System.out.println(info);
```
- `toString()` 호출 시, Child → Parent → Object 순으로 메서드를 찾고 `Object.toString()` 실행  
- 기본 출력 형식: `패키지명.클래스명@hashCode`  
  예: `lang.object.Child@1a2b3c`

---

## 왜 Object가 모든 객체의 최상위 부모인가?

### 공통 기능 제공
- `toString()`, `equals()`, `getClass()` 등은 **모든 객체에 필요한 공통 메서드**  
- 일관된 이름과 기능 제공으로 개발 편의성, 코드 일관성 확보  

### 다형성의 기반
- `Object obj` 타입으로 **모든 객체 참조 가능**  
- 타입 구분 없이 공통 매개변수로 다룰 수 있음  

### 단점
- `obj.sound()`처럼 **자식 클래스 고유 메서드는 직접 호출 불가**  
- 다운캐스팅이 필요 → 코드 복잡도 증가

---

## 다형성 활용 예시
```java
Object obj = new Dog();
if (obj instanceof Dog dog) {
    dog.sound();  // 멍멍
} else if (obj instanceof Car car) {
    car.move();   // 자동차 이동
}
```

→ `Object` 배열도 가능:
```java
Object[] arr = { new Dog(), new Car(), new Object() };
size(arr);

private static void size(Object[] objects) {
    System.out.println("전달된 객체 수: " + objects.length);
}
```

---

## `toString()` 오버라이딩 활용
```java
public class Dog {
    private String dogName;
    private int age;

    @Override
    public String toString() {
        return "Dog{" +
               "dogName='" + dogName + '\'' +
               ", age=" + age +
               '}';
    }
}
```
- 오버라이딩하지 않으면 `Object.toString()` 사용  
- `System.out.println(obj)` 호출 시 자동으로 `toString()` 실행됨  

## ObjectPrinter 활용
```java
public class ObjectPrinter {
    public static void print(Object obj) {
        System.out.println("객체 정보 출력: " + obj.toString());
    }
}
```
- `Dog`, `Car`처럼 `toString()` 재정의된 클래스에 **추상적인 Object 의존 + 다형성 활용**  
- **OCP** (Open‑Closed Principle) 만족:
  - Open: 새로운 클래스 추가 및 `toString()` 오버라이딩 가능  
  - Closed: `ObjectPrinter`는 코드 변경 없이 유지 가능  

---

## `equals()` — 동일성 vs 동등성

| 구분   | 설명 |
|--------|------|
| 동일성 (Identity) | `==` 연산자, **참조 값** 비교 |
| 동등성 (Equality) | `equals()` 메서드, **논리적 동일성** 비교 |

### 기본 equals() 메서드
- `Object.equals()`는 `==` 기반 구현이므로 **동일성 비교만** 수행  

### equals() 오버라이딩 예시
```java
public class UserV2 {
    private String id;
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        UserV2 user = (UserV2) o;
        return Objects.equals(id, user.id);
    }
}
```
- `id` 값이 같으면 동등성을 `true`로 판단  
- 반드시 함께 재정의하는 `hashCode()`와 일관성 유지 필요

### equals() 구현 규칙
- **반사성**: `x.equals(x)`는 항상 `true`  
- **대칭성**: `x.equals(y)`가 `true`면 `y.equals(x)`도 `true`  
- **추이성**: `a.equals(b)` & `b.equals(c)`이면 `a.equals(c)`  
- **일관성**: 객체 상태가 변하지 않는 한 결과는 동일  
- **null 비교**: `x.equals(null)`은 `false`

---

## 문제 예제: `Rectangle` 클래스 구현

**RectangleMain**:
```java
Rectangle rect1 = new Rectangle(100, 20);
Rectangle rect2 = new Rectangle(100, 20);
System.out.println(rect1);
System.out.println(rect2);
System.out.println(rect1 == rect2);
System.out.println(rect1.equals(rect2));
```

**정답: Rectangle 클래스 구현**:
```java
public class Rectangle {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Rectangle r = (Rectangle) o;
        return width == r.width && height == r.height;
    }

    @Override
    public String toString() {
        return "Rectangle{" +
               "width=" + width +
               ", height=" + height +
               '}';
    }
}
```

---

## 기타 Object 주요 메서드
- `clone()` : 객체 복사 (잘 사용되지 않음)  
- `hashCode()` : `equals()`와 함께 사용 (컬렉션 성능에 영향)  
- `getClass()` : 클래스 정보 제공 (메타 정보용)  
- `notify()`, `notifyAll()`, `wait()` : **멀티스레드 동기화용 메서드**

---

###  요약
- `java.lang`은 자바 핵심 클래스 모음, **개발자가 import 없이 항상 사용 가능**  
- `Object` 클래스는 모든 클래스의 공통 부모로서 **공통 기능과 다형성 지원의 핵심**  
- `toString()`과 `equals()`는 오버라이딩을 통해 유용하게 확장 가능  
- `ObjectPrinter.print()` 예시는 **추상 의존 + OCP 기반 설계의 실용 사례**

