---
layout: post
title: Bit Operation 관련 알고리즘
excerpt: "기본적인 비트 연산 구현 연습, 2의 제곱수 판별, 두 수의 비트 차이수 구하기"
tags: [Java, Algorithm, Basic]
categories: [Algorithm]
link:
comments: true
pinned: true
image:
  feature:
---

## Today's Algorithm

##### 알고리즘은 20분 안에 모든 방법을 동원해서 못 풀면 바로 답을 보는 형식으로 연습!

### Bit Operation 비트 연산 이론 학습

- 자주 출제 되지 않지만 연습 없이 만나게 되면 풀기가 매우 까다로운 것이 비트연산 문제

![](/img/2018-04-10-02.png)

- 쉬프트 연산자 - <<, >>, >>>
  - 2^n으로 곱하거나 나눈 결과를 반환한다.
  - 곱셈, 나눗셈보다 빠르다.
  - x << n은 x * 2^n과 같다.
  - x >> n은 x / 2^n과 같다.
  - 8 << 2는 8 * 2^2와 같다.
  - 8 >> 2는 8 / 2^2와 같다.



### 1. 기본적인 비트 연산 구현 연습

- get(int n, int i) : n의 i번째 비트 구하기

- set(int n, int i) : n의 i번째 비트 1로 설정

- clear(int n, int i) : n의 i번째 비트 0으로 설정

- 모범 답안

- 이런 문제들은 대부분 마스크를 하나 잘 만들어놓고 and나 or연산을 하면 대부분 풀린다.

- ```java
  public class BitOperator{
      //n의 i번째 요소를 얻어야하니까 i번째 요소만 1인 숫자를 만들고 그 수를 n과 and 연산을 하면 된다.
      public static boolean get(int n, int i){
      	int mask = 1 << i; //1이 있고 i만큼 쉬프트 연산수행.
          return (n&mask) != 0 ; //boolean이므로 비교해줘야한다.
      }
      public static int set(int n, int i){
          int mask = 1 << i; //다0인데 i번째 비트만 1이 된다.
          return n | mask;//or이므로 n의 i번째 비트만 1이 된다.
      }
      public static int clear(int n, int i){
          int mask = ~(1 << i); //다 1인데 i번째 비트만 0이 된다.
          return n & mask; //i번째 비트만 0이고 나머지는 1
          
      }
  }
  ```



### 2. 2의 제곱수 판별

- 2, 4, 8, 16, 32, 64와 같이 2의 제곱으로 이뤄진 수이면 true를 반환하고 아니면 false를 반환한다.

- 2로 계속 나누는 방법 대신 비트 연산을 이용하여 코드를 작성한다.

- 이진수로 바꿨을 때, 1이 하나고 나머지가 0이면 되는데 어떻게 검사할 지를 모르겠다.

- 모범 답안

- 이건 꼭 암기해둘 것!

- ```java
  public class PowerOf2{
      public static boolean isPowerOf2(int i){
          // 2^n 
          // 10 = 2
          // 100 = 4
          // 1000 = 8
          // 10000 = 16
          // 16-1 = 15
          // 10000 - 1 = 01111
          return (i & (i-1)) == 0; //와 이게 뭐냐 도대체. i와 i의 1의 보수를 and 연산하는 것! 만약 이 때 2의 제곱수라면 모두 0이 된다. 따라서 0.
      }
  }
  ```



### 3. 두 수의 비트 차이수 구하기

- 예를 들어 이진수로 1101, 1110 이 두수는 2개 비트가 다르다.

- 비트에서 1의 갯수를 세는 방법을 모르겠는 부분이다.

- ```java
  public class BitDiffCounter {
      public static int count(int a, int b) {
          //카운트 할 인덱스
          int index = 0;
          
          //1에서 a를 뺀 값과 1에서 b를 뺀 값을 xor연산.
          int c = (1-a)^(1-b);
          
          //이제 c에서 1의 갯수를 세면 된다. 근데 이걸 어떻게 세쥬?ㅡ_ㅡ 
          
          return 0;
      }
  }
  ```

- 모범답안

- ```java
  public class BitDiffCounter {
      public static int count(int a, int b) {
  		
          int diff = a^b; // 두 수의 다른 비트 부분만 1인 mask가 생긴다. 이제 diff에서 1의 개수만 세면 된다. 로직은 같군.
          
          int count = 0;
          while(diff != 0){
              //  1001
              // -0111
              //  0001 -> 제일 앞에있는 1이 없어져서 0이 된다.
              diff = diff&(diff-1); // 제일 앞에 있는 비트를 0으로 set한다. 계속 반복하면서 맨 앞자리를 0으로 셋하고 count를 올린다. 어차피 원래 0인 경우는 그 자리수를 건너뛰고 다음 자리 수의 1을 없애는 것. 그리고 결국 마지막 자리까지 0이 되면 반복문이 종료된다.
              count++;
          }
          
          return count;
      }
  }
  ```

