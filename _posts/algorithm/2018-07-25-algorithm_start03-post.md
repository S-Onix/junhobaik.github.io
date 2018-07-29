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

### 최대값 구하기

```
public static int recursionFindMax(int data[], int begin, int end) {
        if (begin == end)
            return data[begin];
        else {
            return Math.max(data[begin], recursionFindMax(data, begin + 1, end));
        }
}
```

- 이해가 되지 않았던점 최대값을 구하는 방식
- 내가 이해한점 결론은 두 숫자 비교를 순환적으로 함으로써 최대값 도출

> 1. 배열 5개 1,3,5,7,8
> 2. Math.max(data[0], re(data,1,4))
> 3. Math.max(data[1], re(data,2,4))
> 4. Math.max(data[2], re(data,3,4))
> 5. Math.max(data[3], re(data,4,4))
> 6. re(data,4,4) == 8
> 7. Math.max(data[3], 8) = 8
> 8. Math.max(data[2], 8) = 8
> 9. data[0] 번째가 될때까지 반복

### 이진탐색

```
public static int recursionBinarySearch(String array[], int begin, int end, String searchData) {
        if(begin>end)
            return -1;
        else{
            int middle = (begin+end)/2;
            int compResult = searchData.compareTo(array[middle]);
            if(compResult == 0)
                return middle;
            else if(compResult < 0)
                return recursionBinarySearch(array, begin, middle-1, searchData);
            else
                return recursionBinarySearch(array, middle+1, end, searchData);

        }
}
```

- 조건 : 데이터가 정렬되어 있어야함
- `compareTo()` 인스턴스를 비교하는 함수 `return type is int` 정수형으로 반환
  - `< 0` : 비교하고자 하는 인스턴스보다 앞에 위치
  - `= 0` : 비교하고자 하는 인스턴스와 동일
  - `> 0` : 비교하고자 하는 인스턴스보다 뒤에 위치
  ```
    String A = "abc";
    String B = "bcd";
    int result = A.compareTo(b);    
  ```

> 1. 중앙값 검사
> 2. 중앙값과 일치여부 확인
> 3. 찾고자하는 값이 중앙값보다 작으면 첫번째위치에서 중앙값-1 위치까지 검색
> 4. 찾고자하는 값이 중앙값보다 크면 중앙값 + 1 위치에서 마지막 위치까지 검색
> 5. 데이터를 찾을때까지 반복 수행
