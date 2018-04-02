---
layout: post
title: Recursion 관련 알고리즘
excerpt: "주사위로 이동 가능한 경우의 수 모두 구하기, 이미지에서 닫힌 영역 단색 칠하는 함수 구현하기, n비트의 모든 경우의 수를 출력, 순열 구하기, N개 괄호로 만들 수 있는 모든 조합 출력하기"
categories: [Algorithm]
link:
comments: true
pinned: true
image:
  feature:

---

## Today's Algorithm

### Recursion 기본지식

재귀에 관련해서는 복잡한 문제를 내지는 않는다. 여러 문제들이 재귀만 잘 알면 쉽게 풀 수 있는 경우가 많다. 코드가 굉장히 간단해진다. iterator로 풀기가 가능한 경우도 많다.

피보나치 수열은 기본적으로 알고 있어야 한다.

![](/img/2018-03-31-02.png)

재귀 조건인 경우는 분명히 초기 값과 점화식이 있다. 이렇게 두 가지가 주어지면 거의 기계적으로 짤 수 있어야 한다.

```java
//주어진 초기 값 
f(0) = 0;
f(1) = 1;

//주어진 점화식
f(n) = f(n-1) + f(n-2)

int fiibonacci(int n){
    if(n==0)//초기 조건은 if return으로 기계적으로 코딩한다! 
        return 0;
    if(n==1)//초기 조건은 if return으로 기계적으로 코딩한다! 
        return 1;
    return fibonacci(n-1) + fibonacci(n-2);//그리고 뒤에 점화식을 return문으로 짜준다. 거의 공식과 같이 대부분의 recursion이 이렇게 풀린다.
}
```



#### 1. 주사위로 이동 가능한 경우의 수 모두 구하기

- N칸의 보드게임에서 1~6의 눈금이 있는 주사위를 굴려 갈 수 있는 모든 경우의 수를 반환하는 함수 구현

- 나는 못풀었다. 어떻게 풀어야하는 지 감이 잡히지 않음. 문제 이해와 함께 recursion이 여기서 왜 효과적인지를 이해 못 함. N칸의 보드 게임이 NxN칸이 아니라 일직선 N칸이라는 뜻이었다. 답안을 보고서 이해함.

- 모범답안
  피보나치의 구현과 크게 다르지 않다.

  ```java
  public class Dice{
      public static int countWays(int n){
          if(n<0)//음수가 되는 경우를 방지하기 위해 0으로 처리
              return 0;
          if(n == 0)//1칸의 보드게임에서 주사위를 굴려서 갈 수 있는 경우의 수는 1이 나와야 한다. 만약 n이 1이라면 return countWays(1-1)이 반환 값이 되고 n이 0일 때 반환되는 countWays(0-1)이 최종 결과 값이 된다. 그런데 n이 1일 때는 최종 결과 값이 1이 되어야 하므로 첫 단계인 n이 1일 때 1을 반환하는 것이 아니라 마지막 결과 값을 도출하는 두 번째 단계인 n이 0일 때 1을 반환하도록 해야 한다.
              return 1;
          //점화식부터 쓴다.
          return countWays(n-1) + //주사위를 굴려서 한 칸 가게 되면 n칸의 보드에서 n-1만큼 갈 수 있는 공간이 남는다. 만약 총 6칸의 일직선 보드게임이라면 한 칸을 가면 5칸이 남는 원리. 이러한 과정을 한 칸도 안 남을 때까지 계속 반복한다.
                 countWays(n-2) +
  	           countWays(n-3) +
  			   countWays(n-4) +            
                 countWays(n-5) +
                 countWays(n-6);
      }
  }
  ```

  ​

#### 2. 이미지에서 닫힌 영역 단색 칠하는 함수 구현하기

- 그림판 프로그램의 영역 칠하기 기능을 생각하면 이해에 도움이 될 것이다.
- 매개변수 중 x,y가 색을 칠하기 시작하는 위치이다.
- x,y 위치의 색과 같은 색만 칠한다.
- "newC"는 새로 칠할 색상의 값이다.


- 못 풀었다. 페인트통 모양 기능을 말하는 듯? 같은 색을 칠하는 것! 

- 모범 답안

  ```java
  public class painter{
      public static void paint(int[][] image, int x, int y, int newC){
          //helper 함수
          paintRec(image, x, y, newC, image[y][x]); //행렬 표기법에서는 y축이 먼저 나오는 것이 맞다. 그러나 이런 문제가 나온다면 꼭 면접관이나 조건을 확인해볼 것. 보기 편하게 image[x][y]로 해달라고 할 수도 있다. newC는 새로운 컬러이고, image[y][x]는 우리가 칠 할 곳에 칠해져있는 컬러이다. 모두 같은 색을 동시에 새로운 컬러로 바꿔야 하므로 기존에 어떤 색인지도 매개변수로 넘겨야 한다.
      }
      
      //helper함수의 접근자는 private로.
      private static void paintRec(int[][] image, int x, int y, int newC, int targetC){
          //종료조건 리턴타입이 void이므로 return;이라고만 적어준다.
          //y와 x가 음수이면 안 된다. y가 이미지 y축보다 크면 안된다. x는 행렬에서 두 번째 행의 값(image[y][x])이므로 image[0].length으로 표현.
          if(y<0 || x<0 || y>=image.length || x>=image[0].length){
              return;
          }
          //변경할 색깔과 바꿀 색깔이 같거나, 기존의 색깔이 내가 변경하려던 색깔이 아닐 때.
          if(image[y][x]==newC || image[y][x]!=targetC){
              return;
          }
          
          //기존에 있던 컬러 값을 새로운 컬러 값으로 할당한다.
          image[y][x] = newC;
          paintRec(image, x+1, y, newC, targetC); //오른쪽 오른쪽으로 한 칸 가고 나서 다시 헬퍼 함수를 호출함으로, 종료 조건이 만족할 때까지 오른쪽으로 한 칸씩 계속 이동한다. 그런데 호출된 이 모든 헬퍼 함수들이 위, 왼쪽, 아래에 대한 헬퍼 함수가 있으므로 결국 모든 칸을 커버할 수 있게 된다. 만약 색깔이 이미 바뀌어 있다면 종료하고 다른 방향에 대한 헬퍼함수를 실행하므로.
          paintRec(image, x, y+1, newC, targetC); //위
          paintRec(image, x-1, y, newC, targetC); //왼쪽
          paintRec(image, x, y-1, newC, targetC); //아래
          
      }
  }
  ```

  ​

#### 3. n비트의 모든 경우의 수를 출력

java ArrayList generics 예제

http://arabiannight.tistory.com/entry/%EC%9E%90%EB%B0%94Java-ArrayListT-%EC%A0%9C%EB%84%A4%EB%A6%AD%EC%8A%A4Generics%EB%9E%80



- 못 풀었다. 로직은 어느정도 생각이 났는데, 조건에 관련된 부분을 내가 놓쳐서 못하는 듯.

  ```java
  import java.util.ArrayList; //순서가 있고, 데이터의 중복을 허용.

  public class Exercise {
      public static ArrayList<String> bitCombinations(int n){
          //자리수에 관련한 문제인데, 각 자리당 0과1만 존재하므로 2의 n승이 몇 가지인지 구하는 문제.
          //일단 return type이 ArrayList니까 ArrayList를 만들어야하지 않을까?

          ArrayList<String> arrList = new ArrayList<String>();

          int flag = 0;
  ```

```
      for(String s : arrList){
          //만약 s가 null이면 0과 1을 추가하고,
          //값이 있다면 처음부터 0과 1을 번갈아서 String으로 더하면 될 것같은데!
      }

      //종료조건
      if(n == 1){
          return arrList;
      }
      return bitCombinations(n-1);
  }
```

  }

```
  ​

* 모범 답안

  계속 헬퍼함수를 만든다. 이 부분을 내가 익숙하지 않아서 그런 것 같기도 하다.
  답안을 보니 로직은 비슷했던 것 같은데, 코드를 짜는 능력이 부족했다 ㅠㅠ

  ~~~java
  import java.util.ArrayList;

  public class Exercise{
      public static ArrayList<String> bitCombinations(int n){
          return bitCombRec(n, "", new ArrayList<String>());//대체로 매개변수가 다 넘어가고, List를 만드는 함수는 대체로 String을 누적해 쌓다가 그게 완성이 되면 List에 하나 넣어주는 형식. 빈 문자열인 ""에 0과 1을 누적해서 n비트가 완성이 되면 ArrayList에 넣어줄 것이다. 그리고 마지막에 ArrayList 반환
      }
      
      private static ArrayList<String> bitCombRec(int n, String s, ArrayList<String> list){
          //종료 조건 s가 n비트가 되면 이니까, 길이를 비교하면 된다.
          if(n == s.length()){//s가 n비트가 되었으면
              list.add(s);//list에 n비트 길이의 문자열 s를 추가한다.
              return list;
          }
          //잘 모르겠을 때는 우선 그냥 똑같이 쓰고, 어떻게 바꿀까를 고민하자.
          bitCombRec(n, s+"0", list);
          bitCombRec(n, s+"1", list);
          return list;
      }
  }
```

  ​

http://galgum.tistory.com/18



#### 4. 순열 구하기

- 예제:"123"->["123", "132", "213", "231", "312", "321"]

- 다섯명의 친구가 있을 때, 5!의 경우의 수를 다 구하는 것과 같다.

  ​

- 못 풀었다. recursion 감이 잘 안잡힌다 ㅠㅠ

  ```java
  import java.util.List;
  import java.util.ArrayList;

  public class Permutation {
  	public static List<String> getPermutations(String s) {
  	    //일단 들어온 "123"과 값을 넣을 새로운 ArrayList를 만들어서 넘긴다.
  		return getPermutaionsRec(s, new ArrayList<String>());
  	}
  	
  	//들어온 "123"을 가공하여 6가지의 경우의 수를 ArrayList에 저장 한 후, List로 반환한다.
  	private static void getPermutaionsRec(String s, ArrayList<String> arrayList){
  	    //어떻게 처리할까? recursion이니 반복이 핵심일텐데
  	    
  	    //일단 들어온 String을 배열로 만든다.
  	    char[] strings = s.toCharArray();
  	    
  	    System.out.println(strings);
  	    
  	    //일단 종료 조건은 1x2x3 이 length랑 같아지는 순간
  	   // if(){
  	   //     return arrayList
  	   // }
  	    getPermutationsRec(s, arrayList);
  	    
  	    
  	    return ;
  	}
  }

  ```

  ​

- 모범 답안

  String이 들어오면 이 문자열의 길이가 n이고, 여기서  n!의 경우의 수를 모두 구하는 문제.

  즉, 다섯 명의 친구가 줄을 설 수 있는 모든 경우의 수를 구하는 것과 같다.

  ```java
  import java.util.List;
  import java.util.ArrayList;

  public class Permutation{
      public static List<String> getPermutations(String s){
          if(s==null) //null체크
              return null;
          //boolean은 다섯 명 중 앞에 줄을 선 한 명을 구분하기 위해 만든 것. 1번부터 5번 중에 3번이 빠졌다면 3번만 true 나머지는 false가 되고 나머지 번호를 줄 세우는 것. List에 들어갈 값을 저장하기 위한 빈 문자열도 필요하다. 종료 조건이 되면 List에 넣어야 하므로. 마지막에 반환할 List도 넣어준다.
          return permRec(s, new boolean[s.length()], "", new ArrayList<String>());
      }
      
      //Recursive helper함수
      private static List<String> permRec(String s, boolean[] pick, String perm, ArrayList<String> result){
          //종료 조건
          //perm 문자열이 처음에 매개변수로 들어온 s의 길이와 같아졌을 때.
          //5명의 매개변수가 들어왔는데, 내가 줄 세운 명 수가 5명이 되었을 때.
          if(perm.legnth() == s.length()){
              result.add(perm);//5명을 모두 줄 세웠으므로 반환할 List에 문자열을 추가
              return result;
          }
          //점화식 구현 - 줄 세우는 과정
          for(int i=0; i<s.length(); i++){
              //줄을 서지 않은 사람만 골라서 줄을 세운다.
              //즉, 고르지 않았던 (pick[i]가 false인 애들만 줄을 세운다.)
              if(pick[i])//만약 이미 줄을 세웠다면 무시한다! continue는 반복문의 끝으로 이동하여 다음 반복으로 넘어간다.
                  continue;
              pick[i] = true; //i번째 학생을 줄 세웠다.
              //들어온 문자열 s는 바뀔일 없고, pick은 위에서 바꿔졌고, 반환 값 List는 건드릴 필요가 없으므로 우리가 유일하게 바꿔야 할 것은 perm! s에서 뽑은 i번째의 문자열을 추가한다.
              permRec(s, pick, perm + s.charAt(i), result);
              //해당 문자열을 추가하고 다시 안 뽑은 상태로 바꿔서 초기 상태로 바꾼다.
              pick[i] = false;
          }
          //List를 반환
          return result;
      }
  }
  ```

  ​

#### 3. N개 괄호로 만들 수 있는 모든 조합 출력하기

- 모든 괄호는 올바르게 열리고 닫혀야 함
- 올바른 조합: ()()
- 틀린 조합: )()()


- 이번에는 조금 근접한 것 같긴한데, 어디가 문제인지 찾기가 힘들었다.

  ```java
  import java.util.List;
  import java.util.ArrayList;

  public class Parentheses {
      public static List<String> getPairs(int n) {
  		return getPairsRec(n, new boolean[n], "", new ArrayList<String>());
  	}
  	
  	private static List<String> getPairsRec(int n, boolean[] pick, String pairs, ArrayList<String> arrList){
  	    //종료 조건 : 문자열이 쌓이는 pairs의 길이가 괄호의 개수와 같아졌을 때.
  	    if(pairs.length() == n){
              arrList.add(pairs);
  	        return arrList;
  	    }
  	   
          getPairsRec(n, pick, pairs+"(", arrList);
          getPairsRec(n, pick, pairs+")", arrList);    

  	    return arrList;
  	}
  }
  ```

  ​

- 모범 답안

  여기서 +"(", +")"를 하는 것은 계속 String을 생성하기 때문에 비효율적으로 보일 수 있는데, 이것은 테스트 통과용이므로 이 정도는 무난하다고 생각. 만약 정말 효율적으로 하려면 괄호의 총 개수가 2n개를 넘을 수 없으므로 2n개의 String 배열을 만들고 여기에 값을 채워나가는 형식으로 구현하면 된다.

  ```java
  import java.util.list;
  import java.util.ArrayList;

  public class Parentheses{
      public static List<String> getPairs(int n){
          if(n==0)
              return null;//이럴 때는 면접관한테 물어봐라. null로 반환할지, 비어있는 List로 반환할지.
          return getPairsRec(n, n, "", new ArrayList<String>());//괄호를 연 개수와 닫은 개수를 계산하기 위해 n을 두 개 넣는다. 그리고 문자열을 저장할 String 객체 하나를 넣는다.
      }
      
      private static List<String> getPairsRec(int openedPair, int closedPair, String pairs, ArrayList<String> list){
          //종료조건
          //여는 개수가 더 많으면 닫을 수가 없다.
          if(openedPair > closedPair)
              return list;
          //괄호의 개수가 음수일 수도 없다.
          if(openedPair<0 || closedPair<0)
              return list;
          //정상적으로 다 넘어왔으면 최종적으로 0이 될 것이다.
          if(openedPair==0 && closedPair==0){
              list.add(pairs);
              return list;
          }
          //괄호 열 때, 여는 괄호 개수를 감소시키고 여는 괄호를 pairs에 추가.
          getPairsRec(openedPair-1, closedPair, pairs + "(", list);
          //괄호 닫을 때, 닫는 괄호 개수를 감소시키고 닫는 괄호를 pairs에 추가 
          getPairsRec(openedPair, closedPair-1, pairs + ")", list);        
          return list;
      }
  }
  ```

  ​