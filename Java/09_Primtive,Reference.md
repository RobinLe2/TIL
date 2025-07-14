# Primitive type / Reference type
사용하는 값을 변수에 직접 넣을 수 있는 기본형, 그리고 이전에 본 `Student student1` 과 같이 객체가 저장된 메모리의 위치를 가리키는 참조값을 넣을 수 있
는 참조형으로 분류할 수 있다.<br>

***기본형(Primitive Type)*** : `int` , `long` , `double` , `boolean` 처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입을 기본형이라 한다.
***참조형(Reference Type)*** : `Student student1` , `int[] students` 와 같이 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터 타입을 참조형이라 한다. <br>
참조형은 객체 또는 배열에 사용된다.
- 객체는 `.` (dot)을 통해서 메모리 상에 생성된 객체를 찾아가야 사용할 수 있다.
- 배열은 `[]` 를 통해서 메모리 상에 생성된 배열을 찾아가야 사용할 수 있다.

----- 
기본형은 변수에 실제 값을 가지고 있기떄문에 직접 연산이 가능하지만<br>
참조형은 변수에 객체의 위치인 참조값이 들어가 있으므로 직접 계산이 불가능하다.<br>
다음과 같이 .을 통해 객체의 기본형 멤버 변수에 접근한 경우에는 연산을 할 수 있다.
```java
Student s1 = new Student();
s1.grade = 100;
Student s2 = new Student();
s2.grade = 90;
int sum = s1.grade + s2.grade; //연산 가능
```
## 자바는 항상 변수의 값을 복사해서 대입한다.
***변수 대입***
- 기본형과 참조형 모두 항상 변수에 있는 값을 복사해서 대입한다. 기본형이면 변수에 들어 있는 실제 값을 복사해서 대입하고,<br>
참조형이면 변수에 들어있는 참조값을 복사해서 대입한다.

***메서드 호출***
메서드 호출도 마찬가지이다. 메서드를 호출할 때 사용하는 매개변수(파라미터)도 결국 변수일 뿐이다.<br>
따라서 메서드를 호출할 때 매개변수에 값을 전달하는 것도 앞서 설명한 내용과 같이 값을 복사해서 전달한다.<br>

자바에서 메서드의 매개변수(파라미터)는 항상 값에 의해 전달된다. 그러나 이 값이 실제 값이냐, 참조(메모리 주소)값
이냐에 따라 동작이 달라진다. <br>
**기본형**: 메서드로 기본형 데이터를 전달하면, 해당 값이 복사되어 전달된다. 이 경우, 메서드 내부에서 매개변수
(파라미터)의 값을 변경해도, 호출자의 변수 값에는 영향이 없다.<br>
내 종이와 남의 종이 2개가 있는데, 내 종이에 있는 값을 옆 종이에 적어준다고해서 내 종이의 값은 바뀌지 않는다.
**참조형**: 메서드로 참조형 데이터를 전달하면, 참조값이 복사되어 전달된다. 이 경우, 메서드 내부에서 매개변수(파라미터)로 전달된 객체의 멤버 변수를 변경하면, 호출자의 객체도 변경된다.<br>
종이에 있는 주소지를 공유해주기때문에, 건물 내부의 설정을 바꾸면 내 건물의 설정도 바뀌게 된다.

------
활용

```java
Student student1 = createStudent("학생1", 15, 90) //메서드 호출후 결과 반환
Student student1 = student(x001) //참조형인 student를 반환
Student student1 = x001 //student의 참조값 대입
student1 = x001
```
`createStudent()` 는 생성한 `Student` 인스턴스의 참조값을 반환한다. 이렇게 반환된 참조값을 `student1` 변수에 저장했다.<br>
앞으로는 `student1` 을 통해 `Student` 인스턴스를 사용할 수 있다.


# 변수의 초기화
***멤버 변수*** : 자동 초기화<br>
인스턴스의 멤버 변수는 인스턴스를 생성할 때 자동으로 초기화된다.<br>
- 숫자(`int` )= `0` , `boolean` = `false` , 참조형 = `null` (`null` 값은 참조할 대상이 없다는 뜻으로 사용된다.)
- 개발자가 초기값을 직접 지정할 수 있다.<br>

***지역 변수*** : 수동 초기화 <br>
- 지역 변수는 항상 직접 초기화해야 한다

- #  null 과 참조형 변수

자바에서 참조형 변수는 항상 객체의 "주소값(참조값)"을 저장한다. 하지만 아직 객체를 생성하지 않았거나, 나중에 객체를 할당하고 싶다면 어떻게 해야 할까?

바로 `null` 을 사용하면 된다. `null`은 **"아직 아무것도 가리키고 있지 않다"**는 의미다.

## 예시 코드

```java
package ref;

public class Data {
    int value;
}
```

```java
package ref;

public class NullMain1 {
    public static void main(String[] args) {
        Data data = null;
        System.out.println("1. data = " + data);

        data = new Data();
        System.out.println("2. data = " + data);

        data = null;
        System.out.println("3. data = " + data);
    }
}
```

##  실행 결과
```
1. data = null
2. data = ref.Data@x001
3. data = null
```

---

##  코드 분석

###  `Data data = null`
- `Data` 타입의 참조형 변수 `data`를 선언하고 `null` 값을 할당
- **아직 어떤 객체도 가리키지 않음**

### `data = new Data();`
- `new` 키워드를 사용해 `Data` 클래스의 인스턴스를 생성
- 그 **객체의 주소값을 `data`에 할당**

### `data = null;`
- `data`가 가리키던 주소를 제거하고 다시 `null`로 설정
- 더 이상 `data`는 어떠한 객체도 가리키지 않음

---

##  GC(Garbage Collector)의 역할

- 위 코드에서 `data = null;` 이후, 생성되었던 `Data` 객체는 **아무도 참조하지 않게 됨**
- **JVM의 GC(Garbage Collector)**는 이런 객체를 **자동으로 메모리에서 제거**
- C 언어에서는 프로그래머가 수동으로 메모리 해제를 해야 했지만, 자바에서는 GC가 자동으로 처리

 **객체는 누군가 참조하는 한 살아 있고, 아무도 참조하지 않으면 GC가 제거한다.**

---

##  정리

- `null`은 참조형 변수가 아직 아무 객체도 가리키지 않음을 나타냄
- 객체를 `new`로 생성한 뒤에는 주소값이 변수에 저장됨
- 참조를 끊으면 GC가 메모리에서 객체를 제거함

```java
Data data = null;      // 아무것도 참조하지 않음
data = new Data();     // 객체 생성 후 참조
data = null;           // 다시 참조 끊음 → GC 대상
```

---

# NullPointerException

자바에서 가장 많이 발생하는 예외 중 하나는 `NullPointerException` 이다.  
`null` 은 아무 객체도 참조하지 않는 상태이고, 이 상태에서 객체의 멤버에 접근하면 예외가 발생한다.

## 예시 1 - 지역변수에서 null 예외

```java
package ref;

public class NullMain2 {
    public static void main(String[] args) {
        Data data = null;
        data.value = 10; // NullPointerException 예외 발생
        System.out.println("data = " + data.value);
    }
}
```

### 분석

```java
data.value = 10;
// ↓
// null.value = 10 (data는 null이므로)
```

- `null`은 아무 객체도 참조하지 않음
- 이 상태에서 `.value` 를 접근하려 하므로 `NullPointerException` 발생

### 실행 결과

```
Exception in thread "main" java.lang.NullPointerException: Cannot assign field "value" because "data" is null
	at ref.NullMain2.main(NullMain2.java:6)
```

## 예시 2 - 멤버 변수에서 null 예외

```java
package ref;

public class Data {
    int value;
}
```

```java
package ref;

public class BigData {
    Data data;
    int count;
}
```

```java
package ref;

public class NullMain3 {
    public static void main(String[] args) {
        BigData bigData = new BigData();

        System.out.println("bigData.count=" + bigData.count);   // 0
        System.out.println("bigData.data=" + bigData.data);     // null
        System.out.println("bigData.data.value=" + bigData.data.value); // 예외 발생
    }
}
```

### 실행 결과

```
bigData.count=0
bigData.data=null
Exception in thread "main" java.lang.NullPointerException: Cannot read field "value" because "bigData.data" is null
	at ref.NullMain3.main(NullMain3.java:10)
```

### 원인 분석

- `BigData bigData = new BigData();` → `data` 멤버는 참조형이라 자동으로 `null`로 초기화됨
- `bigData.data.value` → `data`가 `null`이므로 `.value` 접근 시 예외 발생

## 예시 3 - 예외 해결 방법

```java
package ref;

public class NullMain4 {
    public static void main(String[] args) {
        BigData bigData = new BigData();
        bigData.data = new Data(); // 객체 생성 및 할당

        System.out.println("bigData.count=" + bigData.count);         // 0
        System.out.println("bigData.data=" + bigData.data);           // ref.Data@주소
        System.out.println("bigData.data.value=" + bigData.data.value); // 0
    }
}
```

### 실행 결과

```
bigData.count=0
bigData.data=ref.Data@x002
bigData.data.value=0
```

### 실행 과정

```java
bigData.data.value
// bigData → x001
// x001.data → x002
// x002.value → 0
```

## 정리

- `NullPointerException` 은 **`null`에 대해 `.` (dot)을 사용했을 때 발생**
- 객체가 생성되지 않은 상태에서 필드나 메서드 접근은 모두 예외 발생의 원인
- 예외 해결을 위해서는 객체 생성 후 참조값을 할당해야 함

```java
MyClass obj = null;
obj.method(); // 예외 발생

obj = new MyClass();
obj.method(); // 정상 실행
```
