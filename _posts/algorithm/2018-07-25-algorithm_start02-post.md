---
title: Recursive Thinking
date: 2018-07-25 00:00:50 +0900
tags:
  - algorithm
---


## 순환적 사고
---
- 수학함수뿐 아니라 다른 많은 문제들을 recursion으로 해결가능
- 일반적으로 for문이나 while문등 반목문들을 recursion을 이용하여 해결가능함

### 문자열 길이의 계산

```
public static int length(String str){
  if(str.equals(""))
    return 0;
  else
    return 1+length(str.substring(1));
}
```

> substring(1) : 첫번째 문자를 제외한 나머지 문자열
> 1. base case : 문자열의 길이가 0이면 0을 리턴함
> 2. "abcd"가 입력값일 경우
> 3. abcd != ""  // 1+length(bcd)
> 4. bcd != ""  // 1+length(cd)
> 5. cd != ""  // 1+length(d)
> 6. d != ""  // 1+length()
> 7. "" == "" // return 0;
> 결과 1+1+1+1 = 4  문자열의 길이 4 출력

### 문자열 출력

```
public static void recursionPrintString(String str){
    if(str.length()==0)
        return;
    else{
        System.out.print(str.charAt(0));
        recursionPrintString(str.substring(1));
    }
}
```

> 1. "abcd" 입력
> 2. a 출력 recursionPrintString("bcd")
> 2. b 출력 recursionPrintString("cd")
> 3. c 출력 recursionPrintString("d")
> 4. d 출력 recursionPrintString("")
> 5. return

### 문자열 역출력

```
public static void recursionReversePrintString(String str){
       if(str.length() == 0){
           return;
       }else{
           recursionReversePrintString(str.substring(1));
           System.out.print(str.charAt(0));
       }
}
```

-스텍에서의 모습
|단계1|단계2|단계3|단계4|단계5|단계6|단계7|단계8|단계9|결과|
|---|---|---|---|---|---|---|---|---|---|
|             |             |             |             |recur("")    |             |             |             |             |return|
|             |             |             |recur("d")   |recur("d")   |recur("d")   |             |             |             |d출력|
|             |             |recur("cd")  |recur("cd")  |recur("cd")  |recur("cd")  |recur("cd")  |             |             |c출력|
|             |recur("bcd") |recur("bcd") |recur("bcd") |recur("bcd") |recur("bcd") |recur("bcd") |recur("bcd") |             |b출력|
|recur("abcd")|recur("abcd")|recur("abcd")|recur("abcd")|recur("abcd")|recur("abcd")|recur("abcd")|recur("abcd")|recur("abcd")|a출력|


### 2진수 출력

```
public static void recursionBinary(int n){
        if(n < 2)
            System.out.print(n);
        else{
            recursionBinary(n/2);   // n을 2로 나눈 몫을 먼저 2진수로 변환하여 인쇄한 후
            System.out.print(n%2);  // n을 2로 나눈 나머지를 줄을 출력
        }
}
```

> 1. 505 입력
> 2. reB(505) reB(252) reB(126) reB(63) reB(31) reB(15) reB(7) reB(3) reB(1)
> 3. 1,1,1,1,1,1,0,0,1 출력


### 배열의 합 구하기

```
public static int recursionArraySum(int [] array, int n){
        if(n<=0)
            return 0;
        else
            return array[n-1]+recursionArraySum(array, n-1);
}
```

> 0번째 배열 값에서 4번째 배열값까지의 합 구하기 // 총 5개 따라서 n = 5
> 1. array[5-1] + recurA(array, 4)  // n = 5
> 2. array[4-1] + recurA(array, 3)  // n = 4
> 3. array[3-1] + recurA(array, 2)  // n = 3
> 4. array[2-1] + recurA(array, 1)  // n = 2
> 5. array[1-1] + recurA(array, 0)  // n = 1
> 6. n == 0 return 0
> 결과 : array[4] + array[3] + array[2] + array[1] + array[0] + 0


### Recursion vs Iteration
- 모든 순환함수는 반복문(iteration)으로 변경 가능
- 그 역도 성립함. 즉 모든 박복문은 recursion으로 표현 해결가능함
- 순환함수는 복잡한 알고리즘을 단순하고 알기쉽게 표현하는 것을 가능하게 함
- 하지만 함수 호출에 따른 오버해드가 발생됨(매개변수 전달, 액티베이션 프레임 생성 등)
- 반복문과 비교해서 실행시간이 더 소요됨.
