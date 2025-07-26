# Java `final` 키워드 요약

## 1. 개념 정리

- `final`은 **변경 불가**의 의미를 가짐
- 변수, 필드, 메서드, 클래스에 모두 사용할 수 있음 (이번에는 변수 중심)
- 한 번 값이 지정되면 변경 불가

---

## 2. final 지역 변수

- 지역 변수에 `final`을 붙이면 **값을 재할당할 수 없음**

```java
final int data = 10;
// data = 20; // ❌ 컴파일 오류
```

- 메서드 매개변수에도 `final` 사용 가능

```java
void print(final int value) {
    // value = 20; // ❌ 불가능
}
```

---

## 3. final 필드 (멤버 변수)

### 3.1 생성자 초기화

- 객체 생성 시 한 번만 값 할당 가능

```java
public class User {
    final int age;

    public User(int age) {
        this.age = age;
    }
}
```

### 3.2 필드에서 직접 초기화

```java
public class FieldInit {
    final int value = 10;
}
```

- 생성자에서 중복 초기화는 불가

---

## 4. static final (상수)

- 여러 객체 간에 **공유**하면서 **변경되지 않는 값**
- 메모리 절약 + 의미 명확

```java
public class Constants {
    public static final int MAX_USERS = 1000;
    public static final double PI = 3.14;
}
```

- 사용 예

```java
if (userCount > Constants.MAX_USERS) {
    System.out.println("대기자로 등록됩니다.");
}
```

---

## 5. 상수 없이 직접 숫자 사용 시 문제

```java
if (userCount > 1000) {
    // 의미 불명확, 중복 수정 필요
}
```

### 상수 사용 시 장점
- 유지보수 용이 (한 곳만 수정)
- 의미 명확 (`MAX_USERS` vs `1000`)
- 매직 넘버 제거

---

## 6. final과 참조형 변수

- 참조형 변수에 `final` 사용 시 **참조값 변경 불가**
- 참조 대상 내부 값은 변경 가능

```java
final Data data = new Data();
data.value = 10; // ✅ 가능
data = new Data(); // ❌ 컴파일 오류
```

---

## 7. final 사용 예시 - 불변 ID 필드

```java
public class Member {
    private final String id;
    private String name;

    public Member(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public void changeName(String name) {
        this.name = name;
    }

    public void print() {
        System.out.println("id: " + id + ", name: " + name);
    }
}
```

```java
public class MemberMain {
    public static void main(String[] args) {
        Member member = new Member("myId", "kim");
        member.print();
        member.changeName("seo");
        member.print();
    }
}
```

**출력 결과**
```
id: myId, name: kim
id: myId, name: seo
```

---

## 8. 요약

| 구분             | 설명                                      |
|------------------|-------------------------------------------|
| `final` 지역 변수 | 한 번만 값 할당 가능                       |
| `final` 필드     | 생성자 또는 필드 초기화 중 택 1            |
| `static final`   | 공유 상수, 메모리 효율 + 의미 명확         |
| 참조형 + `final` | 참조값 변경 불가, 내부 값은 변경 가능      |

- **변하지 않아야 할 값은 `final`로 고정하자!**
