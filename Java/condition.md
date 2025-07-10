# 조건문 (자바 if문, switch문, 삼항연산자)

## 조건문이란?
- 프로그램의 흐름을 분기(갈라지게)시키는 구문
- 특정 조건에 따라 코드 실행 여부 또는 실행 내용을 다르게 할 수 있음
- 대표적으로 `if문`, `switch문`, 삼항연산자가 있다.

---

## 1. if문, else문

### (1) if문의 기본 구조

```java
if (조건식) {
    // 조건식이 true(참)이면 실행
}
```
- 조건식은 반드시 true/false 결과가 나오는 식이어야 함

### (2) if-else문 구조

```java
if (조건식) {
    // 조건이 참일 때 실행
} else {
    // 조건이 거짓일 때 실행
}
```

### (3) 예제와 실행 흐름

```java
int age = 20;

if (age >= 18) {
    System.out.println("성인입니다.");
} else {
    System.out.println("미성년자입니다.");
}
```
- age가 20 → "성인입니다." 출력
- age가 15 → "미성년자입니다." 출력

#### if문 내부 동작 원리 (분석)

```java
if (age >= 18) { ... }
→ if (20 >= 18) { ... }
→ if (true) { ... }  // 블록 실행!
```
조건이 참이므로 실행  
else는 if가 거짓일 때만 실행

---

## 2. else if문

### (1) 여러 조건을 순서대로 검사할 때 사용

```java
int age = 14;

if (age <= 7) {
    System.out.println("미취학");
} else if (age <= 13) {
    System.out.println("초등학생");
} else if (age <= 16) {
    System.out.println("중학생");
} else if (age <= 19) {
    System.out.println("고등학생");
} else {
    System.out.println("성인");
}
```

- 위 코드는 위에서부터 차례로 조건을 검사하며, **가장 먼저 참이 되는 한 블록만 실행하고 종료**
- 예) age=14면 → "중학생"만 출력, 그 아래는 아예 검사하지 않고 넘어감

---

## 3. if문과 else if문의 차이 (독립조건 vs 연관조건)

- **연관된 조건(한 번만 실행):** if ~ else if ~ else
- **독립된 조건(여러 번 실행 가능):** if ~ if

### (1) 독립 if문 예시 (동시에 여러 조건 모두 실행 가능)

```java
int price = 10000;
int age = 10;
int discount = 0;

if (price >= 10000) {
    discount += 1000;
    System.out.println("10000원 이상 구매, 1000원 할인");
}
if (age <= 10) {
    discount += 1000;
    System.out.println("어린이 1000원 할인");
}
System.out.println("총 할인 금액: " + discount + "원");
```
- **두 조건 모두 충족 시 총 2000원 할인**

### (2) else if로 묶은 예시 (한 번만 실행)

```java
if (price >= 10000) {
    discount += 1000;
    System.out.println("10000원 이상 구매, 1000원 할인");
} else if (age <= 10) {
    discount += 1000;
    System.out.println("어린이 1000원 할인");
} else {
    System.out.println("할인 없음");
}
System.out.println("총 할인 금액: " + discount + "원");
```
- **첫 번째 조건만 만족하면 else if 이하 조건은 무시됨**

#### 정리
- 조건이 서로 독립이면 if~if로 각각
- 한 번만 실행되게 하려면 if~else if~else로 묶기

---

## 4. if문의 중괄호({}) 사용

- 한 줄만 실행할 때는 생략 가능
- 하지만 가독성 및 실수 방지를 위해 중괄호 `{}` 항상 쓰는 게 좋음

```java
if (true)
    System.out.println("한 줄이면 중괄호 생략 가능");

// 아래처럼 여러 줄이면 반드시 중괄호!
if (true) {
    System.out.println("여러 줄");
    System.out.println("이것도 if문에서 실행");
}
```

---

## 5. switch문

### (1) switch문 기본 구조

```java
switch (변수 또는 값) {
    case 값1:
        // 코드
        break;
    case 값2:
        // 코드
        break;
    default:
        // 모두 해당하지 않을 때 실행
}
```
- break로 각 case를 마무리
- default는 if문의 else와 동일한 역할

### (2) 예제 (회원 등급에 따른 쿠폰 지급)

```java
int grade = 2;
int coupon;
switch (grade) {
    case 1:
        coupon = 1000;
        break;
    case 2:
        coupon = 2000;
        break;
    case 3:
        coupon = 3000;
        break;
    default:
        coupon = 500;
}
System.out.println("발급받은 쿠폰 " + coupon);
```

### (3) break문이 없는 경우 (중복 처리 활용)
```java
switch (grade) {
    case 1:
        coupon = 1000;
        break;
    case 2: // break 없음!
    case 3:
        coupon = 3000; // 2, 3 둘 다 3000원 지급
        break;
    default:
        coupon = 500;
}
```

### (4) 자바 14 버전 switch문 (더 간단하게)

```java
int coupon = switch (grade) {
    case 1 -> 1000;
    case 2 -> 2000;
    case 3 -> 3000;
    default -> 500;
};
```
- break 없이 값만 바로 반환

### (5) if문 vs switch문 비교
- switch문은 **값이 정확히 일치하는 경우만 분기**  
- if문은 **비교, 범위, 복잡한 조건 등 자유롭게 사용**  
- 단순 값 분기에는 switch, 그 외엔 if문을 사용

---

## 6. 삼항 연산자 (조건 연산자)

- `if ~ else`처럼 단순히 참/거짓에 따라 값을 결정할 때 간단히 사용

```java
(조건식) ? 참_값 : 거짓_값
```

### (1) 예시: 나이에 따라 성인/미성년자
```java
int age = 18;
String status = (age >= 18) ? "성인" : "미성년자";
System.out.println("age = " + age + " status = " + status);
```

### (2) 더 큰 값 구하기
```java
int a = 10;
int b = 20;
int max = (a > b) ? a : b;
System.out.println("더 큰 숫자는 " + max + "입니다.");
```

### (3) 홀수/짝수 판별
```java
int x = 2;
String result = (x % 2 == 0) ? "짝수" : "홀수";
System.out.println("x = " + x + ", " + result);
```

- 삼항 연산자는 반드시 **값**만 나옴 (코드 블록 사용 불가)

---

## 7. 실전 연습문제 & 풀이

### (1) 학점 계산기
```java
int score = 85;
if (score >= 90) {
    System.out.println("학점은 A입니다.");
} else if (score >= 80) {
    System.out.println("학점은 B입니다.");
} else if (score >= 70) {
    System.out.println("학점은 C입니다.");
} else if (score >= 60) {
    System.out.println("학점은 D입니다.");
} else {
    System.out.println("학점은 F입니다.");
}
```

### (2) 거리별 교통수단 출력
```java
int distance = 25;
if (distance <= 1) {
    System.out.println("도보를 이용하세요.");
} else if (distance <= 10) {
    System.out.println("자전거를 이용하세요.");
} else if (distance <= 100) {
    System.out.println("자동차를 이용하세요.");
} else {
    System.out.println("비행기를 이용하세요.");
}
```

### (3) 환율 계산기
```java
int dollar = 10;
if (dollar < 0) {
    System.out.println("잘못된 금액입니다.");
} else if (dollar == 0) {
    System.out.println("환전할 금액이 없습니다.");
} else {
    int won = dollar * 1300;
    System.out.println("환전 금액은 " + won + "원입니다.");
}
```

### (4) 평점에 따른 영화 추천 (순차적 추천, 여러 조건 가능)
```java
double rating = 7.1;
if (rating <= 9) {
    System.out.println("'어바웃타임'을 추천합니다.");
}
if (rating <= 8) {
    System.out.println("'토이 스토리'를 추천합니다.");
}
if (rating <= 7) {
    System.out.println("'고질라'를 추천합니다.");
}
```
- rating이 7.1이라면 "어바웃타임", "토이 스토리" 모두 출력

### (5) 학점에 따른 성취도 (switch문)
```java
String grade = "B";
switch(grade) {
    case "A":
        System.out.println("탁월한 성과입니다!");
        break;
    case "B":
        System.out.println("좋은 성과입니다!");
        break;
    case "C":
        System.out.println("준수한 성과입니다!");
        break;
    case "D":
        System.out.println("향상이 필요합니다.");
        break;
    case "F":
        System.out.println("불합격입니다.");
        break;
    default:
        System.out.println("잘못된 학점입니다.");
}
```

### (6) 삼항 연산자로 더 큰 값, 홀짝 판별
```java
int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println("더 큰 숫자는 " + max + "입니다.");

int x = 2;
String result = (x % 2 == 0) ? "짝수" : "홀수";
System.out.println("x = " + x + ", " + result);
```

---

## 8. 핵심 요약 & 사용 팁

- **if문:** 조건이 다양하거나, 범위·복잡한 식이 필요할 때
- **else if:** 여러 조건 중 한 번만 실행할 때
- **독립 if문:** 여러 조건이 각각 적용될 때
- **switch문:** 값에 따라 간단히 분기할 때 (enum, 상수, 문자 등)
- **삼항연산자:** 단순 값 분기에 적합, 표현식 내에서 값 반환
- **가독성, 코드 실수를 막으려면 중괄호({})를 항상 쓰자**

---

