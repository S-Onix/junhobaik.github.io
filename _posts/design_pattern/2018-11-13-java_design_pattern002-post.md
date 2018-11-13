---
title: JAVA Singleton pattern
date: 2018-11-13 00:00:00 +0900
tags:
  - java
  - design pattern
---
## JAVA Singleton Pattern
- 자바 프로그램이 실행되는데 있어서 반드시 하나의 객체만 존재해야할 경우가 있다.
- 예를 들면 DB의 객체인데 만약 DB에 관련된 객체가 여러개라면 개발자가 모르는 사이 데이터의 조작이 이루어지고 있을 가능성이 농후하다.
- 하나의 인스턴스만을 사용하기 위한 패턴이다.
- 하나의 인스턴스만 생성하게 하기 위해서는 생성자에 접근 제한을 줘야하지 않을까?
  - 그렇지 않다면 new 연산을 통해 생성자를 계속 호출할 수 있을 것 같다(내 생각임)

```java
class SingletonEx{
  private SingletonEx{

  }
}
```

- 그렇다면 객체는 어디에서 생성하는것이 좋을까?
- 보통 싱글톤패턴을 쓰는 클래스들은 getInstance()라는 메소드를 통해 객체를 호출한다.

```java
class SingletonEx{
  SingletonEx singleton;
  private SingletonEx{

  }
  public static SingletonEx getInstance(){
    singleton = new SingletonEx();
    return singleton;
  }
}
```

- 하지만 하나의 객체만을 생성해야하기 때문에 조건을 걸어준다. (해당 객체가 존재하지 않을 경우에만)

```java
class SingletonEx{
  SingletonEx singleton;
  private SingletonEx{

  }
  public static SingletonEx getInstance(){
    if(singleton == null) {
      singleton = new SingletonEx();
    }
    return singleton;
  }
}
```

- 싱글톤패턴을 이용하여 기본적인 예제를 하나 만들어봤다. 그렇다면 사용은 어떻게 하는 것인가?

```java
class Main{
  public static void main(String [] args){
    SingletonEx se = SingletonEx.getInstance();
  }
}
```

- 참조변수만을 이용하여 앞서 생성된? 아니면 생성한 객체를 사용하면 된다.
