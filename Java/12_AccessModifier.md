# Java - 접근 제어자 & 캡슐화

## 1. 접근 제어자란?
Java는 `public`, `private`, `protected`, `default`와 같은 접근 제어자를 제공한다.  
접근 제어자를 사용하면 클래스 외부에서 특정 필드나 메서드에 접근하는 것을 허용하거나 제한할 수 있다.

---

## 2. 접근 제어자의 필요성

### 예시: Speaker 클래스

- 음량은 최대 100까지만 증가해야 한다는 요구사항이 있음
- `volume` 필드가 외부에 노출되면, 메서드가 아닌 직접 값을 변경할 수 있어 위험

```java
public class Speaker {
    int volume;

    Speaker(int volume) {
        this.volume = volume;
    }

    void volumeUp() {
        if (volume >= 100) {
            System.out.println("음량을 증가할 수 없습니다. 최대 음량입니다.");
        } else {
            volume += 10;
            System.out.println("음량을 10 증가합니다.");
        }
    }

    void volumeDown() {
        volume -= 10;
    }

    void showVolume() {
        System.out.println("현재 음량: " + volume);
    }
}
```

**문제점:**  
다른 개발자가 아래처럼 직접 필드에 접근해서 잘못된 값을 넣을 수 있음.

```java
speaker.volume = 200; // 최대값 초과
```

---

## 3. 해결 방법: private 사용

```java
public class Speaker {
    private int volume;

    // 생성자 및 메서드는 동일
}
```

- `volume`을 `private`으로 감싸 외부 접근 차단
- 안전한 메서드를 통해서만 음량 조절 가능

---

## 4. 접근 제어자 종류

| 접근 제어자    | 설명                                                         |
|----------------|--------------------------------------------------------------|
| `private`      | 같은 클래스 내부에서만 접근 가능                             |
| `default`      | 같은 패키지 내부에서 접근 가능 (지정 안하면 기본 적용)       |
| `protected`    | 같은 패키지 or 다른 패키지의 자식 클래스에서 접근 가능       |
| `public`       | 모든 곳에서 접근 가능                                        |

접근 허용 범위 순서:  
`private` < `default` < `protected` < `public`

---

## 5. 접근 제어자 사용 예시

### 클래스: AccessData.java

```java
public class AccessData {
    public int publicField;
    int defaultField;
    private int privateField;

    public void publicMethod() {}
    void defaultMethod() {}
    private void privateMethod() {}

    public void innerAccess() {
        publicField = 100;
        defaultField = 200;
        privateField = 300;

        publicMethod();
        defaultMethod();
        privateMethod();
    }
}
```

- 내부에서는 모든 필드/메서드 접근 가능
- 외부에서는 접근 제어자에 따라 제약 발생

---

## 6. 클래스 레벨 접근 제어자

| 위치             | 사용 가능한 접근 제어자            |
|------------------|------------------------------------|
| 클래스 레벨      | `public`, `default` (package-private) |
| 메서드/필드/생성자 | `private`, `default`, `protected`, `public` |

**주의:**
- `public` 클래스는 파일 이름과 반드시 동일해야 함
- 한 파일에 `public` 클래스는 하나만 가능
- `default` 클래스는 파일 내에 여러 개 정의 가능

---

## 7. 캡슐화(Encapsulation)

### 정의
- 데이터(속성)와 기능(메서드)을 하나로 묶고 외부에서의 직접 접근을 제한하는 것
- 객체지향 프로그래밍의 핵심 원칙 중 하나

### 원칙
1. **데이터는 반드시 숨긴다 (`private`)**
2. **기능도 필요한 것만 공개한다 (`public`)**

### 예시: BankAccount 클래스

```java
public class BankAccount {
    private int balance;

    public void deposit(int amount) {
        if (isAmountValid(amount)) {
            balance += amount;
        }
    }

    public void withdraw(int amount) {
        if (isAmountValid(amount) && balance - amount >= 0) {
            balance -= amount;
        }
    }

    public int getBalance() {
        return balance;
    }

    private boolean isAmountValid(int amount) {
        return amount > 0;
    }
}
```

- `balance`는 외부에서 직접 접근할 수 없음
- `isAmountValid()`는 내부 유효성 검사용 메서드이므로 `private`

---

## 8. 실습 문제

### 문제 1: MaxCounter 클래스

**요구사항**
- 최대값까지만 증가 가능
- 필드들은 모두 `private`
- 외부에서 사용할 수 있도록 클래스는 `public`

```java
public class MaxCounter {
    private int count = 0;
    private int max;

    public MaxCounter(int max) {
        this.max = max;
    }

    public void increment() {
        if (count >= max) {
            System.out.println("최대값을 초과할 수 없습니다.");
            return;
        }
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

---

### 문제 2: 쇼핑카트 구현

**Item 클래스**

```java
public class Item {
    private String name;
    private int price;
    private int quantity;

    public Item(String name, int price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public int getTotalPrice() {
        return price * quantity;
    }
}
```

**ShoppingCart 클래스**

```java
public class ShoppingCart {
    private Item[] items = new Item[10];
    private int itemCount;

    public void addItem(Item item) {
        if (itemCount >= items.length) {
            System.out.println("장바구니가 가득 찼습니다.");
            return;
        }
        items[itemCount++] = item;
    }

    public void displayItems() {
        System.out.println("장바구니 상품 출력");
        for (int i = 0; i < itemCount; i++) {
            Item item = items[i];
            System.out.println("상품명:" + item.getName() + ", 합계:" + item.getTotalPrice());
        }
        System.out.println("전체 가격 합:" + calculateTotalPrice());
    }

    private int calculateTotalPrice() {
        int total = 0;
        for (int i = 0; i < itemCount; i++) {
            total += items[i].getTotalPrice();
        }
        return total;
    }
}
```

---

## 9. 정리 

- **접근 제어자**는 코드의 안정성과 정보 은닉을 위한 필수 도구이다.
- **캡슐화**를 통해 객체의 내부 구현을 숨기고, 필요한 기능만 외부에 제공한다.
- 좋은 프로그램은 자유도가 높은 것이 아니라 **적절한 제약이 있는 구조**이다.
