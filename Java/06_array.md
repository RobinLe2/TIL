# 배열
### 배열의 필요성
- 타입의 변수를 반복해서 선언하고 반복해서 사용하는 문제를 해결하기 위함
```java
package array;

public class Array1Ref1 {
    public static void main(String[] args) {
        int[] students; // 배열 변수 선언
        students = new int[5];  // int가 5개 있는 그릇을 만드는 것

        //변수 값 대입
        students[0] = 90;
        students[1] = 80;
        students[2] = 70;
        students[3] = 60;
        students[4] = 50;

        // 변수 값 사용
        System.out.println("학생1 점수: " + students[0]);
        System.out.println("학생2 점수: " + students[1]);
        System.out.println("학생3 점수: " + students[2]);
        System.out.println("학생4 점수: " + students[3]);
        System.out.println("학생5 점수: " + students[4]);
    }
}
```
 1. 배열 변수 선언  int[] students;
 2. 배열 생성      students = new int[5]
   new는 새로 생성한다는 뜻, int[5] 는 int형 변수 5개라는 뜻 => int형 변수 5개를 다룰 수 있는 배열 생성
 3. 배열의 초기화는 자동적으로 이루어 짐
 ----
 new int[5]로 배열을 생성하면 배열의 크기만큼 메모리를 확보한다.
 ex) int형 5개 생성 -> 4byte * 5 = 20byte 확보
 ```java
int[] students = new int[5]; // 1. 배열 생성
int[] sutdents = x001;       // 2. new int[5] 의 결과로 x001 참조값 반환
students = x001              // 3. 최종 결과
```
int[] students 변수는 int[5]로 생성한 참조값을 가지고있다.
- 이 변수는 참조값을 가지고 있고 , 이 참조 값을 가지고 배열을 참조 할 수  있다. -> 메모리에 있는 실제 배열에 접근하고 사용
```java
//1. 변수 값 읽기
System.out.println("학생1 점수: " + students[0]);
//2. 변수에 있는 참조값을 통해 실제 배열에 접근. 인덱스를 사용해서 해당 위치의 요소에 접근
System.out.println("학생1 점수: " + x001[0]);
//3. 배열의 값을 읽어옴
System.out.println("학생1 점수: " + 90);
```

배열의 인덱스는 0부터 시작한다. 따라서 사용가능한 인덱스의 범위는 0 ~ (n -1)이 된다.

### 기본형 vs 참조형
자바의 변수 데이터 타입을 가장 크게 보면 기본형과 참조형으로 분류할 수 있다. 사용하는 값을 직접 넣을 수 있는 기본형,
그리고 방금 본 배열 변수와 같이 메모리의 참조값을 넣을 수 있는 참조형으로 분류할 수 있다. <br>
- 기본형(Primitive Type): 우리가 지금까지 봤던 `int` , `long` , `double` , `boolean` 처럼 변수에 사용할 값을
직접 넣을 수 있는 데이터 타입을 기본형(Primitive Type)이라 한다. <br>
- 참조형(Reference Type):`int[] students` 와 같이 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터
타입을 참조형(Reference Type)이라 한다. 뒤에서 학습하는 객체나 클래스를 담을 수 있는 변수들도 모두 참조
형이다. 배열, 객체

배열은 왜 참조형을 사용할까?
: 기본형은 모두 사이즈가 명확하게 정해져있다. <br>
   하지만 배열은 사이즈를 동적으로 변경할 수 있으므로 유연성을 제공할 수 있다. <br>
: 기본형은 사용할 값을 직접 저장한다. <br>
  -> 더 빠르고 메모리를 효율적으로 처리한다. <br>
  참조형은 메모리에 저장된 배열이나 객체의 참조를 저장한다. <br>
  -> 더 복잡한 메모리 구조를 만들고 관리할 수 있다.

### 배열 리펙토리 - 변수 값 사용
```java
package array;

public class Array1Ref2 {

    public static void main(String[] args) {
        int[] students; // 배열 변수 선언
        students = new int[5];  // int가 5개 있는 그릇을 만드는 것
        // int[] students = new int[]{ 90,80,70,60,50};   // 배열의 편리한 초기화
        // int[] students = {90,80,70,60,50};             // 배열의 편리한 초기화

        //변수 값 대입
        students[0] = 90;
        students[1] = 80;
        students[2] = 70;
        students[3] = 60;
        students[4] = 50;

        // 변수 값 사용
        for (int i = 0; i < students.length ; i++) {
            System.out.println("학생" + (i + 1) + " 점수: " + students[i]);
        }
    }
}
```

### 2차원 배열

2차원 배열은 행과 열로 구성한다.
arr[row][column] , arr[행][열]

```java
package array;
public class ArrayDi0 {
    public static void main(String[] args) {
// 2x3 2차원 배열을 만든다.
        int[][] arr = new int[2][3]; //행(row), 열(column)
        arr[0][0] = 1; //0행, 0열
        arr[0][1] = 2; //0행, 1열
        arr[0][2] = 3; //0행, 2열
        arr[1][0] = 4; //1행, 0열
        arr[1][1] = 5; //1행, 1열
        arr[1][2] = 6; //1행, 2열
//0행 출력
        System.out.print(arr[0][0] + " "); //0열 출력
        System.out.print(arr[0][1] + " "); //1열 출력
        System.out.print(arr[0][2] + " "); //2열 출력
        System.out.println(); //한 행이 끝나면 라인을 변경한다.
//1행 출력
        System.out.print(arr[1][0] + " "); //0열 출력
        System.out.print(arr[1][1] + " "); //1열 출력
        System.out.print(arr[1][2] + " "); //2열 출력
        System.out.println(); //한 행이 끝나면 라인을 변경한다.
    }
}
```
**실행 결과** 

```
1 2 3 //[0][0], [0][1], [0][2]
4 5 6 //[1][0], [1][1], [1][2]
```

```java
for 문 사용
package array;
public class ArrayDi1 {
    public static void main(String[] args) {
// 2x3 2차원 배열을 만든다.
        int[][] arr = new int[2][3]; //행(row), 열(column)
        arr[0][0] = 1; //0행, 0열
        arr[0][1] = 2; //0행, 1열
        arr[0][2] = 3; //0행, 2열
        arr[1][0] = 4; //1행, 0열
        arr[1][1] = 5; //1행, 1열
        arr[1][2] = 6; //1행, 2열

        for (int row = 0; row <2 ; row++ ){
            for(int col = 0; col < 3 ; col++) {
                System.out.print(arr[row][col] + " "); 
            }
            System.out.println(); //한 행이 끝나면 라인을 변경한다.
        }
    }
}
```
**실행 결과** 

```
1 2 3 //[0][0], [0][1], [0][2]
4 5 6 //[1][0], [1][1], [1][2]
```

### 2차원 배열의 초기화와 배열의 길이
```java
package array;
public class ArrayDi2 {
    public static void main(String[] args) {
// 2x3 2차원 배열을 만든다.
        int[][] arr = {
                {1,2,3},
                {4,5,6}
        }; //행2, 열3

        for (int row = 0; row < arr.length ; row++ ){
            for(int col = 0; col <arr[row].length ; col++) {
                System.out.print(arr[row][col] + " ");
            }
            System.out.println(); //한 행이 끝나면 라인을 변경한다.
        }
    }
}
```
### 중첩 for문을 이용한 구조 개선
```java
package array;
public class ArrayDi3 {
    public static void main(String[] args) {
// 2x3 2차원 배열을 만든다.
        int[][] arr = new int[3][3]; //행2, 열3

        int i = 1;
        for (int row=0; row<arr.length; row++){
            for (int col=0; col < arr[row].length ; col++){
                arr[row][col] = i++;
            }
        }

        for (int row = 0; row < arr.length ; row++ ){
            for(int col = 0; col <arr[row].length ; col++) {
                System.out.print(arr[row][col] + " ");
            }
            System.out.println(); //한 행이 끝나면 라인을 변경한다.
        }
    }
}
```
### 향상 for문
***향상된 for문 정의***
```java
int[] numbers = {1,2,3,4,5};

//항샹된  for문, for-each문
  for(int number : numbers){
  System.out.println(number);
  }

//for-each문을 사용할 수 없는 경우, 증가하는 index 값 필요
for(int i = 0; i < numbers.length; ++i) {
System.out.println("number" + i + "번의 결과는: " + numbers[i]);


```
단축키 iter 사용 
