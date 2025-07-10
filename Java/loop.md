# 자바 반복문 정리

## 반복문이란?
- 특정 코드를 여러 번 반복해서 실행할 때 사용하는 구문
- **자바의 반복문 종류:**  
  - `while`
  - `do-while`
  - `for`

---

## 1. while문

### 기본 구조
```java
while (조건식) {
    // 반복 실행할 코드
}
```
- 조건식이 **참(true)**이면 코드 블록을 실행  
- 거짓이 되면 반복문을 종료

### 예제
```java
int count = 0;
while (count < 3) {
    count++;
    System.out.println("현재 숫자는: " + count);
}
```
**출력**
```
현재 숫자는:1
현재 숫자는:2
현재 숫자는:3
```

---

## 2. do-while문

### 기본 구조
```java
do {
    // 반복 실행할 코드
} while (조건식);
```
- **무조건 한 번은 실행**  
- 이후 조건식을 검사해서 반복 여부 결정

### 예제
```java
int i = 10;
do {
    System.out.println("현재 숫자는: " + i);
    i++;
} while (i < 3);
```
**출력**
```
현재 숫자는:10
```

---

## 3. for문

### 기본 구조
```java
for (초기식; 조건식; 증감식) {
    // 반복 실행할 코드
}
```
- 초기식 → 조건식 → 코드실행 → 증감식 → 조건식 ...  
- **반복 횟수가 명확할 때 주로 사용**

### 예제
```java
for (int i = 1; i <= 10; i++) {
    System.out.println(i);
}
```
**출력**
```
1
2
...
10
```

---

## 4. break, continue

- **break:** 반복문 즉시 종료
- **continue:** 반복문의 나머지 부분을 건너뛰고, 다음 반복으로 이동

### break 예제
```java
int sum = 0, i = 1;
while (true) {
    sum += i;
    if (sum > 10) {
        System.out.println("합이 10보다 크면 종료: i=" + i + " sum=" + sum);
        break;
    }
    i++;
}
```

### continue 예제
```java
int i = 1;
while (i <= 5) {
    if (i == 3) {
        i++;
        continue;
    }
    System.out.println(i);
    i++;
}
```
**출력:**  
```
1
2
4
5
```

---

## 5. 중첩 반복문

- 반복문 안에 또 다른 반복문 가능

### 예제: 구구단
```java
for (int i = 1; i <= 9; i++) {
    for (int j = 1; j <= 9; j++) {
        System.out.println(i + " * " + j + " = " + (i * j));
    }
}
```

---

## 6. 반복문 연습 문제

### 자연수 출력
#### while문
```java
int count = 1;
while (count <= 10) {
    System.out.println(count);
    count++;
}
```
#### for문
```java
for (int count = 1; count <= 10; count++) {
    System.out.println(count);
}
```

---

### 짝수 출력
#### while문
```java
int num = 2, count = 1;
while (count <= 10) {
    System.out.println(num);
    num += 2;
    count++;
}
```
#### for문
```java
for (int num = 2, count = 1; count <= 10; num += 2, count++) {
    System.out.println(num);
}
```

---

### 1부터 N까지 누적합
#### while문
```java
int max = 100, sum = 0, i = 1;
while (i <= max) {
    sum += i;
    i++;
}
System.out.println(sum);
```
#### for문
```java
int max = 100, sum = 0;
for (int i = 1; i <= max; i++) {
    sum += i;
}
System.out.println(sum);
```

---

### 피라미드 출력
```java
int rows = 5;
for (int i = 1; i <= rows; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

## 7. while vs for

| 구분      | for문                                   | while문                                         |
| --------- | --------------------------------------- | ----------------------------------------------- |
| **장점**  | 반복 횟수 명확, 초기화/조건/증감 한 줄 | 복잡한 조건/종료 시점 명확하지 않을 때 적합     |
| **단점**  | 복잡한 반복 조건은 코드 가독성 떨어짐  | 초기화/조건/증감 코드가 분산됨, 실수 발생 가능  |

> **정해진 횟수 반복:** for문  
> **그 외 조건 반복:** while문

---

## 한줄 요약
- 반복 횟수가 명확하면 **for문**
- 그 외에는 **while문**

