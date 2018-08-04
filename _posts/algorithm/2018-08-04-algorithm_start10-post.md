---
title: Quick Sort(퀵정렬)
date: 2018-08-03 00:00:10 +0900
tags:
  - algorithm
---


## 퀵정렬
---

### 분할정복법

- 분할정복법 (Divide and Conquer)
  - 분할 : 배열을 다음과 같은 조건이 만족되도록 두 부분으로 나눈다
    - elements in lower parts <= elements in upper parts
  - 정복 : 각 부분을 순환적으로 해결
  - 합병 : 안해도 됨

> ex> 최대값을 찾기 위해 반을 나누고 앞쪽과 뒤쪽에서 최대값을 찾은후
> 두 값 중 더 큰 값을 고르는 것
> 분할 : 앞, 뒤 (동일한 믄제)
> 정복 : 큰 값을 찾기 위한 알고리즘
> 합병 : 앞과 뒤에서 가장 큰 값들을 비교 후 최대값 결정

### 퀵정렬
- 기준값(pivot)보다 작은값과 큰 값으로 분활 (반반으로 쪼개진다고 보장할 수 없음)
- 파티션을 나누는 갯수가 N번 -> 한번 검사할 때마다 검사할 데이터의 개수는 N/2
- 복잡도는 **O(nlogn)**

1. pivot 기준값을 잡는다
2. start point와 end point를 위치한다
3. S(start point)는 pivot 값보다 작은값을 무시하면서 간다
4. E(end point)는 pivot 값보다 큰값을 무시하면서 간다

![quick](https://user-images.githubusercontent.com/33478245/43671470-4635f622-978a-11e8-8729-06213483d66e.PNG)

```
private static void quickSort(int[] array, int start, int end){
        //오른쪽 파티션의 첫번째 값
        int rightPartFirstValue = partition(array, start, end);
        //오른쪽방과 왼쪽방의 개수가 이상 차이가 나야 재귀함수 호출
        if(start < rightPartFirstValue-1){
            quickSort(array,start, rightPartFirstValue-1);
        }
        if(rightPartFirstValue < end){
            quickSort(array, rightPartFirstValue, end);
        }
  }
```

> partition 함수를 통해 나뉘어진 파트중 오른쪽 파트의 첫번째 값을 가져옴
> 나뉘어진 파트에서 오른쪽방개수 - 왼쪽방개수 > 1 이여야 재귀함수 호출

```
private static int partition(int [] array, int start, int end){
        int pivot = array[(start+end)/2];
        int temp = 0;
        while(start <= end){
            while(array[start] < pivot) start++;
            while(array[end] > pivot) end--;
            if(start <= end) {
                swap(array,start,end);
                start++;
                end--;
            }
        }
        return start;
}
```

- pivot값을 설정하는 것을 어떻게 할 것인가?
  - 1. 랜덤으로 돌려서? : 여기서 문제 이미 정렬된 pivot의 값을 설정하게 된다면? temp값을 지정하면 되지 않을까? 그렇다면 temp의 범위는 어떻게 설정할 것인가?
  - 2. 특정값을 지정해서

- 처음 생각한것 : 굳이 while문 안의 if문이 필요한 것인가?
- 지금 생각하게 된 것 : 값을 바꾼 이후 위치는 어디에 존재할 것인가?
- 만약 `if`문 내에 `start++, end--`가 없다면 무한루프를 돌고 있을 것이다.
- 따라서 `if`문은 필요하다는 결론을 도출해냄

- [전체코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/Sort/Sort_Quick.java)
