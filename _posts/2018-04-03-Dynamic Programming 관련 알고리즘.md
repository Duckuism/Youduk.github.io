---
layout: post
title: Dynamic Programming 관련 알고리즘
excerpt: "주어진 값 N에 대해 피보나치 수열의 값을 구하기"
tags: [Java, Algorithm, DP]
categories: [Algorithm]
link:
comments: true
pinned: true
image:
  feature:
---

## Today's Algorithm

##### 알고리즘은 20분 안에 모든 방법을 동원해서 못 풀면 바로 답을 보는 형식으로 연습!

### Dynamic Programming 이론 학습

동적 프로그래밍 문제들은 까다롭고 오래 걸리는 것들이 많다. 코딩테스트 출제 빈도는 낮기 때문에 다른 섹션보다는 우선 순위는 떨어진다. 하지만 출제되면 까다롭기 때문에 시간을 두고 익힐 필요가 있다. 신입 문제에서는 잘 출제되지 않지만, 경력 문제에서는 간간히 나온다.

![](/img/2018-04-02-01.png)

구했던 값들을 저장해놨다가 다시 쓰는 개념이므로, 캐시와 유사하다. 이렇게 생각하면 그렇게 부담스럽지 않게 접근할 수 있다. 만약 하나하나의 메서드가 시간이 오래걸린다고한다면 성능 향상에 아주 좋으므로 알아둬야 할 필요가 있다.



#### 1. 주어진 값 N에 대해 피보나치 수열의 값을 구하기

- 일반 재귀 버전 구현

- 다이나믹 프로그래밍 버전 구현

- 모범 답안

  ```java
  public class Fibonacci{
      public int fibonacci(int n){
  		if(n == 0){
  			return 0;
  		}
  		if(n == 1){
  			return 1;
  		}
  		return fibonacci(n-1)+fibonacci(n-2);        
      }
      public int fibonacciFaster(int n){
          return fibonacciRec(n, new int[n+1]);
      }
      
      private int fibonacciRec(int n, int[] cache){
          if(n==0){
              return 0;
          }
          if(n==1){
              return 1;
          }
          if(cache[n] != 0){
              return cache[n];
          }
          //아하! 빈 배열을 만들고 배열에 계산된 값을 저장하는 것.
          //이 때, n과 index를 똑같이 만듦으로써 n이 무엇이냐에 따라서 cache[n]으로 바로 접근해서 값을 불러오기때문에 memoization과 같은 것!!!!
          //생각보다 쉬운데 이해하기 어려웠다.
          cache[n] = fibonacciRec(n-1, cache) + fibonacciRec(n-2, cache);
          return cache[n]
      }
  }
  ```

  ​

### 