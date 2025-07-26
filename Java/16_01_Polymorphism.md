# 다형성 (Polymorphism)

##  개념 소개
- 객체지향 프로그래밍의 3대 특징: 캡슐화, 상속, **다형성**
- 다형성은 객체지향 프로그래밍의 **꽃** 
- **Polymorphism**: "여러 가지 형태를 가질 수 있는 성질"

##  다형성의 핵심 이론 2가지
1. **다형적 참조**
2. **메서드 오버라이딩 (Overriding)**

---

##  다형적 참조
### 1. 기본 예시
```java
Parent parent = new Parent();
Child child = new Child();
Parent poly = new Child();
```
- `Parent parent = new Parent()` → 부모 인스턴스
- `Child child = new Child()` → 자식 인스턴스 + 부모 클래스 포함
- `Parent poly = new Child()` → 부모 타입 변수로 자식 인스턴스 참조 = **다형적 참조**

### 2. 실행 예시
```java
poly.parentMethod(); // Parent 타입 메서드 호출
poly.childMethod();  // 컴파일 오류 (자식 메서드 직접 호출 불가)
```
- 자식 기능은 부모 타입 변수로 직접 호출 불가
- 해결: **다운캐스팅 필요**

### 3. 캐스팅
```java
Child child = (Child) poly;
child.childMethod();
```
- **업캐스팅**: 자식 → 부모 (자동)
- **다운캐스팅**: 부모 → 자식 (명시적 필요)

### 4. 일시적 다운캐스팅
```java
((Child) poly).childMethod();
```
- 한 줄로 즉시 호출 가능, 변수 선언 생략 가능

### 5. 캐스팅 주의점
```java
Parent parent2 = new Parent();
Child child2 = (Child) parent2; // 런타임 오류 (ClassCastException)
```
- 자식 객체가 실제로 생성되지 않았으면 다운캐스팅 불가능 → **런타임 오류 발생**

---

##  instanceof 연산자
```java
if (parent instanceof Child) {
    Child child = (Child) parent;
    child.childMethod();
}
```
- 객체가 특정 클래스의 인스턴스인지 확인
- 다운캐스팅 전에 필수적으로 체크하면 안전함

### 자바 16 이후 문법
```java
if (parent instanceof Child child) {
    child.childMethod();
}
```
- `instanceof` 검사와 동시에 다운캐스팅까지 수행

---

##  메서드 오버라이딩과 다형성
- **멤버 변수는 오버라이딩 안됨**, **메서드는 오버라이딩됨**

### 예시 코드
```java
Parent poly = new Child();
System.out.println(poly.value);     // Parent의 value 출력
poly.method();                      // Child의 method() 실행 (오버라이딩된 메서드가 우선권 가짐)
```

### 실행 결과
```
value = parent
Child.method
```
- `method()`는 자식 클래스에 오버라이딩되어 있으므로 **자식 클래스 메서드가 실행됨**
- `value`는 오버라이딩되지 않기 때문에 **Parent 클래스의 멤버가 사용됨**

---

##  정리
| 구분 | 설명 |
|------|------|
| 다형성 | 하나의 객체가 여러 타입으로 참조될 수 있음 |
| 다형적 참조 | 부모 타입으로 자식 인스턴스를 참조 |
| 업캐스팅 | 자식 → 부모 (자동, 생략 가능) |
| 다운캐스팅 | 부모 → 자식 (명시적 필요, 위험) |
| instanceof | 다운캐스팅 전 타입 확인 필수 |
| 메서드 오버라이딩 | 실행 시점에 실제 인스턴스의 메서드가 호출됨 (우선권) |
| 변수 접근 | 참조 변수 타입 기준으로 접근됨 (오버라이딩 안됨) |

---

##  추가 Tip
- 업캐스팅은 안전 → 부모의 메서드만 사용
- 다운캐스팅은 위험 → 반드시 instanceof로 체크
- 오버라이딩된 메서드는 다형적 참조 상황에서도 실제 인스턴스 기준으로 동작 → 진짜 다형성의 힘

---

## 예제 요약
### 1. 다형적 참조
```java
Parent poly = new Child();
poly.parentMethod(); // OK
poly.childMethod();  // X
```
### 2. 다운캐스팅
```java
Child child = (Child) poly;
child.childMethod(); // OK
```
### 3. instanceof
```java
if (poly instanceof Child) {
    ((Child) poly).childMethod();
}
```
### 4. 메서드 오버라이딩
```java
Parent poly = new Child();
poly.method(); // Child.method 실행됨
```

---

## ✅ 핵심 문장 요약
- **부모는 자식을 참조할 수 있다. 자식은 부모를 참조할 수 없다.**
- **오버라이딩된 메서드는 항상 우선권을 가진다.**
- **다운캐스팅은 반드시 instanceof로 체크한 후 사용한다.**
- **다형성은 좋은 코드 구조와 유연한 설계를 가능하게 해준다.**
