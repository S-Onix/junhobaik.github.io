---
title: Couning cell in a Blob
date: 2018-07-29 00:00:00 +0900
tags:
  - algorithm
---


## Counting Cell in a Blob
---

![blob](https://user-images.githubusercontent.com/33478245/43365201-804510d0-9318-11e8-9bc1-f10ae6cfa0e1.PNG)

- Binary 이미지
- 각 픽셀은 background pixel 이거나 image pixel
- 서로 연결된 pixel의 집합을 Blob이라고 함
- 상하좌우 및 대각방향으로도 연결 된것으로 간주

### 입, 출력
- 입력
  - N*N 크기의 2차원 배열
  - 하나의 좌표(x,y)

- 출력
  - 픽셀(x,y)가 포함된 blob의 크기
  - blob에 속하지 않는 경우 0 반환

### Recursive Thinkning
- 현재 픽셀이 이 속한 blob의 크기를 카운트하기 위해서는?
  - 현재 픽셀이 image color가 아니면 0반환
  - 현재 픽셀이 image color라면
    - 현재 픽셀을 카운트
    - 현재 픽셀이 중복카운트 되는것을 막기 위해 다른 숫자로 지정
    - 현재 픽셀에 이웃한 모든 픽셀들에 대해 그 픽셀이 속한 blob의 크기를 카운트
    - 더이상 이웃한 pixel이 없는 경우 카운터를 반환

![blbo2](https://user-images.githubusercontent.com/33478245/43365221-be05e16a-9318-11e8-9fec-3c94a9421f79.PNG)

### issue
- 생각하지 못한점 : IMAGE_PIXEL이 아닌경우
- 내가 생각했던점 : count 변수를 만들고 해당 위치가 image_pixel일 경우 +1씩 해주기
- 내가 생각했던점의 문제점 : 그렇다면 recursion으로 어떻게 표현할 것인가?

- [소스코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/recursion/RecursionBlob.java)
