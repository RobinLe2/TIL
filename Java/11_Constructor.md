# 생성자 (자바 Constructor)

---

##  생성자란?
- 객체를 생성할 때 자동으로 호출되는 특별한 메서드(반환 타입 없음, 클래스명과 이름 동일)
- **객체 초기화**에 사용. 필수값 입력 보장, 실수 방지 가능

---

## 1. 생성자가 필요한 이유

```java
package construct;
public class MemberInit {
    String name;
    int age;
    int grade;
}
```

```java
package construct;
public class MethodInitMain1 {
    public static void main(String[] args) {
        MemberInit member1 = new MemberInit();
        member1.name = "user1";
        member1.age = 15;
        member1.grade = 90;
        MemberInit member2 = new MemberInit();
        member2.name = "user2";
        member2.age = 16;
        member2.grade = 80;
        MemberInit[] members = {member1, member2};
        for (MemberInit s : members) {
            System.out.println("이름:" + s.name + " 나이:" + s.age + " 성적:" + s.grade);
        }
    }
}
```
> 객체 생성 후 매번 필드 값을 일일이 대입해야 하는 **반복/실수** 문제

---

## 2. 메서드 활용 & this 키워드

- **메서드로 초기화 반복 줄이기**

```java
package construct;
public class MemberInit {
    String name;
    int age;
    int grade;
    void initMember(String name, int age, int grade) {
        this.name = name; // this.멤버변수 = 매개변수
        this.age = age;
        this.grade = grade;
    }
}
```

- **this의 의미**  
  - 멤버변수와 매개변수 이름이 같을 때 멤버를 명확히 지정

---

## 3. 생성자 도입

```java
package construct;
public class MemberConstruct {
    String name;
    int age;
    int grade;
    MemberConstruct(String name, int age, int grade) {
        System.out.println("생성자 호출 name=" + name + ",age=" + age + ",grade=" + grade);
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}
```

```java
package construct;
public class ConstructMain1 {
    public static void main(String[] args) {
        MemberConstruct member1 = new MemberConstruct("user1", 15, 90);
        MemberConstruct member2 = new MemberConstruct("user2", 16, 80);
        MemberConstruct[] members = {member1, member2};
        for (MemberConstruct s : members) {
            System.out.println("이름:" + s.name + " 나이:" + s.age + " 성적:" + s.grade);
        }
    }
}
```
- **생성자는 new와 동시에 자동 호출**
- **필수값 누락 방지, 초기화 일관성**

---

## 4. 기본 생성자

- 클래스에 생성자를 직접 하나도 정의하지 않으면  
  **자바가 매개변수 없는 기본 생성자를 자동으로 추가**
- 생성자를 하나라도 정의하면 **직접 기본 생성자를 만들어야 함**

```java
public class MemberInit {
    String name;
    int age;
    int grade;
    // 자동 생성: public MemberInit() { }
}
MemberInit m = new MemberInit(); // 가능
```

---

## 5. 생성자 오버로딩 & this()

- **오버로딩:** 매개변수 종류/개수 다르게 여러 생성자 정의
- **this()**: 생성자 내부에서 다른 생성자 호출(코드 중복 제거)
- **this()는 생성자 첫 줄에만 사용 가능**

```java
package construct;
public class MemberConstruct {
    String name;
    int age;
    int grade;
    MemberConstruct(String name, int age) {
        this(name, age, 50); // 성적 미입력시 50점으로 자동
    }
    MemberConstruct(String name, int age, int grade) {
        System.out.println("생성자 호출 name=" + name + ",age=" + age + ",grade=" + grade);
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}
```

---

## 6. 생성자 호출 실수 방지 & 장점

- 생성자를 강제 호출해야 하므로 필수 입력 실수(누락) 차단
- 객체 생성시 필드 초기화 누락/중복 방지
- **this()**로 코드 중복 제거  
- **기본 생성자 필요시 명시적으로 작성해야 함**

---

## 7. 정리

- 생성자는 **객체를 생성할 때 딱 한 번만 호출**  
- 초기화, 필수값 입력, 일관성, 실수 방지에 최적  
- 오버로딩(여러 형태 제공), this()로 중복 제거  
- 기본 생성자는 직접 만들지 않으면 자바가 자동 생성(단, 직접 생성자 정의시엔 자동생성 X)
- **멤버/매개변수 이름 충돌시엔 this로 명확히 구분!**

---

