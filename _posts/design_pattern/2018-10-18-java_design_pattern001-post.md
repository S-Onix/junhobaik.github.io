---
title: JAVA Bean Pattern
date: 2018-10-17 00:00:00 +0900
tags:
  - java
  - design pattern
---
## JAVA Bean Pattern
- 자바의 암묵적인? 룰이라고 해야하나 개발자는 클래스 내의 변수를 직접적으로 사용하지 않는다. 그렇다면 이 변수들을 어떻게 사용할 것인가?
- 메소드를 이용해서 변수(데이터)에 접근하고 수정한다.

```java
//이렇게 할 수 도 있다.
public class MyClass{
  int variable1;
  String variable2;

  public static void main(String [] args){
    MyClass mc = new MyClass();
    mc.variable1 = 10;
    mc.variable2 = "문자열";
  }
}

```

- 위의 예제와 같이 사용할 수 있지만 자바의 캡슐화(보안)의 개념을 알게되면 다음과 같이 사용하는 것은 좋지 못하다는 것을 알게 된다.
- 그렇다면 어떻게 접근할 건데?

```java
public class MyClass{
  int variable1;
  String variable2;

  public int getVariable1(){
    return variable1;
  }

  public void setVariable1(int variable1){
    this.variable1 = variable1;
  }

  public String getVariable2(){
    return variable2;
  }

  public void setVariable2(String variable2){
    this.variable2 = variable2;
  }

  public static void main(String [] args){
    MyClass mc = new MyClass();
    mc.setVariable1(10);
    mc.setVariable2("문자열");

    mc.getVariable1();
    mc.getVariable2();
  }
}
```

- 다음과 같이 클래스의 메소드를 이용해서 객체의 변수에 접근하고 수정할 수 있다.
