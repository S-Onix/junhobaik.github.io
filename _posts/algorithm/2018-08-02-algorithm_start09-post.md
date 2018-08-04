---
title: Merge sort(합병정렬)
date: 2018-08-02 00:00:10 +0900
tags:
  - algorithm
---


## 합병정렬
---

### 분할정복법

- 분할정복법 (Divide and Conquer)
  - 분할 : 해결하고자 하는 문제를 작은 크기의 **동일한** 문제들로 분할
  - 정복 : 각각의 작은 무제를 순환적으로 해결
  - 합병 : 작은 문제의 해를 합하여 원래 문제에 대한 해를 구함

> ex> 최대값을 찾기 위해 반을 나누고 앞쪽과 뒤쪽에서 최대값을 찾은후
> 두 값 중 더 큰 값을 고르는 것
> 분할 : 앞, 뒤 (동일한 믄제)
> 정복 : 큰 값을 찾기 위한 알고리즘
> 합병 : 앞과 뒤에서 가장 큰 값들을 비교 후 최대값 결정

### 합병정렬
- 데이터가 저장된 배열을 절반으로 나눔
- 각각을 순환적으로 정렬
- 정렬된 두 개의 배열을 합쳐 전체를 정렬
- 하나의 추가 배열이 필요함

![sort](https://user-images.githubusercontent.com/33478245/43561257-c5b918ba-9605-11e8-9306-411c7b7a9b0a.PNG)

```
public static void merge(int [] array, int [] temp, int start, int mid, int end){
        for(int a = start; a<=end;a++){
            temp[a] = array[a];
        }
        int i = start;
        int j = mid+1;
        int k = start;

        while(i<=mid && j<=end){
            if(temp[i] <= temp[j]) {
                array[k] = temp[i];
                i++;
            }
            else {
                array[k] = temp[j];
                j++;
            }
            k++;
        }
        //앞 쪽의 데이터가 남아았을 때
        for(int front = 0; front <= mid-i ; front++){
            array[k+front] = temp[i+front];
        }
}
```



### 실행시간

![sor1](https://user-images.githubusercontent.com/33478245/43562010-7ce63402-9609-11e8-8879-4081d7783315.png)


- [전체코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/Sort/Sort_merge.java)
