---
title: StackOverflowError
date: 2018-08-04 00:00:10 +0900
tags:
  - Error
---


## StackOverflowError
---

### 발생원인
- 재귀함수 호출에 따른 메모리 부족현상 발생

### 해결방안
- 내가 생각한 것 : IDE의 메모리를 강제적으로 올린다.
- 사용하는 IDE : intelliJ
- `Help` -> `Edit custom VM Options..`

![intellij](https://user-images.githubusercontent.com/33478245/43671944-74270db0-9793-11e8-8a06-9c4ef9660e5e.PNG)


- Xms : 초기 Heap size 설정
- Xmx : 최대 Heap size 설정
- Xss : 각 Thread에 할당되는 Stack size 설정
- Xmn : New 영역을 위한 Heap size 설정

### 실질적인 해결방안
- 내가 작성한 코드의 이상이 있었다.
- 재귀함수에 대한 잘못된 코드작성은 메모리 부족현상 및 무한 루프에 빠짐
- 코드를 작성할때의 꼼꼼함을 다시한번 생각하게 하는 에러였음

### 내가 얻은 것
- IDE의 메모리 설정하는 법
- 코드 재리뷰 및 결국 사용자의 잘못으로 발생되는 애러라는 것
