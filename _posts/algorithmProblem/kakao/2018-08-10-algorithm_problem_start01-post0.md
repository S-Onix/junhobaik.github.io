---
title: 카카오 코딩테스트 01번 비밀 지도
date: 2018-08-10 00:00:20 +0900
tags:
  - algorithm problem
  - kakao
---


## 보물찾기
---

- 비밀 지도(난이도: 하)
네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.

<br/>

1. 지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 “공백”(“ “) 또는 “벽”(“#”) 두 종류로 이루어져 있다.
2. 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 “지도 1”과 “지도 2”라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
3. “지도 1”과 “지도 2”는 각각 정수 배열로 암호화되어 있다.
4. 암호화된 배열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

### 문제풀이

1. 입력값 설정한다 (맵의 크기, 지도 배열)
2. 두 배열을 비트연산한다 (둘중 하나가 1인 경우 벽이기 때문에 or 연산을 통해 벽을 구한다)
3. 연산된 결과값을 2진수 문자열로 변환한다
4. 변환된 문자열을 문제의 조건에 맞기 "#" or " "으로 변경 후 출력한다.

### 코드

- 입력값을 설정하는 과정에서 2가지 방법을 이용 why? 다른 문제 대비 입력에 익숙해지기 위해서
  1. 키보드를 통한 입력
    - 키보드를 통해 입력한 곳에서는 전부 Exception 처리가 필요했음(까먹기 쉬우니 조심)

  2. 배열에 선언

```

//1번
public static void initMap() throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        System.out.println("맵의 크기를 입력하세요");
        MAPSIZE = Integer.parseInt(br.readLine());
        map1 = new int[MAPSIZE];
        map2 = new int[MAPSIZE];
        System.out.println("지도1의 암호를 입력하세요");
        for(int i = 0; i < map1.length; i++){
            map1[i] = Integer.parseInt(br.readLine());
        }

        System.out.println("지도2의 암호를 입력하세요");
        for(int i = 0; i < map2.length; i++){
            map2[i] = Integer.parseInt(br.readLine());
        }

}

//2번
private static int [] arr1 = {46,33,33,22,31,50};
private static int [] arr2 = {27,56,19,14,14,10};
```

- 두 배열을 비트연산함

```
public static int [] orOperation(int [] array1, int [] array2){
        int [] resultArray = new int [array1.length];

        for(int i = 0; i < resultArray.length; i++){
            resultArray[i] = array1[i]|array2[i];
        }
        return resultArray;
}
```

- 연산된 결과값을 2진수 문자열로 변환
  - 이부분에서 변환함수를 몰랐기 때문에 시간을 낭비함 역시 이래서 사람은 알고봐야함 내가 불편하다고 생각하는 것은 대부분의 사람이 느끼고 그에 따른 기능을 만들어놨을 것.
  - **Integer.toBinaryString(숫자)**
  - 여기서 의문 그렇다면 2진수인 값을 10진수로 어떻게 바꾸는가? Integer.parseInt("2진수문자열", 2); 이렇게 하면 된다고 한다. 뒤의 숫자에 따라 8진수 16진수도 가능함
  - 10진수 -> 2진수 : Integer.toBinaryString(10진수)
  - 10진수 -> 8진수 : Integer.toOctalString(10진수)
  - 10진수 -> 16진수 : Integer.toHexString(10진수)

```
public static String [] convertBinaryString(int [] array){
    String [] resultArray = new String[array.length];

    for(int i = 0; i < resultArray.length; i++){
        resultArray[i] = Integer.toBinaryString(array[i])
                .replace("1", "#")
                .replace("0", " ");
    }

    return resultArray;
}
```

- [전체코드](https://github.com/S-Onix/algorithme_Training/blob/master/src/algorithm_problem/BitOperation/Bit_Operation_01.java)
