
# Java - 상속 (Inheritance)

## 1. 상속의 필요성

- 공통 기능을 **부모 클래스**에 정의하면 **중복 제거** 및 **유지보수** 용이
- 예시:
  ```java
  public class ElectricCar {
      public void move() { System.out.println("차를 이동합니다."); }
      public void charge() { System.out.println("충전합니다."); }
  }

  public class GasCar {
      public void move() { System.out.println("차를 이동합니다."); }
      public void fillUp() { System.out.println("기름을 주유합니다."); }
  }
  ```
  → `move()` 중복됨 → `Car` 클래스로 상위 추출

## 2. 기본 상속 구조

```java
public class Car {
    public void move() {
        System.out.println("차를 이동합니다.");
    }
}
public class ElectricCar extends Car {
    public void charge() {
        System.out.println("충전합니다.");
    }
}
public class GasCar extends Car {
    public void fillUp() {
        System.out.println("기름을 주유합니다.");
    }
}
```

## 3. 상속의 장점

- **코드 재사용** 가능
- **공통 기능 추가 시 부모 클래스만 수정**
- 새로운 클래스 확장(extend) 쉬움
  ```java
  public class HydrogenCar extends Car {
      public void fillHydrogen() {
          System.out.println("수소를 충전합니다.");
      }
  }
  ```

## 4. 메모리 구조

```java
ElectricCar car = new ElectricCar();
```

- 실제 메모리에는 `Car`와 `ElectricCar` 모두 포함됨
- 메서드 호출 시:
  - 현재 클래스에 없으면 → 부모 클래스에서 탐색
  - 못 찾으면 → 상위 상위로 계속 탐색
  - 그래도 없으면 → 컴파일 에러

## 5. 메서드 오버라이딩 (Overriding)

- 부모의 메서드를 자식 클래스에서 **재정의**
- `@Override` 애노테이션 사용 권장
  ```java
  public class ElectricCar extends Car {
      @Override
      public void move() {
          System.out.println("전기차를 빠르게 이동합니다.");
      }
  }
  ```

## 6. 오버로딩 vs 오버라이딩

| 구분       | 설명                                                         |
|------------|--------------------------------------------------------------|
| 오버로딩   | 메서드 이름은 같고, 매개변수 타입/순서/개수 다르게 정의       |
| 오버라이딩 | 상속받은 메서드 이름, 매개변수, 반환타입까지 동일하게 재정의 |

## 7. 메서드 오버라이딩 조건

- 메서드 이름, 매개변수, 반환타입 동일
- 접근 제어자는 부모보다 더 제한적일 수 없음
- `static`, `final`, `private` 메서드는 오버라이드 불가
- 생성자는 오버라이딩 불가

## 8. 접근 제어자와 상속

| 접근자     | 같은 클래스 | 같은 패키지 | 다른 패키지 (상속X) | 다른 패키지 (상속O) |
|------------|-------------|--------------|----------------------|----------------------|
| `private`  | O           | X            | X                    | X                    |
| (default)  | O           | O            | X                    | X                    |
| `protected`| O           | O            | X                    | O                    |
| `public`   | O           | O            | O                    | O                    |

## 9. super 키워드

- 부모의 메서드 또는 필드를 자식에서 사용할 때 `super` 사용
- 생성자에서 부모 생성자 호출 시 `super(...)`

## 10. 생성자 호출 순서

- 자식 생성자 → 부모 생성자 순서로 실행됨
- `super()`는 자식 생성자의 첫 줄에 위치해야 하며, 생략 시 기본 생성자 자동 호출됨

## 11. final 키워드

- `final class`: 상속 불가
- `final method`: 오버라이딩 불가
