---
title: Designing Recursion
date: 2018-07-25 00:01:50 +0900
tags:
  - algorithm
---


## 순환 알고리즘의 설계
---

- 순환적 알고리즘 조건
  - 적어도 하나의 base case, 즉 순환되지 않고 종료되는 case가 존재해야함
  - 모든 case는 결국 base case로 수렴해야 함

- 암시적(implicit) 매개변수를 **명시적(explicit) 매개변수** 로 바꿔라!

### 순차적 탐색(반복문 vs 순환함수)

```
public int search(int [] data, int n, int target){
        for(int i=0; i<n;i++){
            if(data[i] == target)
                return i;
        }
        return -1;
}
```

- 이 함수의 미션은 data[0]에서 data[n-1] 사이에서 target을 검색하는 것이다.
- 하지만 검색 구간은 시작 인데스 0은 보통 생략한다.
- 0은 표시되어 있지 않지만 시작 인덱스는 0부터 시작한다고 암묵적으로 동의한것 <br/>따라서 명시적으로 표현되지 않기때문에 암시적 매개변수라고 한다.

```
public int recursionSearch(int [] data, int begin, int end, int target){
        if(begin>end)
            return -1;
        else if(target == data[begin])
            return begin;
        else
            return recursionSearch(data, begin+1, end, target);
}
```

- 여기서 base case는 `if(begin>end)` 모든 조건 검사한 경우 -1반환
- 첫번째와 두번째 조건이 맞지 않는다면 시작지점을 +1 하고 다시 검색 시작

- 두 알고리즘의 차이는 첫번째는 암시적으로 시작점을 지정했지만 <br/>두번째 알고리즘에서는 명시적으로 시작점과 끝점을 정해놓음
- 자기 자신을 호출할 때의 매개변수까지 생각하고 순환함수를 설계해야함

### 뒤에서부터 순차적 탐색

```
public int recursionSearch(int [] data, int begin, int end, int target){
        if(begin>end)
            return -1;
        else if(target == data[end])
            return end;
        else
            return recursionSearch(data, begin, end-1, target);
}
```

### 다른 버전의 순차 탐색
- 탐색하고자 하는 범위의 중간까지 먼저 탐색
- 중간+1 지점부터 끝까지 탐색

```
public int otherSequenceSearch(int data[], int begin, int end, int target){
        if(begin>end)
            return -1;
        else{
            int middle = (begin+end)/2;
            if(target == data[middle])
                return middle;

            int index = otherSequenceSearch(data, begin, middle-1, target);
            if(index != -1)
                return index;
            else
                return otherSequenceSearch(data,middle+1, end, target);
        }
}
```
