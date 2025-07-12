# Method 메서드

***자바에서의 함수***

필요한 기능을 미리 정의해두고 필요할 때마다 호출해서 사용할 수 있다.
```java
public static int add(int a, int b) {  // 메서드 선언 = 메서드 이름, 반환타입, 매개변수(파라미터) 목록을 포함한다.
        System.out.println(a + "+" + b + " 연산 수행");    // 메서드 본문
        int sum = a + b;  
        return sum;

    }
```
`public static`
- `public` : 다른 클래스에서 호출할 수 있는 메서드라는 뜻이다. 접근 제어에서 학습한다.
-`static` : 객체를 생성하지 않고 호출할 수 있는 정적 메서드라는 뜻이다. 자세한 내용은 뒤에서 다룬다.
 -두 키워드의 자세한 내용은 뒤에서 다룬다. 지금은 단순하게 메서드를 만들 때 둘을 사용해야 한다고 생각하
   자.
`int add(int a, int b)`
- `int` : 반환 타입을 정의한다. 메서드의 실행 결과를 반환할 때 사용할 반환 타입을 지정한다.
- `add` : 메서드에 이름을 부여한다. 이 이름으로 메서드를 호출할 수 있다.
- `(int a, int b)` : 메서드를 호출할 때 전달하는 입력 값을 정의한다. 이 변수들은 해당 메서드 안에서만 
  사용된다. 이렇게 메서드 선언에 사용되는 변수를 영어로 파라미터(parameter), 한글로 매개변수라 한다.

***메서드 호출과 용어정리***<br>
메서드를 호출할 때는 다음과 같이 메서드에 넘기는 값과 매개변수(파라미터)의 타입이 맞아야 한다. 물론 넘기는 값과
매개변수(파라미터)의 순서와 갯수도 맞아야 한다.
```
호출: call("hello", 20)
메서드 정의: int call(String str, int age)
```
**인수(Argument)**<br>
여기서 `"hello"` , `20` 처럼 넘기는 값을 영어로 Argument(아규먼트), 한글로 인수 또는 인자라 한다.<br>

**매개변수(Parameter)**
메서드를 정의할 때 선언한 변수인 `String str` , `int age` 를 매개변수, 파라미터라 한다.
메서드를 호출할 때 인수를 넘기면, 그 인수가 매개변수에 대입된다.<br>

**용어정리**<br>
**인수**라는 용어는 '인’과 '수’의 합성어로, '들어가는 수’라는 의미를 가진다. 즉, 메서드 내부로 들어가는 값을 의미
한다. 인자도 같은 의미이다.<br><br>
**매개변수, parameter**는 '매개’와 '변수’의 합성어로, '중간에서 전달하는 변수’라는 의미를 가진다.<br>
즉, 메서드 호출부와 메서드 내부 사이에서 값을 전달하는 역할을 하는 변수라는 뜻이다.

### 매개변수가 없거나 반환 타입이 void인 경우
```java
package method;

public class Method2 {
    public static void main(String[] args) {
        printHeader();
        System.out.println("= 프로그램이 동작합니다 =");
        printFooter();
    }

    public static void printHeader() {
        System.out.println("= 프로그램을 시작합니다 =");
        return;
    }
    public static void printFooter() {
        System.out.println("= 프로그램을 종료합니다 =");
        return;
    }
}
```
---
모든 메서드는 항상 return을 호출해야한다. 그러나 반환 타입 void의 경우에는 예외로 생략해도 된다.<br>
자바 컴파일러가 반환 타입이 없는 경우에는 return을 마지막줄에 넣어주는데 이 때, return을 만나면 해당 메서드는 종료된다.

***return문을 만나면 즉시 메서드를 빠져나간다***
```java
 public static void main(String[] args) {
        checkAge(10);
        checkAge(20);
        
    }

    public static void checkAge(int age) {
        if (age < 18) {
            System.out.println(age + "살, 미성년자는 출입이 불가능합니다.");
            return;
        } 
        System.out.println(age+"살 입장하세요.");
        

    }
```
----
18세 미만의 경우 "미성년자는 출입이 불가능합니다"를 출력하고 바로 `return` 문이 수행된다. 따라서 다음 로직
을 수행하지 않고, 해당 메서드를 빠져나온다.<br>

18세 이상의 경우 "입장하세요"를 출력하고, 메서드가 종료된다. 참고로 반환 타입이 없는 `void` 형이기 때문에
마지막 줄의 `return` 은 생략할 수 있다.

## 자바에서는 항상 변수의 값을 복사해서 대입한다.

변수와 값 복사
다음 코드를 보고 어떤 결과가 나올지 먼저 생각해보자.
**MethodValue0**
```java
package method;
public class MethodValue0 {
public static void main(String[] args) {
int num1 = 5;
int num2 = num1;
num2 = 10;
System.out.println("num1=" + num1);
System.out.println("num2=" + num2);
}
}
```
**실행 결과**
```
num1=5
num2=10
```
**실행 과정**
```java
int num2 = num1; //num1의 값은 5이다. num1(5)
int num2 = 5; //num2 변수에 대입하기 전에 num1의 값 5를 읽는다. 결과: num1(5), num2(5)
num2 = 10; // num2에 10을 대입한다. 결과: num1(5), num2(10)
```
여기서 값을 복사해서 대입한다는 부분이 바로 이 부분이다.
```java
int num2 = num1;
```

이 부분은 생각해보면 `num1` 에 있는 값 `5` 를 복사해서 `num2` 에 넣는 것이다.<br>
복사한다고 표현한 이유는 `num1` 의 값을 읽어도 `num1` 에 있는 기존 값이 유지되고, 새로운 값이 `num2` 에
들어가기 때문이다. 마치 `num1` 의 값이 `num2` 에 복사가 된 것 같다.<br>
`num1` 이라는 변수 자체가 `num2` 에 들어가는 것이 아니다. `num1` 에 들어있는 값을 읽고 복사해서 `num2`
에 넣는 것이다.<br>
간단하게 `num1` 에 있는 값을 `num2` 에 대입한다고 표현한다. 하지만 실제로는 그 값을 복사해서 대입하는
것이다.<br>

```java
public class MethodValue1 {
    public static void main(String[] args) {
        int num1 = 5;
        System.out.println("1. changeNumber 호출 전, num1: "+ num1);
        changeNumber(num1);
        System.out.println("4. changeNumber  호출 후, num1: " + num1);
    }

    public static void changeNumber(int num2) {
        System.out.println("2. changeNumber 변경 전, num2: " + num2);
        num2 = num2 * 2;
        System.out.println("3. changeNumber 변경 후, num2: "+ num2);

    }
}
```
실행 과정 코드

```java
changeNumber(num1); //changeNumber를 호출한다. num1(5)
changeNumber(5); //num1의 값을 읽는다.
void changeNumber(int num2=5) //num1의 값 5가 num2에 복사된다. 결과: num1(5), num2(5)
num2 = num2 * 2; //num2에 2를 곱한다. 결과: num1(5), num2(5)
num2 = 5 * 2; //num2의 값을 읽어서 2를 곱한다. 결과: num1(5), num2(5)
num2 = 10; //num2에 계산 결과인 값 10을 대입한다. 결과: num1(5), num2(10)
num2를 출력한다: num2의 값인 10이 출력된다.
num1을 출력한다: num1의 값인 5가 출력된다.
```
결과적으로 매개변수 `num2` 의 값만 10으로 변경되고 `num1` 의 값은 변경되지 않고 기존 값인 5로 유지된다. 자바는 항
상 값을 복사해서 전달하기 때문에 `num2` 의 값을 바꾸더라도 `num1` 에는 영향을 주지 않는다.

----
```java
  public static void main(String[] args) {
        int number = 5;
        System.out.println("1. changeNumber 호출 전, number: "+ number);
        changeNumber(number);
        System.out.println("4. changeNumber  호출 후, number: " + number);
    }

    public static void changeNumber(int number) {
        System.out.println("2. changeNumber 변경 전, number: " + number);
        number = number * 2;
        System.out.println("3. changeNumber 변경 후, number: "+ number);

    }
```
이번에는 `main()` 에서 정희한 변수와 메서드의 매개변수(파라미터)의 이름이 둘다  `number`로 같다.

**실행 결과**
```
1. changeNumber 호출 전, number: 5
2. changeNumber 변경 전, number: 5
3. changeNumber 변경 후, number: 10
4. changeNumber 호출 후, number: 5
```
`main()`도 사실은 메서드이다. 각각의 메서드 안에서 사용하는 변수는 서로 완전히 분리된 다른 변수이다. 물론 이름
이 같아도 완전히 다른 변수다.<br>
따라서 `main()` 의 `number` 와 `changeNumber()` 의 `number` 는 서로 다른 변수이
다.


```java
public class MethodValue3 {
    public static void main(String[] args) {
        int num1 = 5;
        System.out.println("changeNumber 호출 전, num1: "+ num1);
        num1 = changeNumber(num1);
        System.out.println("changeNumber  호출 후, num1: " + num1);
    }

    public static int changeNumber(int num2) {
        num2 = num2 * 2;
        return num2;
    }
}
```
**실행 결과**
```
changeNumber 호출 전, num1: 5
changeNumber 호출 후, num1: 10
```
**실행 과정**
```java
num1 = changeNumber(num1); //num1(5)
num1 = changeNumber(5);
//호출 시작:changeNumber()
//num1의 값 5가 num2에 대입된다. num1의 값을 num2에 복사한다. num1(5), num2(5)
int changeNumber(int num2=5)
num2 = num2 * 2; //계산 결과: num1(5), num2(10)
return num2; // num2의 값은 10이다.
return 10;
//호출 끝: changeNumber()
num1 = changeNumber(5);//반환 결과가 10이다.
num1 = 10;//결과: num1(10)
```
---
꼭 기억하자! **자바는 항상 변수의 값을 복사해서 대입한다.**<br>
(참고로 뒤에서 참조형이라는 것을 학습하는데, 이때도 똑같다. 결국 참조형 변수에 있는 값인 **참조값을 복사**하는 것이
다! 이것은 나중에 알아본다.)

### 메서드와 형변환
메서드를 호출 할 때에도 형변환이 적용된다. 

```java
public class MethodCasting1 {
    public static void main(String[] args) {
        double number = 1.5;
        //printNumber(number).     // double을 int형에 대입하므로 컴파일 오류
        printNumber((int) number); // 명시적 형변환을 사용해 double을 int로 변환
    }
    public static void printNumber(int n) {
        System.out.println("숫자: " + n );
    }
}
```

자동 형변환<br>
`int < long < double`<br>
메서드를 호출할 때 매개변수에 값을 전달하는 것도 결국 변수에 값을 대입하는 것이다. 따라서 앞서 배운 자동 형변환
이 그대로 적용된다.

###메서드 오버로딩<br>
- 이름이 같고 매개변수가 다른 메서드를 여러개 정의하는 것<br>

***규칙***<br>
메서드의 이름이 같아도 매개변수의 타입 및 순서가 다르면 오버로딩이 가능하다. 참고로 반환 타입은 인정하지 않는다.<br>

`용어` <br>
메서드 시그니처<br>
`메서드 시그니처 = 메서드 이름 + 매개변수 타입(순서)`<br>
메서드를 구분할 수 있는 고유한 식별자나 서명<br>

```java
public class MethodOverloading3 {
    public static void main(String[] args) {
        System.out.println("1: " + add(1, 2));
        System.out.println("2: " + add(1.2, 1.5));

    }

    public static int add(int a, int b) {
        System.out.println("1번 호출");
        return a + b;
    }

    public static double add(double a, double b) {
        System.out.println("2번 호출");
        return  a + b;
    }
}
```
