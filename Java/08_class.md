# 클래스
***클래스가 필요한 이유***
```java
package class1;

public class ClassStart2 {
    public static void main(String[] args) {
        String[] studentNames = {"학생1", "학생2"};
        int[] studentAges = {15, 16};
        int[] studentGrade = {90, 80};

        for (int i = 0; i < studentNames.length; i++) {
            System.out.println("이름:" + studentNames[i] + " 나이:" + studentAges[i] + " 성적:" + studentGrade[i]);
        }
    }
}
```
위처럼 이름, 나이, 성적을 각각 따로 나누어서 관리하는 것은 사람이 관리하기 좋은 방식이 아니다. <br>
사람이 관리하기 좋은 방식은 학생이라는 개념을 하나로 묶는 것이다. 그리고 각각의 학생 별로 본인의 이름, 나이, 성적
을 관리하는 것이다.

```java
package class1;

public class Student {
    String name;
    int age;
    int grade;
}
```
***클래스***<br>
class 키워드를 사용해 학생 클래스(Student)를 정의한다.<br>
클래스에 정의한 변수들을 멤버변수, 또는 필드라 한다.
- 멤버 변수 : 이 변수들은 특정 클래스에 소속된 멤버이기에 이렇게 부른다.
- 필드: 데이터 항목을 가르키는 전통적인 용어이다.

```java
package class1;

public class ClassStart3 {
    public static void main(String[] args) {
        Student student1;
        student1 = new Student();
        student1.name = "학생1";
        student1.age = 15;
        student1.grade = 90;

        Student student2 = new Student();
        student2.name = "학생2";
        student2.age = 16;
        student2.grade = 80;

        System.out.println("이름: "+student1.name + " 나이: "+ student1.age + " 성적: " + student1.grade);
        System.out.println("이름: "+student2.name + " 나이: "+ student2.age + " 성적: " + student2.grade);
    }
}
```
**클래스와 사용자 정의 타입**<br>  
- 타입은 데이터의 종류나 형태를 나타낸다.
- `int` 라고 하면 정수 타입, `String` 이라고 하면 문자 타입이다.
- 클래스를 사용하면 `int`, `String` 과 같이 학생(`Student`)라는 타입을 직접 만들 수 있다.
- 사용자가 직접 정의하는 사용자 정의 타입을 만들려면 설계도가 필요하다. 이 **설계도가 바로 클래스**이다.
- 설계도인 클래스를 사용해서 **실제 메모리에 만들어진 실체를 객체 또는 인스턴스**라 한다.
- 클래스를 통해서 사용자가 원하는 종류의 데이터 타입을 마음껏 정의할 수 있다.<br>

**용어: 클래스, 객체, 인스턴스** 
- 클래스는 설계도이고, 이 설계도를 기반으로 실제 메모리에 만들어진 실체를 객체 또는 인스턴스라 한다. 둘다 같은 의
미로 사용된다.
- 여기서는 학생(`Student` ) 클래스를 기반으로 학생1(`student1` ), 학생2(`student2` ) 객체 또는 인스턴스를 만들었다.

***객체의 사용***<br>
객체에 접근하려면 .(점, dot) 키워드를 사용하면 된다. 변수에 들어있는 참조값을 읽어서 메모리에 존재하는 객체에 접근한다.<br>
```java
//1. 객체 값 읽기
System.out.println("이름:" + student1.name);
//2. 변수에 있는 참조값을 통해 실제 객체에 접근하고, name 멤버 변수에 접근한다.
System.out.println("이름:" + x001.name);
//3. 객체의 멤버 변수의 값을 읽어옴
System.out.println("이름:" + "학생1");
```


## 클래스-Class<br>
클래스는 객체를 생성하기 위한 '틀' 또는 '설계도'이다. 클래스는 객체가 가져야 할 속성(변수)과 기능(메서드)를 정의한다.<br>
예를 들어 학생이라는 클래스는 속성으로 `name` , `age` , `grade` 를 가진다. 참고로 기능(메서드)은 뒤에서 설명한
다. 지금은 속성(변수)에 집중하자<br>
틀: 붕어빵 틀을 생각해보자. 붕어빵 틀은 붕어빵이 아니다! 이렇게 생긴 붕어빵이 나왔으면 좋겠다고 만드는 틀일
뿐이다. 실제 먹을 수 있는 것이 아니다. 실제 먹을 수 있는 팥 붕어빵을 객체 또는 인스턴스라 한다.<br>
설계도: 자동차 설계도를 생각해보자. 자동차 설계도는 자동차가 아니다! <br>설계도는 실제 존재하는 것이 아니라 개념으로만 있는 것이다. 
설계도를 통해 생산한 실제 존재하는 흰색 테슬라 모델 Y 자동차를 객체 또는 인스턴스라 한다.<br>
## 객체 - Object<br>
객체는 클래스에서 정의한 속성과 기능을 가진 실체이다. 객체는 서로 독립적인 상태를 가진다.<br>
예를 들어 위 코드에서 `student1` 은 학생1의 속성을 가지는 객체이고, `student2` 는 학생2의 속성을 가지는 객체이다.
`student1` 과 `student2` 는 같은 클래스에서 만들어졌지만, 서로 다른 객체이다.<br>
## 인스턴스 - Instance<br>
인스턴스는 특정 클래스로부터 생성된 객체를 의미한다. 그래서 객체와 인스턴스라는 용어는 자주 혼용된다. 인스턴스는 
주로 객체가 어떤 클래스에 속해 있는지 강조할 때 사용한다.<br> 예를 들어서 `student1` 객체는 `Student` 클래스의
인스턴스다. 라고 표현한다.<br>
## 객체 vs 인스턴스<br>
둘다 클래스에서 나온 실체라는 의미에서 비슷하게 사용되지만, 용어상 인스턴스는 객체보다 좀 더 관계에 초점을 맞춘
단어이다.<br> 보통 `student1` 은 `Student` 의 객체이다. 라고 말하는 대신 `student1` 은 `Student` 의 인스턴스이다.
라고 특정 클래스와의 관계를 명확히 할 때 인스턴스라는 용어를 주로 사용한다.<br>
좀 더 쉽게 풀어보자면, 모든 인스턴스는 객체이지만, 우리가 인스턴스라고 부르는 순간은 특정 클래스로부터 그 객체가
생성되었음을 강조하고 싶을 때이다.<br> 예를 들어 `student1` 은 객체이지만, 이 객체가 `Student` 클래스로부터 생성된
다는 점을 명확히 하기 위해 `student1` 을 `Student` 의 인스턴스라고 부른다.<br>
하지만 둘다 클래스에서 나온 실체라는 핵심 의미는 같기 때문에 보통 둘을 구분하지 않고 사용한다.


