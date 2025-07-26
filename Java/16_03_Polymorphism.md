# 다형성과 설계

## 좋은 객체 지향 프로그래밍이란?
- 역할과 구현을 분리하여 유연하고 확장 가능한 구조로 작성하는 것
- 다형성을 활용하여 클라이언트 코드의 변경 없이 기능을 확장할 수 있음

---

## 다형성 - 역할과 구현 예제1: 단일 구현 종속

```java
Driver driver = new Driver();
K3Car k3Car = new K3Car();
driver.setK3Car(k3Car);
driver.drive();
```

- `Driver` 클래스가 `K3Car`에 직접 의존
- 차량이 변경되면 `Driver` 코드도 변경 필요

---

## 다형성 - 역할과 구현 예제2: if-else로 분기

```java
if (k3Car != null) {
    k3Car.startEngine();
} else if (model3Car != null) {
    model3Car.startEngine();
}
```

- 차량이 늘어날수록 조건 분기가 증가
- 변경에 취약한 구조

---

## 다형성 - 역할과 구현 예제3: 인터페이스 도입

### 인터페이스 정의
```java
public interface Car {
    void startEngine();
    void offEngine();
    void pressAccelerator();
}
```

### 구현 클래스
```java
public class K3Car implements Car {...}
public class Model3Car implements Car {...}
```

### 클라이언트 코드
```java
Driver driver = new Driver();
driver.setCar(new K3Car());
driver.drive();

driver.setCar(new Model3Car());
driver.drive();
```

- `Driver`는 `Car` 인터페이스만 참조 → 역할에만 의존
- 변경에 닫히고 확장에 열림 (OCP 원칙 준수)

---

## OCP (Open-Closed Principle)

| 개념 | 설명 |
|------|------|
| Open for extension | 새로운 기능 추가에 열려있음 |
| Closed for modification | 기존 코드 수정 없이 확장 가능 |

- `Car` 인터페이스를 구현하면 새로운 차량 추가 가능
- `Driver` 코드 수정 없이 새로운 구현체 사용 가능

---

## 전략 패턴 (Strategy Pattern)
- 알고리즘을 인터페이스로 정의하고, 구현체를 주입해서 런타임에 교체 가능
- `Car`가 전략 인터페이스, `Driver`는 전략을 사용하는 클라이언트

---

## 실전 문제1: 다형성을 이용한 메시지 발송

```java
public interface Sender {
    void sendMessage(String message);
}
```

```java
public class EmailSender implements Sender {
    public void sendMessage(String message) {
        System.out.println("메일을 발송합니다: " + message);
    }
}
```

```java
public class SmsSender implements Sender {
    public void sendMessage(String message) {
        System.out.println("SMS를 발송합니다: " + message);
    }
}
```

```java
public class FaceBookSender implements Sender {
    public void sendMessage(String message) {
        System.out.println("페이스북에 발송합니다: " + message);
    }
}
```

```java
Sender[] senders = {new EmailSender(), new SmsSender(), new FaceBookSender()};
for (Sender sender : senders) {
    sender.sendMessage("환영합니다!");
}
```

---

## 실전 문제2: 결제 시스템 개발

### 리팩토링 전
- 조건문으로 결제 수단 분기
- 수단이 추가될수록 `PayService` 코드가 늘어남

### 리팩토링 후

```java
public interface Pay {
    boolean pay(int amount);
}
```

```java
public class PayService {
    public void processPay(String option, int amount) {
        Pay pay = PayStore.findPay(option);
        boolean result = pay.pay(amount);
        if (result) {
            System.out.println("결제가 성공했습니다.");
        } else {
            System.out.println("결제가 실패했습니다.");
        }
    }
}
```

```java
public abstract class PayStore {
    public static Pay findPay(String option) {
        if (option.equals("kakao")) return new KakaoPay();
        else if (option.equals("naver")) return new NaverPay();
        else return new DefaultPay();
    }
}
```

- 새로운 결제 수단 추가 시 `PayStore`만 수정
- `PayService`는 변경 없음 → OCP 원칙 준수

---

## 실전 문제3: 사용자 입력 처리

```java
Scanner scanner = new Scanner(System.in);
while (true) {
    System.out.print("결제 수단을 입력하세요:");
    String option = scanner.nextLine();
    if (option.equals("exit")) break;

    System.out.print("결제 금액을 입력하세요:");
    int amount = scanner.nextInt();
    scanner.nextLine();

    payService.processPay(option, amount);
}
```

---

## 정리

| 항목 | 설명 |
|------|------|
| 다형성 | 클라이언트 코드의 변경 없이 구현 객체 교체 가능 |
| 인터페이스 | 역할 정의, 확장에 용이 |
| OCP 원칙 | 확장에는 열려있고 변경에는 닫혀 있음 |
| 전략 패턴 | 인터페이스를 통해 알고리즘 유연하게 교체 가능 |

- 다형성 + 인터페이스 설계 → 유지보수에 강한 구조
- 변화하는 부분(main, 설정)은 허용하되 핵심 로직은 그대로 유지
