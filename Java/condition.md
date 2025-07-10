## 조건문이란?
조건문이란 특정 조건에 따라 프로그램의 흐름(코드 실행 경로)이 달라지게 하는 구문

대표적으로 if, switch문이 있다


* 1. if문 기본

if (조건식) {
    // 조건이 참(true)일 때 실행되는 코드
}
예시 코드

```
package cond;
public class If1 {
    public static void main(String[] args) {
        int age = 20; // 사용자 나이

        if (age >= 18) {
            System.out.println("성인입니다.");
        }

        if (age < 18) {
            System.out.println("미성년자입니다.");
        }
    }
}
```
실행 결과

성인입니다.

age = 20이므로 첫 번째 if문만 실행
조건이 거짓이면 코드 블록이 실행되지 않는다

* 2. else문
if문의 조건이 거짓(false)일 때 실행할 코드를 작성할 수 있다

if (조건식) {
    // 참일 때 실행
} else {
    // 거짓일 때 실행
}
예시 코드

```
package cond;
public class If2 {
    public static void main(String[] args) {
        int age = 20;
        if (age >= 18) {
            System.out.println("성인입니다."); // 참일 때
        } else {
            System.out.println("미성년자입니다."); // 거짓일 때
        }
    }
}
```
실행 결과

성인입니다.

* 3. else if문
여러 조건을 순서대로 검사

위에서부터 순서대로 조건을 체크, 처음으로 참이 되는 코드만 실행하고 전체 if문을 빠져나감

```
if (조건1) {
    // 조건1 참
} else if (조건2) {
    // 조건2 참
} else if (조건3) {
    // 조건3 참
} else {
    // 모두 거짓
}
```

[문제] 나이에 따라 출력 다르게 하기
출력 조건

7세 이하: "미취학"

8~13세: "초등학생"

14~16세: "중학생"

17~19세: "고등학생"

20세 이상: "성인"

비효율적 코드(각 if문 독립, 비추천)

```
package cond;
public class If3 {
    public static void main(String[] args) {
        int age = 14;

        if (age <= 7) {
            System.out.println("미취학");
        }
        if (age >= 8 && age <= 13) {
            System.out.println("초등학생");
        }
        if (age >= 14 && age <= 16) {
            System.out.println("중학생");
        }
        if (age >= 17 && age <= 19) {
            System.out.println("고등학생");
        }
        if (age >= 20) {
            System.out.println("성인");
        }
    }
}
모든 조건을 다 검사함 → 비효율적
```

효율적 코드(else if 추천)

```
package cond;
public class If4 {
    public static void main(String[] args) {
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
    }
}
```

위에서부터 맞는 조건 한 번만 실행, 나머지는 검사 안 함
--

* 4. if, else if, else의 차이
if ~ else if ~ else : 연관된 조건, 최대 한 번만 실행

여러 개의 if문 : 독립 조건, 조건마다 모두 실행될 수 있음

할인 등 동시 적용해야 하는 경우에는 if문을 분리해서 사용!


[예제] 여러 조건이 동시에 적용되는 경우 (중복 if문)
문제

아이템 가격이 10,000원 이상 → 1,000원 할인

나이가 10세 이하 → 1,000원 추가 할인

각 조건이 모두 적용되어야 함!

```
package cond;
public class If5 {
    public static void main(String[] args) {
        int price = 10000; // 아이템 가격
        int age = 10;      // 나이
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
    }
}
```
실행 결과
10000원 이상 구매, 1000원 할인
어린이 1000원 할인
총 할인 금액: 2000원
두 조건 모두 해당 → 총 2000원 할인
--
else if 사용 시 주의
```
package cond;
public class If6 {
    public static void main(String[] args) {
        int price = 10000;
        int age = 10;
        int discount = 0;

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
    }
}
```
실행 결과
10000원 이상 구매, 1000원 할인
총 할인 금액: 1000원
첫 번째로 해당하는 조건만 적용됨. 두 조건이 모두 필요하다면 여러 개의 if문을 써야 함!
--

* 5. if문의 중괄호({}) 생략
명령문이 한 줄이면 중괄호 생략 가능
(하지만 가독성과 유지보수성 때문에 항상 중괄호 쓰는 것을 추천)

if (true)
    System.out.println("if문에서 실행됨");
아래 두 번째 문장은 if문과 상관없이 무조건 실행됨


if (true)
    System.out.println("if문에서 실행됨");
    System.out.println("if문에서 실행 안됨");

둘 다 if문에 포함하려면 반드시 {}로 묶기


if (true) {
    System.out.println("if문에서 실행됨");
    System.out.println("if문에서 실행 안됨");
}


if, else if, else

연관된 조건, 한 번만 실행

여러 개의 if문

독립 조건, 여러 번 실행 가능

조건문 안에서는 코드의 효율성과 요구사항(동시 적용 여부)에 따라 if문/else if문 선택

가독성 위해 항상 중괄호 {} 사용 권장
