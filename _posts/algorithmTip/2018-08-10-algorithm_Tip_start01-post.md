---
title: 대량의 데이터를 입력할 때 무엇을 사용하는 것이 좋은가?
date: 2018-08-10 00:00:10 +0900
tags:
  - algorithm Tip
---


## 입력방법
---

- 자바를 처음 배우는 사람들은 대부분 `Scanner` 클래스를 이용하여 입력합니다. 그런데 알고리즘 문제를 풀며 공부하는 가운데 `Scanner`를 이용한 입력은 실행시간이 오래걸린다는 사실을 알게 되었고 다른 방법을 소개하고자 합니다.

### Scanner

```
#import java.util.Scanner;

public class scannerEx{
  public static void main(String [] args){
    Scanner scan = new Scanner(System.in);
    int inputNum = scan.nextInt();
  }
}
```

- 대부분의 자바 개발자들은 코드를 작성하는데 있어서 편하고 쉽기 때문에 `Scanner`를 사용합니다. 그러나 간편하게 쓰는 것과 달리 컴퓨터에서는 중간 과정들의 처리가 많기 떄문에 실제 실행속도는 느리게 됩니다. 간단한 테스트코드를 통해서도 알 수 있습니다.

```
public static void main(String [] args){
  Scanner scan = new Scanner(System.in);
  int var;
  long runTimeCheck = System.currentTimeMillis();

  for(int i = 0 ; i < 100000; i++){
    var = scan.nextInt();
  }

  System.out.println(System.currentTimeMillis() - runTimeCheck);  
}
```

- **2441ms** 가 소요되었습니다. 대략 하나의 입력에 소요되는 시간은 0.024ms입니다. 입력에만 소요되는 시간이기 떄문에 실제로 프로그래밍할 떄에는 더 많은 시간이 걸리겠죠? 그렇다면 이제 소개해드릴 `BufferedReader`는 어떻게 다를까요?

### BufferedReader
- `Scanner`에 비해 사용방법은 어려울 수 있습니다. 그러나 속도적인 측면에서 보자면 그런 어려움은 감수할 수 있습니다.

```
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class BufferedReaderEx{
  public static void main(String [] args) throws Exception{
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    String s = br.readLine();
    int s = br.read();
    int b = Integer.parseInt(br.readLine());

  }

}
```

- 앞서 `Scanner`와 다르게 추가된 사항들이 많습니다. `InputStreamReader`라든지 main 함수에서의 예외처리라든지 이러한 사항들은 익히지 않는다면 쉽게 잊어먹기 마련입니다. 그렇기 때문에 BufferedReader를 이용한 입력은 충분한 연습이 필요합니다. 그렇다면 이제 실행시간에 대해 알아보도록 해보겠습니다.

```
public static void main(String [] args) throws Exception{
  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

  long runTimeCheck = System.currentTimeMillis();
  int var;

  for(int i = 0; i < 100000; i++){
    var = Integer.parseInt(br.readLine());
  }

  System.out.println(System.currentTimeMillis() - runTimeCheck);
}

```

- 실행시간은 놀랍게도 **452ms** 가 소요됬습니다. 1억개의 데이터를 입력했을경우 `Scanner`의 경우에는 2441000ms `BufferedReader`의 경우 452000ms가 소요되는 것을 알 수있습니다. 대략 6배정도의 차이입니다. 물론 프로그램의 용도에 따라 실행시간이 달라질 수는 있습니다. 그리고 목적에 따라 Scanner를 사용할 수도 있습니다. 대량의 데이터 입력을 하는 경우에는 BufferedReader를 사용하는 것이 유리하다는 결론을 내릴 수 있었습니다.


### 결론
- 대량의 데이터 입력에는 BufferedReader가 유리하다
- BufferedReader하는 법을 연습하자
- 컴퓨터에게 더 효율적인 방법을 찾는 프로그래머가 되자
