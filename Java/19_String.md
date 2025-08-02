#  `String` 클래스 

##  개요
- Java에서 문자열은 `char[]` 기반이지만, 자주 쓰이므로 **`String` 클래스로 편리하게 취급**
- `String`은 **불변(Immutable) 참조형 클래스**로, 내부 값을 직접 바꿀 수 없음

---

##  문자열 생성 방법
- 리터럴 방식: `String str = "hello";`
- 인스턴스 생성 방식: `String str = new String("hello");`
- 리터럴은 **문자열 풀(String pool)** 을 사용해 메모리 효율화  
- `==` 은 참조 비교, `equals()` 는 값 비교에 사용해야 함

---

##  내부 구조
- Java 8 이전: `private final char[] value;`
- Java 9 이후: `private final byte[] value;` (Latin‑1 또는 UTF‑16 인코딩)
- 내부 `char[]` 또는 `byte[]` 은 외부에서 접근 불가 → *캡슐화*

---

##  주요 메서드

| 카테고리 | 메서드 | 설명 |
|---------|--------|------|
| 정보 조회 | `.length()`, `.isEmpty()`, `.isBlank()`, `.charAt(i)` | 문자열 길이, 빈 값, 공백 여부, 특정 인덱스 문자 |
| 비교 | `.equals()`, `.equalsIgnoreCase()`, `.compareTo()`, `.startsWith()`, `.endsWith()` | 문자열 비교 및 순서 확인 |
| 검색 | `.contains()`, `.indexOf()`, `.lastIndexOf()` | 포함 여부, 첫/마지막 등장 위치 |
| 조작 | `.substring()`, `.concat()`, `.replace()`, `.replaceAll()`, `.toLowerCase()`, `.trim()`, `.strip()` | 부분 문자열, 연결, 대/소문자 변환, 공백 제거 등 |
| 변환 | `.split()`, `.join()`, `.valueOf()`, `.toCharArray()`, `.format()`, `.matches()` | 분할·결합, 형식 지정, 정규식 매칭 등 |

---

##  불변 객체 특성 (`Immutable`)
- `concat()` 은 원본을 바꾸지 않고 **새로운 `String` 객체** 반환  
- 예: `str.concat(" world")` 후에도 `str` 은 변하지 않음
- 변경 시마다 새로운 객체 생성 → **문자열 조합이 많다면 성능 저하 가능성**

---



## 왜 StringBuilder인가?

- `String`은 불변(immutable) 객체 → 문자열 변경 시마다 새로운 객체 생성 → 성능 저하
- `StringBuilder`는 가변(mutable) 객체 → 메모리 낭비 없이 문자열 수정 가능
- 문자열을 반복해서 연결하거나 수정해야 하는 상황에서는 `StringBuilder`를 사용해야 성능상 유리

---

##  내부 구조 및 특성

- `StringBuilder`는 `AbstractStringBuilder`를 상속
- 내부 배열:  
  - Java 8 이전: `char[] value`  
  - Java 9 이후: `byte[] value` (Compact String 적용 → Latin-1 또는 UTF-16)
- 내부 배열을 직접 수정하며 final이 아님 → 성능 향상
- 단, **동기화 처리 없음 → 쓰레드 안전하지 않음**

---

## 주요 메서드 정리 및 예제

### ✅ 메서드 요약

| 메서드 | 설명 |
|--------|------|
| `.append(String)` | 문자열 끝에 추가 |
| `.insert(int, String)` | 지정한 위치에 삽입 |
| `.delete(int, int)` | 지정한 범위 삭제 |
| `.reverse()` | 문자열 뒤집기 |
| `.toString()` | `StringBuilder` → `String` 변환 |

###  메서드 체이닝 예제

```java
StringBuilder sb = new StringBuilder();
sb.append("A").append("B").append("C").append("D")
  .insert(4, "Java")
  .delete(4, 8)
  .reverse();
String result = sb.toString();  // 결과: "DCBA"
```

- 각 메서드는 자기 자신을 반환 → 체이닝 가능
- 주의: 원본 객체 자체가 변경됨 (immutable 아님)

---

##  성능 팁

- `"A" + "B"` 와 같이 리터럴 연결은 컴파일 타임에 `"AB"`로 변환됨 → 문제 없음
- `"A" + 변수 + "C"` 처럼 동적일 경우는 `StringBuilder`로 변환됨
- 루프에서 `+=` 사용은 `StringBuilder` 객체를 매번 생성하므로 비효율적
- 많은 문자열을 연결하거나 조작해야 할 때는 직접 `StringBuilder` 사용하는 것이 좋음

---

##  StringBuffer와 비교

| 구분 | StringBuilder | StringBuffer |
|------|---------------|---------------|
| 동기화 | ❌ 비동기 (빠름) | ✅ 동기화 (느림) |
| 쓰레드 안전성 | 낮음 | 높음 |
| 추천 환경 | 단일 쓰레드 | 멀티 쓰레드 |

---

## 6. 실습 문제 풀이

###  `startsWith()`

```java
boolean result = url.startsWith("https://");
```

---

###  `.length()` 문자열 길이 총합 구하기

```java
int sum = 0;
for (String s : arr) {
  System.out.println(s + ":" + s.length());
  sum += s.length();
}
```

---

###  `indexOf()` 확장자 검색

```java
int index = str.indexOf(".txt");
```

---

###  `substring()`으로 분할

```java
String filename = str.substring(0, 5);
String extName = str.substring(5, 9);
```

---

###  `indexOf()` + `substring()` 활용

```java
int idx = str.indexOf(ext);
String filename = str.substring(0, idx);
String extName = str.substring(idx);
```

---

###  `indexOf()` 반복 탐색

```java
int count = 0;
int index = str.indexOf(key);
while (index >= 0) {
  count++;
  index = str.indexOf(key, index + 1);
}
```

---

###  `trim()` 공백 제거

```java
String trimmed = original.trim();
```

---

###  `replace()` 문자열 교체

```java
String result = input.replace("java", "jvm");
```

---

###  `split()` 문자열 분리

```java
String[] parts = email.split("@");
String idPart = parts[0];
String domainPart = parts[1];
```

---

###  `split()` + `join()` 조합

```java
String[] splitFruits = fruits.split(",");
String joined = String.join("->", splitFruits);
```

---

###  `reverse()` 문자열 뒤집기

```java
String reversed = new StringBuilder(str).reverse().toString();
```

---

##  최종 요약

- `StringBuilder`는 문자열 조작 시 반드시 알아야 할 클래스
- 루프나 대량의 문자열 처리 → `StringBuilder` 사용 권장
- `StringBuffer`는 멀티 쓰레드 환경에서 고려
- 문자열을 누적하거나 가공할 때마다 `+`를 쓰는 것이 아니라, `StringBuilder`로 직접 조작하면 훨씬 효율적임


