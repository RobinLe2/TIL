# 다형성2

##  개요
- 다형성의 진짜 힘은 "중복 제거", "유연한 설계", "확장성"에 있음
- 본 파트에서는 **상속**, **추상 클래스**, **인터페이스**, **다형적 참조**, **오버라이딩**을 활용하여
  중복을 제거하고, 유지보수하기 쉬운 코드를 만드는 방법을 학습함

---

##  다형성 미사용 예제: 중복의 문제
```java
Dog dog = new Dog();
Cat cat = new Cat();
Caw cow = new Cow();

System.out.println("동물 소리 테스트 시작");
dog.sound();
System.out.println("동물 소리 테스트 종료");

System.out.println("동물 소리 테스트 시작");
cat.sound();
System.out.println("동물 소리 테스트 종료");

System.out.println("동물 소리 테스트 시작");
cow.sound();
System.out.println("동물 소리 테스트 종료");
```
###  문제점
- 각 동물마다 반복되는 코드 존재
- 동물 추가 시 `sound()` 테스트 로직이 계속 중복됨
- 타입이 다르기 때문에 공통 메서드 사용 불가

---

## 다형성 활용1: 상속과 오버라이딩 도입

### `Animal` 클래스를 상속받는 구조
```java
public class Animal {
    public void sound() {
        System.out.println("동물 소리");
    }
}
```
```java
public class Dog extends Animal {
    @Override public void sound() { System.out.println("멍멍"); }
}
public class Cat extends Animal {
    @Override public void sound() { System.out.println("냐옹"); }
}
public class Cow extends Animal {
    @Override public void sound() { System.out.println("음매"); }
}
```

### 중복 제거된 메서드
```java
private static void soundAnimal(Animal animal) {
    System.out.println("동물 소리 테스트 시작");
    animal.sound();
    System.out.println("동물 소리 테스트 종료");
}
```

---

##  다형성 활용2: 배열과 for문

```java
Animal[] animals = {new Dog(), new Cat(), new Cow()};

for (Animal animal : animals) {
    soundAnimal(animal);
}
```

- **공통 타입인 `Animal`로 배열 생성 가능**
- **다형적 참조 + 오버라이딩**으로 각 동물의 소리 호출됨

---

##  추상 클래스 도입

### 문제점
- `Animal animal = new Animal();` ← 불필요한 인스턴스 생성 가능
- `sound()` 오버라이딩 누락 가능

### 해결: 추상 클래스 + 추상 메서드
```java
public abstract class AbstractAnimal {
    public abstract void sound(); // 반드시 오버라이딩
    public void move() {
        System.out.println("동물이 움직입니다.");
    }
}
```

- 인스턴스 생성 불가
- 자식 클래스는 `sound()` 반드시 오버라이딩

---

##  순수 추상 클래스

```java
public abstract class AbstractAnimal {
    public abstract void sound();
    public abstract void move();
}
```

- 모든 메서드 추상화 → **순수 추상 클래스**
- 오직 설계도(규약)로만 사용

---

##  인터페이스 도입

### 기존 순수 추상 클래스를 인터페이스로 대체
```java
public interface InterfaceAnimal {
    void sound();
    void move();
}
```

### 구현 예시
```java
public class Dog implements InterfaceAnimal {
    public void sound() { System.out.println("멍멍"); }
    public void move() { System.out.println("개 이동"); }
}
```

- `implements` 사용
- `InterfaceAnimal` 타입으로 다형적 참조 가능
- 모든 메서드 오버라이딩 강제됨

---

##  인터페이스 다중 구현

```java
public interface Fly {
    void fly();
}
public class Bird extends AbstractAnimal implements Fly {
    public void sound() { System.out.println("짹짹"); }
    public void fly() { System.out.println("새 날기"); }
}
```

- `extends` + `implements` 조합 가능
- 하나의 클래스가 여러 인터페이스 다중 구현 가능

---

##  다중 구현 충돌 문제 해결

- `InterfaceA` 와 `InterfaceB` 모두 `methodCommon()` 정의 가능
- 충돌 안 나는 이유: 인터페이스는 **기능 구현을 갖지 않음**
- 결국 구현은 하위 클래스가 수행 → 오버라이딩된 메서드 사용됨

---

## 📚 정리

| 요소 | 설명 |
|------|------|
| 다형성 | 하나의 타입으로 다양한 객체를 다룰 수 있음 |
| 추상 클래스 | 공통 기능 제공 + 오버라이딩 강제 가능 |
| 추상 메서드 | 오버라이딩 강제 (구현 없음) |
| 순수 추상 클래스 | 모든 메서드가 추상 → 설계도 역할 |
| 인터페이스 | 규약 제공, 다중 구현 가능 |
| 다중 구현 | 여러 인터페이스를 구현할 수 있음 |
| 다형적 참조 | 부모 타입으로 자식 인스턴스를 참조 가능 |
| 메서드 오버라이딩 | 실제 인스턴스의 메서드가 실행됨 |

---

##  핵심 문장 요약

- **다형성은 중복을 줄이고, 확장을 쉽게 한다**
- **추상 클래스는 생성 불가 + 오버라이딩 강제**
- **인터페이스는 규약 제공 + 다중 구현 가능**
- **좋은 설계는 변하지 않는 코드를 만드는 것**
