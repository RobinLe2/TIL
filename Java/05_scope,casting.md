# scope

### 스코프 존재 이유
- 비효율적인 메모리 활용을 줄이기 위해
- 코드 복잡성의 증가를 막기 위해

```java
public class While2_3 {
    public static void main(String[] args) {
        int sum = 0;
        int i = 1;
        int endNum = 3;

        while (i <= endNum) {
            sum += i;
            System.out.println("i= " + i + " sum =" + sum);
            i++;
        }

    }
}
```
-------
- 스코프의 관점으로 봤을 때 i는 while문 안에서만 사용된다. 하지만 i 스코프의 범위는 main() 메서도 전체가 된다. <br>
 따라서 불필요한 메모리가 활용된다. <br>
- 하지만  for 문을 사용하면 i가 for문 안의 스코프 범위만 사용됨.  <br>
  따라서 스코프의 점위를 제한하는 것이 메모리 사용과 유지보수 관점에서 좋다.

# 형변환 
- 작은 범위에서 큰 범위로 값을 넣을 수 있다. (자동형 변환)
- int -> long, double -> long
```java
public class Casting1 {
    public static void main(String[] args) {
        int intValue = 10;
        long longValue;
        double doubleValue;

        longValue = intValue; //int -> long
        System.out.println("longValue = " + longValue);

        doubleValue = intValue; // int -> double
        System.out.println("doubleValue = "+ doubleValue);

        doubleValue = 20L; // long => double
        System.out.println("doubleValue =" + doubleValue);
    }
}
```
### 데이터 타입의 강제 변환
- 큰 범위에서 작은 범위로 갈 때는 형 변환을 표시해 주어야한다.(명시적 형변환)
```java
public class Casting2 {
    public static void main(String[] args) {
        double doubleValue = 1.5;
        int intValue = 0;

        // intValue = doubleValue;  //컴파일 오류 발생
        intValue = (int)doubleValue;    // 형 변환
        System.out.println(intValue);
    }
}
```
- 형 변환을 한다고 해서 doubleValue 자체의 타입이 변경되거나 그 안에 있는 값이 변경되는 것은 아니다.
  doubleValue에서 읽은 값을 형 변환 하는것이다.
```java
public class Casting3 {
    public static void main(String[] args) {
        long maxIntValue = 2147483647; // int 최고값
        long maxIntOver = 2147483648L;   // int 최고값 + 1(초과)
        int intValue = 0;

        intValue = (int)maxIntValue; // 형 변환
        System.out.println("maxIntValue casting = " + intValue);
        intValue = (int)maxIntOver; // 형 변환
        System.out.println("maxIntOver casting = " + intValue);
    }
}
```
---
정상 범휘
- long maxIntValue 의 경우 int로 표현 할 수 있는 숫자 중 가장 큰 숫자인 2147483647을 입력했다.
  이 경우 int로 표현할 수 있는 범위 내에 있기 때문에 long -> int 로 형변환을 해도 아무런 문제가 없다.

초과 범위
- long maxIntValue의 경우 int로 표현 할 수 있는 가장 큰 숫자보다 큰 숫자를 입력했다.
  이 숫자는 리터럴 int의 범위를 넘어가기 때문에 마지막에 L을 붙여서 long형을 사용해야한다.
  이 경우에는  iong -> int로 형 변환하면 문제가 발생하게 된다.

기존 볌위를 초과해서 표현하게 되면 전혀 다른 숫자가 표현되는데, 이런 현상을 오버플로우라고 한다.<br>
이러한 오버플로우가 발생한 것 자체가 문제이다.   

### 계산과 형변환
- 같은 타입끼리의 계산은 같은 타입의 결과를 낸다
- 서로 다른 타입의 계산은 큰 범위로 자동 형 변환이 일어난다.
```java
public class Casting4 {
    public static void main(String[] args) {
        int div1 = 3/2 ;       // 1.5
        System.out.println("div1 = " + div1 ); // 1

        double div2 = 3/2 ;   // 1.5
        System.out.println("div2 = " + div2); // 1.0

        double div3 = 3.0 / 2; // 1.5
        System.out.println("div3 = " + div3);  // 1.5

        double div4 = (double)3 / 2; // 1.5
        System.out.println("div4 = " + div4);  // 1.5

        int a = 3;
        int b = 2;
        double result = (double) a / b;
        System.out.println("result = " + result); // 1.5
    }
}
```

