# 상속(Inheritance) 정리


## 1. 상속이란?
public class Child extends Parent와 같이, 한 클래스가 다른 클래스(부모)를 확장하여 상속받는 것.

부모 클래스의 public 및 protected로 선언된 변수와 메소드를 자식 클래스가 마치 자신의 것처럼 사용할 수 있음.

extends 클래스명이 해당 클래스를 상속받는다는 의미.

```
public class Parent {
    public Parent() {
        System.out.println("Parent constructor");
    }
    public void printName() {
        System.out.println("Parent printName()");
    }
}
public class Child extends Parent {
    public Child() {
        System.out.println("Child constructor");
    }
}
public class InheritancePrint {
    public static void main(String[] args) {
        Child child = new Child();
        child.printName();
    }
}
```

실행 결과
```
Parent constructor
Child constructor
Parent printName()
```
자식 클래스의 생성자를 호출하면, 부모 클래스의 생성자가 먼저 실행된다.

부모 클래스에만 있는 printName() 메소드도 자식 클래스에서 사용할 수 있다.

부모 클래스에서는 별도의 준비 없이, 기본 생성자만 있으면 상속 가능하다.

이미 잘 만들어진 클래스를 상속하여 추가 기능을 확장할 수 있다.

## 2. super()
부모 클래스에 매개변수가 있는 생성자가 있으면, 자식 클래스에서 super()를 명시적으로 호출해야 함.

super()는 부모 클래스의 생성자를 호출함을 의미한다.

super.메소드명()을 사용하면 부모 클래스의 메소드를 호출할 수 있다.

자식 클래스 생성자에서 super()를 명시하지 않으면, 컴파일러가 자동으로 추가한다.

단, super()는 반드시 자식 클래스 생성자의 첫 줄에 위치해야 한다.

## 3. 메소드 오버라이딩(Overriding)
자식 클래스에서 부모 클래스의 메소드와 **시그니처(이름, 리턴타입, 매개변수 타입/개수)**가 완전히 동일하게 선언하는 것.

오버라이딩된 메소드는 부모 클래스와 동일한 리턴 타입을 가져야 한다.

오버라이딩된 메소드의 접근제어자는 부모보다 더 넓은 범위만 허용된다. (좁히면 컴파일 에러 발생)

오버라이딩된 메소드가 있을 경우, 자식 클래스의 메소드가 실행된다.

## 4. 참조 자료형의 형 변환
상속 관계라면, 부모 타입 변수로 자식 객체를 참조할 수 있다.

```
ParentCasting obj = new ChildCasting(); // 가능
```
반대로, 자식 타입 변수로 부모 객체를 참조할 수는 없다.

```
ChildCasting obj2 = new ParentCasting(); // 불가
```
자식 클래스에서는 부모 클래스의 변수와 메소드를 모두 사용할 수 있지만,
부모 클래스는 자식 클래스의 고유한 변수/메소드를 사용할 수 없다.

만약 부모 타입 변수에 실제로 자식 객체가 할당되어 있다면,
명시적 형 변환을 통해 자식 타입으로 사용할 수 있다.

```
ParentCasting parent2 = child;
ChildCasting child2 = (ChildCasting) parent2; // 가능
```
## 5. instanceof 예약어
객체가 어떤 타입인지 확인하는 데 사용하는 예약어.

예시:
```
if (obj instanceof ChildCasting) { ... }
```
객체의 타입을 확인한 후, 명시적으로 형 변환해서 자식 클래스의 메소드도 호출할 수 있다.

주의:
상속 구조에서 instanceof Parent는 자식 객체에도 true이므로,
가장 하위 타입부터 체크하는 것이 올바른 방식이다.

```
public class InheritanceCasting {
    public static void main(String args[]) {
        InheritanceCasting inheritance = new InheritanceCasting();
        inheritance.objectCastArray();
    }
    public void objectCastArray() {
        ParentCasting[] parentArray = new ParentCasting[3];
        parentArray[0] = new ChildCasting();
        parentArray[1] = new ParentCasting();
        parentArray[2] = new ChildCasting();
        objectTypeCheck(parentArray);
    }
    private void objectTypeCheck(ParentCasting[] parentArray) {
        for(ParentCasting tempParent: parentArray) {
            if(tempParent instanceof ChildCasting) {
                System.out.println("ChildCasting");
                ChildCasting tempChild = (ChildCasting)tempParent;
                tempChild.printAge();
            } else if(tempParent instanceof ParentCasting) {
                System.out.println("ParentCasting");
            }
        }
    }
}
```
실행 결과

```
ChildCasting
printAge() - 18 month
ParentCasting
ChildCasting
printAge() - 18 month
```
