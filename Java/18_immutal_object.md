# 불변 객체

## 📌 기본형과 참조형의 공유 기본형과 참조형의 공유
- **기본형(Primitive Type)**: 값 자체를 저장 → 절대 공유되지 않음
  - 예: `int a = 10; int b = a;` → b값 변경해도 a에는 영향 없음
- **참조형(Reference Type)**: 객체 주소(참조값)를 저장 → 여러 변수가 같은 객체를 참조 가능
  - 예: `Address a = new Address("서울"); Address b = a;` → 둘 다 같은 Address 객체 공유

## 📌 공유 참조와 사이드 이펙트 공유 참조와 사이드 이펙트
- 참조형은 **값을 공유**하기 때문에, 한 쪽에서 객체 변경 시 **다른 참조 변수에도 영향**이 감
- 사이드 이펙트(Side Effect): 예상치 못한 곳에서 값이 바뀌는 문제

## 📌 불변 객체 - 도입 불변 객체 - 도입
- 객체의 **값을 절대 변경할 수 없도록 만든 클래스**
- `setValue()` 같은 변경 메서드 제거
- 모든 필드는 `private final`
- 생성자로만 값 초기화 가능

## 📌 불변 객체 - 예제 불변 객체 - 예제
```java
public class ImmutableAddress {
    private final String value;

    public ImmutableAddress(String value) {
        this.value = value;
    }

    public String getValue() {
        return value;
    }
}
```
- 사용 예:
```java
ImmutableAddress a = new ImmutableAddress("서울");
ImmutableAddress b = a;
b = new ImmutableAddress("부산");
```
→ `a`는 여전히 "서울", `b`는 "부산" → 공유 안됨 → 안전

## 📌 불변 객체 - 값 변경 불변 객체 - 값 변경
- 기존 객체를 변경하는 대신 **새로운 객체를 반환**
```java
public class ImmutableObj {
    private final int value;

    public ImmutableObj(int value) {
        this.value = value;
    }

    public ImmutableObj add(int addValue) {
        return new ImmutableObj(this.value + addValue);
    }

    public int getValue() {
        return value;
    }
}
```
- 사용 예:
```java
ImmutableObj obj1 = new ImmutableObj(10);
ImmutableObj obj2 = obj1.add(20);
```
→ `obj1`: 10, `obj2`: 30

## 📌 문제와 풀이 
- 기존 `MyDate`는 `setYear()` 등으로 값이 변할 수 있음 → 불변 객체로 수정
```java
public class ImmutableMyDate {
    private final int year;
    private final int month;
    private final int day;

    public ImmutableMyDate(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }

    public ImmutableMyDate withYear(int year) {
        return new ImmutableMyDate(year, this.month, this.day);
    }

    public ImmutableMyDate withMonth(int month) {
        return new ImmutableMyDate(this.year, month, this.day);
    }

    public ImmutableMyDate withDay(int day) {
        return new ImmutableMyDate(this.year, this.month, day);
    }

    @Override
    public String toString() {
        return year + "-" + month + "-" + day;
    }
}
```
- 사용 예:
```java
ImmutableMyDate date1 = new ImmutableMyDate(2024, 1, 1);
ImmutableMyDate date2 = date1;
date1 = date1.withYear(2025);
```
→ `date2`: 2024-1-1, `date1`: 2025-1-1

## 정리 
- **불변 객체는 공유 가능하지만 값 변경이 불가능** → 사이드 이펙트 예방
- Java의 대표적인 불변 객체: `String`, `Integer`, `LocalDate` 등
- 모든 객체를 불변으로 만들 필요는 없음 → 필요할 때만 적용
- **멀티스레드 안정성**, **디버깅 용이성**, **값 타입처럼 사용 가능** 등의 장점

> 요약: 참조형 객체의 공유 문제를 피하려면 **값을 바꾸지 못하게 하는 불변 설계**가 해답
