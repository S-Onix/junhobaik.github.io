---
title: Couning cell in a Blob
date: 2018-07-30 00:00:00 +0900
tags:
  - algorithm
---


## N-Queens
---

![nqueens](https://user-images.githubusercontent.com/33478245/43377963-50481a6c-93b3-11e8-8dd0-ffd269a6ff5a.PNG)

- 한 행에 하나의 말을 놓을 수 있게 배치해야함

### 상태공간트리

![stt](https://user-images.githubusercontent.com/33478245/43378087-0f32de08-93b4-11e8-95ed-e24281f0ee13.PNG)

- 즉 해가 존재한다면 그것은 반드시 이 트리의 어떤 한 노드에 해당함 따라서 이 트리를 체계적으로 탐색하면 해를 구할 수 있다.

### Backtracing

![stt2](https://user-images.githubusercontent.com/33478245/43378210-d78cacd0-93b4-11e8-8e8e-4921bbfcea05.PNG)

- Backtracking :  상태공간 트리를 깊이 우선 방식으로 탐색하여 해를 찾는 알고리즘을 말한다.

- 현재 도착한 노드를 알아야한다. (정보제공 필요)
  - 매개변수를 이용
  - 전역변수를 이용

### 제약조건
1. 배치한 노드와 대각선 방향 혹은 같은 선상에 위치할 경우 한단계아래 노드로 되돌아가기
2. 트리의 level과 찾고자하는 Queen의 개수가 같은경우 종료

- 1번에 대한 나의 생각 2차원 배열을 이용하여 좌표값을 넣는 노가다를 생각함
- but, 일차원배열에 저장된 위치를 이용하여 2차원 그래프와 같이 생각할 수 있게 됨

![dxdy](https://user-images.githubusercontent.com/33478245/43379881-36b01ee6-93be-11e8-9a91-5f856b3c50f5.PNG)

```
static boolean promising(int level){
        for(int i = 1; i < level; i++){
          // 같은 선상에 위치한 경우
            if(col[i] == col[level])
                return false;
          // 대각선에 위치한 경우
            else if(level-i == Math.abs(col[level]-col[i])){
                return false;
            }
        }
        return true;
}
```


- 다음 노드 검색 for 문
- level에 해당하는 위치의 숫자를 넣어주고
- 다음 level 검사

```
for(int i = 1 ; i<=N; i++){
            col[level+1] = i;
            if(queens(level+1))
                return true;
}
```

- [전체코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/recursion/RecursionNQueen.java)
