---
title: 멱집합(powerset)
date: 2018-07-30 00:00:10 +0900
tags:
  - algorithm
---


## 멱집합
---

- 멱집합 : 어떤집합의 모든 부분집합의 집합

- {a,b,c,d,e,f} 의 모든 부분집합을 나열하기 위해서는
  - a를 제외한 {b,c,d,e,f}의 모든 부분집합들을 나열하고
  - {b,c,d,e,f}의 모든 부분집합에 {a}를 추가한 집합들을 나열한다.

- base case : 공집합일 경우
- 집합이 공집합이 아닐경우 한 원소 t에 대해 t를 제외한 모든 부분집합을 구한다
- 왜 멱집합은 2^n개의 구조를 띄는가?

![stt](https://user-images.githubusercontent.com/33478245/43435638-6b6c9fe4-9470-11e8-87ff-36d995f1ad4b.jpg)

- 위의 상태공간트리를 보고 확연히 이해할 수 있었다.
- 자신을 포함하는 경우와 그렇지 않은 경우 그리고 트리의 레벨에 따른 원소의 개수를 확인 할 수 있었다

```
if 부분집합에 원소를 포함할지 여부를 모든 원소에 대해 적용했다면
    부분집합을 출력
    return;
else
    1) 현재 레벨의 원소를 포함하지 않고 다음 레벨로 넘어감
    2) 현재 레벨의 원소를 포함하고 다름 레벨로 넘어감
```

- [소스코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/recursion/RecursionPowerset.java)
