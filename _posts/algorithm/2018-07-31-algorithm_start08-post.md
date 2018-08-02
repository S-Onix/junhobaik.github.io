---
title: 정렬
date: 2018-07-31 00:00:10 +0900
tags:
  - algorithm
---


## 정렬 알고리즘
---

|알고리즘|성능|
|---|---|
|Bubble sort||
|Insertion sort|간단하게 구현가능하지만 느림|
|Selection sort||
|---|---|
|Quick sort||
|Merge sort|비교적 위의 알고리즘에 비해 빠름|
|Heap sort||
|---|---|
|Radix sort|O(N)|

### 기본적인 정렬 알고리즘

1. 선택 정렬
  - 가장 작은 수를 선택하여 첫 번째과 위치를 바꾼다
  - 실행시간 :
    - 최소값을 찾기위해서는 n-1번 반복
    - 그 다음 작은 수를 찾기 위해서는 n-2번 반복 ....
    - (n-1)+(n-2)+(n-3)+...+2+1 = n(n-1)/2 = O(n^2)

```
public static void SelectionSort(int array[] , int n ){
      int indexMin, temp;

      for (int i = 0; i < n-1; i++) {
        indexMin = i;
        for (int j = i + 1; j < n; j++) {
            if (array[j] < array[indexMin]) {
                indexMin = j;
            }
        }
        temp = array[indexMin];
        array[indexMin] = array[i];
        array[i] = temp;
      }
}
```

2. 버블 벙렬
  - 인접한 두 수를 비교하여 정렬하는 알고리즘
  - 인접한 두 수중 앞의 수가 더 클경우 교환

```
public static void BubbleSort(int array[], int n){
    int temp;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < n-i-1; j++){
            if(array[j] > array[j+1]){
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
            }
        }
    }
}
```

3. 삽입 정렬
  - 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입하는 알고리즘
  - 비교대상보다 클 경우 한칸씩 오른쪽으로 이동

```
public static int[] InsertionSort(int array[], int n){
        int temp;
        int j = 0;
        for(int i = 1; i < n; i++){
            temp = array[i];
            for(j = i-1 ; j>=0 && temp<array[j]; j--){
                array[j+1] = array[j];
            }
            array[j+1] = temp;
        }
        return array;
}
```

- [소스코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/Sort/Sort.java)
