---
title: Recursion
date: 2018-07-23 00:00:50 +0900
tags:
  - algorithm
---


## 순환(Recursion)함수
---
- 자기 자신을 호출하는 함수

```
//무한루프에 빠지게 됨
public class Code01{
  public static void main(String [] args){
      func();
  }

  public static void func(){
    System.out.println("Hello");
    func();
  }
}
```

-Recursion은 항상 무한루프에 빠지는것인가?

```
public class Code02{
  public static void main(String [] args){
    int n = 4;
    func(n);
  }
  public static func(int n){
    //Base case
    if(n<=0)
      return 0;
    //Recursion case
    else{
      Systen.out.println{n};
      func(n-1);
    }

  }
}
```

> 1. func(4);
> 2. func(3);
> 3. func(2);
> 4. func(1);
> 5. func(0); retrun 자신을 호출한 메소드로 이동
> output : 4 3 2 1

- Recursion이 적절한 구조를 가지고 있다면 효율적인 사용 가능 (코드량이 줄수 있음)
- Base case : 적어도 하나의 재귀에 빠지지 않는 경우가 존재해야함.
- Recursion case : recursion을 반복하다보면 결국 base로 수렴해야 한다.

```
//1~n까지 더하는 함수
public static int recursionAddOneToN(int n){
    if(n==0)
        return 0;
    else
        return n + recursionAddOneToN(n-1);
}
```

> 1. func(4);
> 2. func(3);
> 3. func(2);
> 4. func(1);
> 5. func(0); retrun 자신을 호출한 메소드로 이동
> output : 4 7 9 10

```
//factorial
public static int recursionFactorial(int n) {
    if (n == 0)
        return 1;
    else
        return n * recursionFactorial(n - 1);
}
```

> 1. func(4) = 4 * func(3);
> 2. func(3) = 3 * func(2);
> 3. func(2) = 2 * func(1);
> 4. func(1) = 1 * func(0);
> 5. func(0) = 1; retrun 자신을 호출한 메소드로 이동
> 역으로 올라가면 1*1*2*3*4 = 24 == 4!

```
//double power(X의 N승 계산)
public static double recursionPow(double x, int n) {
    if (n == 0)
        return 1;
    else
        return x * recursionPow(x, n - 1);
}
```

> 1. func(2, 4) = 2 * func(2, 3);
> 2. func(2, 3) = 2 * func(2, 2);
> 3. func(2, 2) = 2 * func(2, 1);
> 4. func(2, 1) = 2 * func(2, 0);
> 5. func(2, 0) = 1; retrun 자신을 호출한 메소드로 이동
> 역으로 올라가면 1*2*2*2*2 = 16 == 2^4

```
//Fibonacci Number
public static int recursionFibo(int n){
    if (n < 2)
        return n;
    else
        return recursionFibo(n-1)+recursionFibo(n-2);
}
```

> 1. func(2, 4) = 2 * func(2, 3);
> 2. func(2, 3) = 2 * func(2, 2);
> 3. func(2, 2) = 2 * func(2, 1);
> 4. func(2, 1) = 2 * func(2, 0);
> 5. func(2, 0) = 1; retrun 자신을 호출한 메소드로 이동
> 역으로 올라가면 1*2*2*2*2 = 16 == 2^4

```
//최대공약수
public static int recursionEuclid(int num1, int num2){
    if( num2 == 0)
        return num1;
    else return recursionEuclid(num2, num1%num2);
}
```

> 최대 공약수가 이해가 되지 않았음 why? 유클리드 호제법을 몰랐었기 때문에
> 2개의 자연수 a,b 에 대해서 a를 b로 나눈 나머지를  r이라 하면(단, a>b) a와 b의 최대공략수는 b와 r의 최대공략수와 같다.
> ex) 1071, 1029의 최대공략수 구하기
> 1. a = 1071, b = 1029, (a%b)=r=42
> 2. a = 1029, b = 42 (a%b)=r=21
> 3. a= 42, b = 21 r = 0;
> 4. 따라서 최대 공약수는 r 이 0일때의 b값 = 21
