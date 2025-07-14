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
- 학생(`Student`)이라는 타입을 만들면 되지 않을까? 
- 클래스를 사용하면 `int`, `String` 과 같은 타입을 직접 만들 수 있다.
- 사용자가 직접 정의하는 사용자 정의 타입을 만들려면 설계도가 필요하다. 이 **설계도가 바로 클래스**이다.
- 설계도인 클래스를 사용해서 **실제 메모리에 만들어진 실체를 객체 또는 인스턴스**라 한다.
- 클래스를 통해서 사용자가 원하는 종류의 데이터 타입을 마음껏 정의할 수 있다.<br>

**용어: 클래스, 객체, 인스턴스** 
- 클래스는 설계도이고, 이 설계도를 기반으로 실제 메모리에 만들어진 실체를 객체 또는 인스턴스라 한다. 둘다 같은 의
미로 사용된다.
- 여기서는 학생(`Student` ) 클래스를 기반으로 학생1(`student1` ), 학생2(`student2` ) 객체 또는 인스턴스를 만들었다.

  
