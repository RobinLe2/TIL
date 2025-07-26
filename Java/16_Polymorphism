# Java 다형성 정리

---

## 1. 다형성의 개념

###  정의

- 다형성(Polymorphism)은 객체지향 프로그래밍의 핵심 개념 중 하나로, 하나의 객체가 여러 타입으로 동작할 수 있게 하는 성질.
- "여러 형태"를 가질 수 있다는 의미.

---

## 2. 다형성의 핵심 개념

### 2.1 다형적 참조

```java
Parent poly = new Child();
```

- 부모 타입의 변수 `poly`는 자식 타입의 인스턴스를 참조할 수 있음
- 이때 `poly`로는 부모 클래스에 정의된 메서드만 호출 가능

### 2.2 한계

```java
poly.childMethod(); // 컴파일 오류
```

- 자식의 고유 기능은 참조 타입이 부모일 경우 접근 불가

---

## 3. 업캐스팅과 다운캐스팅

### 3.1 업캐스팅 (자식 → 부모)

```java
Parent parent = new Child(); // 자동 형변환
```

- 안전하며 명시적 캐스팅 생략 가능

### 3.2 다운캐스팅 (부모 → 자식)

```java
Child child = (Child) parent;
child.childMethod();
```

- 명시적 캐스팅 필요
- 실행 시 `ClassCastException` 위험 있음

---

## 4. 다운캐스팅의 주의점

###  안전한 경우

```java
Parent parent = new Child();
Child child = (Child) parent; // OK
```

###  위험한 경우

```java
Parent parent = new Parent();
Child child = (Child) parent; // 런타임 오류 발생!
```

- 메모리에는 자식 정보가 없기 때문에 잘못된 참조로 오류 발생

---

## 5. instanceof로 타입 확인

```java
if (parent instanceof Child) {
    Child child = (Child) parent;
    child.childMethod();
}
```

- instanceof 연산자는 실제 인스턴스 타입을 확인할 수 있음
- Java 16부터는 Pattern Matching으로 다음과 같이 가능:

```java
if (parent instanceof Child child) {
    child.childMethod();
}
```

---

## 6. 다형성과 메서드 오버라이딩

### 예제

```java
class Parent {
    void method() {
        System.out.println("Parent method");
    }
}

class Child extends Parent {
    @Override
    void method() {
        System.out.println("Child method");
    }
}
```

### 호출 결과

```java
Parent poly = new Child();
poly.method(); // Child method
```

- 오버라이딩 된 메서드는 참조 타입과 상관없이 실제 인스턴스 기준으로 실행됨

---

## 7. 변수와 메서드 차이

```java
class Parent {
    String value = "parent";
    void method() {
        System.out.println("Parent.method");
    }
}
class Child extends Parent {
    String value = "child";
    @Override
    void method() {
        System.out.println("Child.method");
    }
}
```

- `poly.value` → "parent" (변수는 참조 타입 기준)
- `poly.method()` → "Child.method" (메서드는 인스턴스 타입 기준)

---

## 8. 정리

| 항목       | 설명                                            |
| ---------- | ----------------------------------------------- |
| 다형성     | 여러 타입의 객체를 하나의 타입으로 다룰 수 있음 |
| 업캐스팅   | 자식 → 부모 (자동, 안전)                        |
| 다운캐스팅 | 부모 → 자식 (명시적, 위험함)                    |
| instanceof | 캐스팅 전 안전 검사                             |
| 오버라이딩 | 인스턴스 타입 기준으로 메서드 결정              |
| 변수 참조  | 참조 변수 타입 기준                             |

---

## 9. 실전 활용 예시

###  전략 패턴

```java
interface PayStrategy {
    boolean pay(int amount);
}
class KakaoPay implements PayStrategy {
    public boolean pay(int amount) {
        System.out.println("카카오페이 결제: " + amount);
        return true;
    }
}
```

```java
PayStrategy pay = new KakaoPay();
pay.pay(10000);
```

###  메시지 전송

```java
interface Sender {
    void send(String to, String message);
}
class SmsSender implements Sender {
    public void send(String to, String message) {
        System.out.println("SMS: " + message + " to " + to);
    }
}
Sender sender = new SmsSender();
sender.send("010-1234-5678", "Hello!");
```

---

## 핵심 요약

- 다형성은 설계 유연성과 코드 확장성 향상
- 상속, 오버라이딩, 업/다운 캐스팅을 이해해야 제대로 쓸 수 있음
- instanceof로 안전하게 캐스팅
