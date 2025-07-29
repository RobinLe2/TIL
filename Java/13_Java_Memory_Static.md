# 자바 메모리 구조와 static

## 1. 자바 메모리 구조

자바는 프로그램 실행 중 다음과 같은 메모리 영역을 사용합니다:

### 1.1 메서드 영역 (Method Area)
- 클래스의 바이트코드, static 변수, 메서드, 상수 풀 등이 저장됨
- 모든 인스턴스에서 공유되는 공간
- 프로그램 시작 시 생성되고 종료 시까지 유지됨

### 1.2 스택 영역 (Stack Area)
- 메서드 호출 시 생성되는 스택 프레임 저장
- 지역 변수 및 매개변수 저장
- 메서드 종료 시 해당 스택 프레임 제거됨
- 쓰레드별로 하나씩 존재

### 1.3 힙 영역 (Heap Area)
- `new` 키워드로 생성된 객체와 배열 저장
- 참조가 사라진 객체는 GC(가비지 컬렉션) 대상이 됨

### 예제: 스택 영역 사용

```java
public class JavaMemoryMain1 {
    public static void main(String[] args) {
        System.out.println("main start");
        method1(10);
        System.out.println("main end");
    }

    static void method1(int m1) {
        System.out.println("method1 start");
        int cal = m1 * 2;
        method2(cal);
        System.out.println("method1 end");
    }

    static void method2(int m2) {
        System.out.println("method2 start");
        System.out.println("method2 end");
    }
}
```

### 예제: 힙과 스택 함께 사용하는 경우

```java
public class Data {
    private int value;

    public Data(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }
}
```

```java
public class JavaMemoryMain2 {
    public static void main(String[] args) {
        System.out.println("main start");
        method1();
        System.out.println("main end");
    }

    static void method1() {
        System.out.println("method1 start");
        Data data1 = new Data(10);
        method2(data1);
        System.out.println("method1 end");
    }

    static void method2(Data data2) {
        System.out.println("method2 start");
        System.out.println("data.value=" + data2.getValue());
        System.out.println("method2 end");
    }
}
```

## 2. static 변수

### 인스턴스 변수로 count를 세면 공유되지 않음

```java
public class Data1 {
    public String name;
    public int count;

    public Data1(String name) {
        this.name = name;
        count++;
    }
}
```

### 외부 객체를 통해 공유 변수 활용

```java
public class Counter {
    public int count;
}
```

```java
public class Data2 {
    public String name;

    public Data2(String name, Counter counter) {
        this.name = name;
        counter.count++;
    }
}
```

### static 변수 사용

```java
public class Data3 {
    public String name;
    public static int count;

    public Data3(String name) {
        this.name = name;
        count++;
    }
}
```

```java
public class DataCountMain3 {
    public static void main(String[] args) {
        Data3 data1 = new Data3("A");
        Data3 data2 = new Data3("B");
        Data3 data3 = new Data3("C");

        System.out.println("총 객체 수: " + Data3.count);
    }
}
```

## 3. static 메서드

### 일반 메서드 예

```java
public class DecoUtil1 {
    public String deco(String str) {
        return "*" + str + "*";
    }
}
```

### static 메서드로 개선

```java
public class DecoUtil2 {
    public static String deco(String str) {
        return "*" + str + "*";
    }
}
```

```java
public class DecoMain2 {
    public static void main(String[] args) {
        String result = DecoUtil2.deco("hello java");
        System.out.println(result);
    }
}
```

## 4. static 메서드 내 제약사항

```java
public class DecoData {
    private int instanceValue;
    private static int staticValue;

    public static void staticCall() {
        // instanceValue++;  // 컴파일 오류
        // instanceMethod(); // 컴파일 오류
        staticValue++;
        staticMethod();
    }

    public void instanceCall() {
        instanceValue++;
        instanceMethod();
        staticValue++;
        staticMethod();
    }

    private void instanceMethod() {
        System.out.println("instanceValue=" + instanceValue);
    }

    private static void staticMethod() {
        System.out.println("staticValue=" + staticValue);
    }
}
```

## 5. 실습 문제

### 문제 1: 자동차 수량 세기

```java
public class Car {
    private static int totalCars;
    private String name;

    public Car(String name) {
        System.out.println("차량 구입, 이름: " + name);
        this.name = name;
        totalCars++;
    }

    public static void showTotalCars() {
        System.out.println("구매한 차량 수: " + totalCars);
    }
}
```

```java
public class CarMain {
    public static void main(String[] args) {
        Car car1 = new Car("K3");
        Car car2 = new Car("G80");
        Car car3 = new Car("Model Y");
        Car.showTotalCars();
    }
}
```

### 문제 2: 수학 유틸리티 클래스

```java
public class MathArrayUtils {
    private MathArrayUtils() {}

    public static int sum(int[] values) {
        int total = 0;
        for (int value : values) {
            total += value;
        }
        return total;
    }

    public static double average(int[] values) {
        return (double) sum(values) / values.length;
    }

    public static int min(int[] values) {
        int min = values[0];
        for (int value : values) {
            if (value < min) min = value;
        }
        return min;
    }

    public static int max(int[] values) {
        int max = values[0];
        for (int value : values) {
            if (value > max) max = value;
        }
        return max;
    }
}
```

```java
public class MathArrayUtilsMain {
    public static void main(String[] args) {
        int[] values = {1, 2, 3, 4, 5};
        System.out.println("sum=" + MathArrayUtils.sum(values));
        System.out.println("average=" + MathArrayUtils.average(values));
        System.out.println("min=" + MathArrayUtils.min(values));
        System.out.println("max=" + MathArrayUtils.max(values));
    }
}
```

## 6. 정리

| 변수 종류       | 저장 위치     | 생성 시점          | 생존 범위             | 접근 방법             |
|----------------|---------------|---------------------|------------------------|------------------------|
| 지역 변수       | 스택          | 메서드 호출 시      | 메서드 종료 시 제거   | 메서드 내에서만 접근  |
| 인스턴스 변수   | 힙            | new 시점            | 참조 없어질 때까지     | 참조변수.변수명        |
| static 변수     | 메서드 영역   | 클래스 로딩 시       | JVM 종료 시까지        | 클래스명.변수명        |

- static 메서드/변수는 인스턴스 없이 사용 가능
- 공통 기능 제공 시 유용
- `main()` 메서드도 static 메서드이다


## JVM 메모리 구조 (텍스트 도식)

        ┌────────────────────────────┐
        │        Method Area         │
        │────────────────────────────│
        │ - 클래스 정보               │
        │ - static 변수              │
        │ - 상수 풀(Constant Pool)   │
        │ - 메서드 바이트코드         │
        └────────────────────────────┘
                   ▲
                   │ 클래스 로딩 시

        ┌────────────────────────────┐
        │           Heap             │
        │────────────────────────────│
        │ - new 로 생성된 객체        │
        │ - 인스턴스 변수             │
        └────────────────────────────┘
                   ▲
                   │ 객체 생성 시

        ┌────────────────────────────┐
        │           Stack            │  (Thread 별)
        │────────────────────────────│
        │ - 지역 변수                 │
        │ - 매개변수                  │
        │ - 메서드 호출 프레임         │
        └────────────────────────────┘
                   ▲
                   │ 메서드 호출 시

        ┌────────────────────────────┐
        │  PC Register / Native Stack│
        │────────────────────────────│
        │ - 명령 주소 추적            │
        │ - 네이티브 메서드 스택       │
        └────────────────────────────┘

