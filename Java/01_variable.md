## 변수

```java
public class Var1 {
    public static void main(String[] args) {
        System.out.println(10);
        System.out.println(10);
        System.out.println(10);
    }
}
```
- 10을 3번 출력하는 대신 20으로 변경하고 싶다면?
- 사용자가 숫자를 입력하고, 그 숫자를 출력하고 싶다면?
-> 이를 위해 값을 보관해두고 필요할 때 값을 꺼내 읽을 수 있는 저장소가 필요함. 이를 변수라 한다.

```java
public class Var2 {
    public static void main(String[] args) {
        int a;  // 변수 선언
        a = 10; // 변수 초기화

        System.out.println(a);
        System.out.println(a);
        System.out.println(a);
    }
}
```
- a의 값을 변경하면 출력결과가 모두 함께 변경됨.

###  변수 선언
int a 
- 숫자 정수(integer)을 보관할 수 있는 이름이 a 인 데이터 저장소를 만든다.
- 변수를 만드는 것을 변수 선언이라고 한다.

a = 10;
- 자바에서 = 의 값은 오른쪽에 있는 값을 왼쪽에 저장한다는 뜻이다.
- 변수 a에 값 10을 저장한다.
- 선언 한 변수에 처음 값을 대입하는 것을 변수 초기화라고 함.

System.out.println(a) 
- 변수에 저장되어 있는 값을 읽음.

### 변수 값 변경

```java
public class Var3 {
    public static void main(String[] args) {
        int a; // 변수 선언
        a = 10; // 변수 초기화
        System.out.println(a);
        a= 50; // 변수 값 변경 a (10 -> 50)
        System.out.println(a);
    }
}
```
변수의 값을 변경하면 기존 값은 삭제가 된다.

### 변수 선언과 초기화
* 변수를 선언하면 컴퓨터의 메모리 공간을 확보하며 그 곳에 데이터를 저장한다.
- 변수를 선언할 때 하나씩 선언할 수도 있고, 여러개를 한 번에 선언할 수 있다.
* 변수 초기화는 선언한 변수에 처음으로 값을 저장하는 것이다.

```java
public class Var5 {
    public static void main(String[] args) {
        // 1. 변수 선언, 초기화 각각 따로
        int a;
        a = 1;
        System.out.println(a);

        int b = 2; // 2. 변수 선언과 초기화를 한번에
        System.out.println(b);

        int c = 3 , d =4 ; // 3. 여러 변수 선언과 초기화를 한번에
        System.out.println(c);
        System.out.println(d);
    }
}
```
#### 변수는 반드시 초기화 해야한다.

```java
public class Var6 {
    public static void main(String[] args) {
        int a;
        System.out.println(a);
    }
}
```
컴퓨터 메모리에는 이전에 어떤 값이 들어가 있었는 모른다.
따라서 초기화를 하지 않으면 이상한 값이 출력될 수 있어, 자바는 선언 후 변수를 초기화해주어야한다.

### 변수의 타입
```java
public class Var7 {
    public static void main(String[] args) {
        int a = 100;        // 정수
        double b = 10.5;    // 실수
        boolean c = true;   // 불리언(boolean) true, false 입력가능
        char d = 'A';       // 문자 하나 ' ' 작은 따옴표를 사용해서 감싸야한다.
        String e = "Hello Java"; // 문자열 , 문자열을 다루기 위한 특별한 타입

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
        System.out.println(d);
        System.out.println(e);
    }
}
```
- 데이터를 다루는 종류에 따른 다양한 형식
- 각 변수는 지정한 타입에 맞는 값을 사용해야한다.
* 리터럴 : 코드에 개발자가 직접 적은 100, 10.5, true, 'A', "Hello Java"  와 같은 고정된 값

```java
public class Var8 {
    public static void main(String[] args) {
        //정수
        byte b = 127; // -128 ~ 127
        short s = 32767; // -32,768 ~ 32,767
        int i = 2147483647; // -2,147,483,648 ~ 2,147,483,647 약(20억)
        long l = 9223372036854775807L;
        // -9223372036854775808 ~ 9223372036854775807

        //실수
        float f = 10.0f;
        double d =10.0;
    }
}
```
실무에서는 
- 정수 int, long
- 실수 double
- 문자열 String
- 불린형 boolean   들을 대부분 사용한다.

### 변수 명명 규칙
* 규칙
* 변수 이름은 숫자로 시작할 수 없다.
* 공백이 들어갈 수 없다.
* 예약어를 변수로 사용할 수 없다.
* 변수 이름에는 영문자, 숫자, 달러 기호 또는 밑줄만 사용할 수 있다.
* camelCase를 사용한다. (예시 orderDetail, myAccount)

  - 자바 언어 관례
  - 클래스는 첫 글자 대문자, 나머지는 모두 첫 글자 소문자로 시작 + camelCase
  - 예외) 상수 : 모두 대문자를 사용하고 언더바로 구분,  패키지 : 패키지는 모두 소문자를 사용
