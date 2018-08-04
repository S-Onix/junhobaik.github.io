---
title: 미로찾기 Maze
date: 2018-07-28 00:00:00 +0900
tags:
  - algorithm
---


## 미로 찾기 (feat. reucrsion)
---

![maze](https://user-images.githubusercontent.com/33478245/43364762-f7c77f16-930f-11e8-86db-46c5cf4c64b0.PNG)

- 현재 위치에서 출구까지 가는 경로가 있으려면
  1. 현재 위치가 출구
  2. 이웃한 셀들 중 하나에서 현재 위치를 다시 지나지 않고 출구까지 가는 경로가 있는 경우

### 미로찾기(Decision Problem)
- Yes or No 의 답변으로 하는 문제
- 사람이 동과할 수 있는 장소는 0, 벽은 1, 지나왔지만 출구가 없는 경우 2, 방문여부 3


1. x,y 좌표가 맵내에 있는지 확인
2. 이미 방문한 위치면 false를 반환 // 즉 PATHWAY_COLOR가 아닌경우
3. 출구인 경우
4. 출구는 아니지만 방문하지 않은 셀인 경우

```
//1번 경우
if(x < 0 || y < 0 || x >= N || y >= N)
  return false;
```

```
//2번 경우
else if (maze[x][y] != PATHWAY_COLOR)
  return false;
```

```
//3번 경우
else if(x==N-1 && y==N-1){
  maze[x][y] = PATH_COLOR;
  return true;
}
```

```
4번 경우
else{
  //방문여부 체크
  maze[x][y] = PATH_COLOR;

  //북동남서 방향으로 검색
  if(findMazePath(x-1, y) || findMazePath(x, y+1) || findMazePath(x+1, y)|| findMazePath(x,y-1))
    return true;

  //출구까지 가는 경로가 없을 경우
  maze[x][y] = BLOCKED_COLOR;
  return false;
}
```

### issue
- 처음에 이해 못한점 : x,y 좌표에 대한 이해
- 이제 이해한점 : 북동남서 방향으로 검색하기 때문에 x-1의 위치가 북쪽이라는 것
- 왜 헷갈렸는가? 기존 그래프에서의 x,y좌표와 같이 생각했기 않기때문에

![maze02](https://user-images.githubusercontent.com/33478245/43364763-f7fb647a-930f-11e8-898a-e613d7657153.PNG)

- [전체코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/recursion/RecursionMaze.java)
