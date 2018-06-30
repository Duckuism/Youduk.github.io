---
layout: post
title: Linked List 관련 알고리즘
excerpt: "Single linked list 구현하기, Single linked list에서 중복 데이터 제거하기, Single linked list 역으로 정렬하기,Single linked list에서 뒤에서 K번째 원소를 반환하는 함수 구현하기, Single linked list에서 회문(palindrome)판별하기"
tags: [Java, Algorithm, Linked List]
categories: [Algorithm]
link:
comments: true
pinned: true
image:
  feature:
---

### Linked List 이론 학습

![](/img/2018-04-02-02.png)

제일 첫 번째 원소를 가리키는 head가 필요하고 head의 타입은 node타입이다. 제일 처음에는 null을 가리키고 있다.

![](/img/2018-04-02-03.png)

위 그림은 새로운 원소를 추가했을 때의 그림이다. 
새로운 Node 클래스를 만들어주고, 이 Node클래스는 특정 데이터를 가지고 있고 다음 Node를 가리킬 수 있어야 한다. 원래는 generics으로 만들어도 되지만 예제에서는 간단하게 int 타입으로 만들었다. 다음 노드를 가리킬 수 있게 Node 타입의 next란 변수를 가지고 있다. 빨간색 화살표는 값이 변경되었기 때문이다. `node.next = head;`를 통해 next변수의 값이 head의 값으로 변경되었고, `head = node`를 통해 head의 값이 node의 값으로 변경되었다. 첫 번째 원소를 추가한 경우라서 그런 것이 아닐까? 원소를 하나 더 추가할 때는 다를까?

![](/img/2018-04-02-04.png)

위 그림은 두 번째 새로운 원소를 추가했을 때의 그림이다.

녹색이 새로 추가된 노드고, 빨간 화살표는 값을 바꾸는 것이다. 코드는 동일하다. 

![](/img/2018-04-02-05.png)

위 그림은 Double Linked List의 그림이다.

더블링크드리스트의 경우는 앞, 뒤로 모두 갈 수 있어야 하므로 Node에 prev가 추가되어야 한다.

녹색창의 코드가 5줄인데, 그 이유는 값을 변화시키는 빨간색 화살표가 4줄이기 때문이다. 3줄이라고 착각하지 말 것. 즉 노드를 만드는 1줄과 값을 업데이트시키는 4줄이 있어야 하기 때문에 총 5줄의 코드가 필요한 것이다.



#### Linked List 출제 경향

- Double Linked List는 코딩 문제로 잘 출제되지 않는다. (복잡해서 시간이 오래걸리기 때문에)
- 제한된 짧은 시간에 풀 수 잇는 문제가 출제된다.
- Single linked list로도 검증은 충분하다.
- <u>Double linked list로는 쉽게 풀 수 있지만 Single linked list로는 풀기 까다로운 문제들이 자주 출제 된다.</u>
- 신입들을 위해 쉽게 낸다고하면 Single linked list의 기본 기능(삽입, 삭제)을 구현하는 문제가 출제되기도 하지만, <u>Single linked list가 있다고 가정하고 특정 기능의 함수를 구현하는 문제가 자주 출제 된다.</u>(Single linked list는 구현할 수 있다고 생각하고 여기의 head point가 주어지면 list의 순서를 바꿔보아라, list를 두 세개로 쪼개봐라, 특정 값을 도출해봐라 등)

Linked리스트도 알고 있어야 하지만 작성하는 코드에서 가변 길이의 데이터를 생성하거나 처리할 때 자바에서 제공하는 컬렉션을 잘 알고 있어야 한다.

![](/img/2018-04-02-06.png)

자주 쓰이는 클래스들이고, List인터페이스를 구현하고 있다. 같은 인터페이스를 구현했으므로 기본적인 함수들을 거의 비슷하다. 

#### 1. Single linked list 구현하기

- addToHead(n)

  - 리스트의 head에 노드를 추가
  - node.data는 n으로 설정

- removeFirst()

  - 리스트의 첫 노드 제거
  - 제거할 것이 없으면 RuntimeException을 발생

- 못 풀었다. 어째 20분안에 풀 수 있는게 하나도 없네 ㅡ_ㅡ 
  아.. 나중에 보니까 class가 하나 더 있었다. 영향은 없는 부분이지만 앞으로 잘 확인해야겠다.

  ```java
  import java.lang.RuntimeException;

  public class SingleLinkedList {
      private Node head;
      
      public void addToHead(int n) {
          head = new Node();
          head.data = n;
          return ;
      }
      
      public void removeFirst() {
          if(head != null){
              head = null;
          }
          return ;
      }
      
      @Override
      public String toString() {
          String str = "[ ";
          for(Node n = head; n!=null; n=n.next) {
              str += n.data;
              str += " ";
          }
          str += "]";
          return str;
      }
  }
  ```

- 모범 답안

  ```java
  import java.lang.RuntimeException;

  public class SingleLinkedList {
      private Node head;
      
      public void addToHead(int n) {
  		Node newNode = new Node(); // 새로운 노드 생성
          newNode.data = n //node의 data는 n으로 설정
          newNode.next = head; //node의 next를 현재 head의 값으로 할당(node.next가 기존의 head가 가리키고 있던 맨 마지막 값을 가리킨다.)
          head = newNode; //head의 값을 새로생긴 node의 값으로 할당(head가 새로 생긴 노드를 가리킨다.)
      }
      
      public void removeFirst() {
          if(head == null){ //head가 null이면 아무것도 없는 것.
              throw new RuntimeException("Nothing to remove");
          }
          head = head.next; //하나 밖에 없는 경우도 head가 null이 될테니 괜찮다.
      }
      
      @Override
      public String toString() {
          String str = "[ ";
          for(Node n = head; n!=null; n=n.next) {
              str += n.data;
              str += " ";
          }
          str += "]";
          return str;
      }
  }
  ```



#### 2. Single linked list에서 중복 데이터 제거하기

- HastSet이라는 힌트가 있어서 어떻게 푸는지는 생각을 해봤는데, 코드로 못짜겠다..

- Set을 만들고 여기에 node데이터 값을 모두 넣었다가 빼면서 다시 link하는 방식으로 풀고 싶었다.

- 모범답안

  123,12가 들어있으면 12가 중복이되어서 12를 제거하는 것. 정말 많이 출제된다.

  구현하는 방법은 여러가지가 있다. loop를 두 번 돌면서 중복 데이터를 제거할 수 있지만 비효율적이고 코드가 복잡해진다.

  ```java
  import java.util.HashSet;

  public class MyList {
      private Node head;

      public void addToHead(int n) {
          Node newNode = new Node();
          newNode.data = n;
          newNode.next = head;
          head = newNode;
      }

      @Override
      public String toString() {
          String str = "[ ";
          for(Node n = head; n!=null; n=n.next) {
              str += n.data;
              str += " ";
          }
          str += "]";
          return str;
      }
      
      public void removeDuplicates() {
          HashaSet<Integer> set = new HashSet<Integer>();//node의 data가 Integer이므로

          Node prev = null; //더블링크드리스트는 검색을 해서 중복이면 바로 제거가 가능하지만 싱글링크드리스트는 중간에서 제거하기가 힘들다. 따라서 그 전의 노드에 대해 알고 있어야 한다.
          Node n = head; //시작점을 지정한다.
          
          while(n!=null){
              //중복체크는 우선 set에 데이터를 넣고 data가 다시 나오면 중복인 것. 123을 넣었는데 1이 또 나오면 중복인 원리.
              if(set.contains(n.data)){//set에 현재 노드의 data가 존재한다면
              	prev.next = n.next;//이전 노드의 다음이 현재 노드가 아니라 현재의 다음 노드이므로 현재 노드는 링크가 해제된다.
              }else{//set에 없는 노드라면 
                  set.add(n.data);//set에 넣어준다.
                  prev = n; //다음 loop에서는 현재 노드가 prev가 되어야하므로 현재 노드를 prev에 할당한다.                
              }
              n=n.next;//iteration을 위해 추가
          }
          
          
      }
  }
  ```

  ​

#### 3. Single linked list 뒤집기

- 이번엔 감을 좀 잡은 것 같았는데 아쉽다. hashSet에서 getter를 어떻게 써야하는 지 몰라서 시간 내에 못풀었다.

  ```java
  import java.util.HashSet;

  public class MyList {
      private Node head;
      
      public void reverse() {
          HashSet<Integer> set = new HashSet<Integer>();
          
          Node prev = null; //이전 노드
          Node n = n; //시작점
          
          while(n!=null){
              set.add(n.data);
          }
          
          HashSet<Integer> result = new HashSet<Integer>();
          
          for(int i = set.size(); i>0; i--){
              result.add(set[i]);//여기가 에러 ㅠㅠ 이것만 풀면 해결인데!
          }
      }

      public void addToHead(int n) {
          Node newNode = new Node();
          newNode.data = n;
          newNode.next = head;
          head = newNode;
      }

      @Override
      public String toString() {
          String str = "[ ";
          for(Node n = head; n!=null; n=n.next) {
              str += n.data;
              str += " ";
          }
          str += "]";
          return str;
      }
  }
  ```



- 모범 답안

  원리는 비슷한데.. 역시 훨씬 짧고 간결하다. 그러나 이 답은 비효율적이다. Node를 새로 만들기 때문에. 더 잘 최적화하면 iterator로 한다고 하는 거보니, 내가 처음에 생각한 예제가 맞는듯.

  ```java
  public class MyList {
      private Node head;
      
      public void reverse() {
  		Node oldHead = head; // Node oldHead에 Node head 값을 복사해 놓고,
          head = null; //Node head값을 null로 바꿔서 head를 지워버린다.
          
  		//Node n에 Node oldHead 값을 할당. Node n이 null이 아니라면 반복문 실행. Node n은 현재 Node n이 참조하고있는 다음 Node의 값을 할당(참조 값이므로 얕은 복사.
          for(Node n=oldHead; n!=null; n=n.next){ 
              addToHead(n.data);
          }
      }

      public void addToHead(int n) {
          Node newNode = new Node();//일단 newNode는 int data, Node next를 가지고 있음.
          newNode.data = n;//newNode의 data는 매개변수 n으로 할당
          newNode.next = head;//newNode의 next에는 Node head를 가리키는 주소값 할당
          head = newNode;//Node head를 Node newNode의 값으로 변경
      }

      @Override
      public String toString() {
          String str = "[ ";
          for(Node n = head; n!=null; n=n.next) {
              str += n.data;
              str += " ";
          }
          str += "]";
          return str;
      }
  }
  ```

  ​

!!! Node의 클래스 정의가 int data; Node next;라는 것을 지금 알았다.. next가 자료 값이 아니었구나 ㅠㅠ 즉 next는 다음 노드의 참조 주소를 가지고 있는 pointer이고 직접 자료 값을 가지고 있는 것이 아니다! 이것이 제일 중요. 내가 이해를 못하고 있던 부분이다.



#### 4. Single linked list에서 뒤에서 K번째 원소를 반환하는 함수 구현하기

- 맨 끝 원소는 0번째 원소이다.

- 드디어 한 문제 풀었다 ㅠㅠ 이번에는 시간 생각하지 않고 계속 풀었다. next 변수의 데이터 타입이 Node라는 것을 간과해서 제대로 생각하지 못했던 것이 큰 원인이었다.

  ```java
  public class MyList {
      private Node head;

      public void addToHead(int n) {
          Node newNode = new Node();
          newNode.data = n;
          newNode.next = head;
          head = newNode;
      }

      public void reverse(){
          Node oldHead = head;
          head = null;
          for(Node n=oldHead; n!=null; n=n.next){
              addToHead(n.data);
          }
      }

      public Node kthToLast(int k) { //즉 Node를 반환하니까, k-1번째 Node의 next를 반환하면 되지 않나? index를 쓰려면 헬퍼함수가 필요할 듯.index 변수에 영향을 받지 않으려면 자기 자신을 재귀하면 안된다. 헬퍼함수만 재귀해야 함.
          int idx = 0;
          reverse();
          Node result = new Node();
          for(Node n=head; n!=null; n=n.next){
              if(idx == k-1){
                  result = n.next;
              }
              idx++;
          }
          return result;
      }

  }
  ```

- 모범답안

  k 번째가 0부터 시작하는지 1부터 시작하는지 꼭 물어볼 것.

  ```java
  public class MyList {
      private Node head;

      public void addToHead(int n) {
          Node newNode = new Node();
          newNode.data = n;
          newNode.next = head;
          head = newNode;
      }

      public Node kthToLast(int k) { 
          if(k < 0){ //k가 음수가 들어오면 안된다. null을 반환할지 exception을 반환할지는 면접관한테 물어볼 것.
          	return null;
          }
        	Node n1 = head; //iteration을 도울 포인트
          Node n2 = head; //두 사람이 달리는 데 앞 사람이 10미터 앞에서 출발하면, 앞 사람이 100미터에 다다랐을 때 뒷 사람은 90미터에 다다른 상태이다. 그리고 이 두 사람의 차이가 10미터인데 우리가 얻길 원하는 값이 바로 이 10미터이다. 이런 방식으로 원하는 값을 구하는 방법을 러너기법이라고 한다.
          for(int i=0; i<k; i++){//우선 n2를 k만큼 달리게 한다.
              if(n2 == null){// 뒤에서 15번째를 구하라고 했는데 k가 10개밖에 없다면 반환 값이 없다. 이 부분도 없으면 null을 반환하도록 처리해주어야한다.
                  return null;
              }
              n2 = n2.next;
          }
          while(n2.next != null){//앞의 for문에서 n2는 이미 k만큼 달려서 앞서 있는 상황이다. 이제 n1이 n2와 같은 속도로 달리면 k만큼의 차이를 가지고 계속 달리게 된다. n2가 끝에 도달할 때까지 달린 후, n2와 n1의 차이를 얻으면 된다.
              n1 = n1.next;
              n2 = n2.next;
          }
          return n1;//둘의 차이는 k만큼 return이 되므로 n1을 반환하면 된다.
      }

  }
  ```

#### 5. Single linked list에서 회문(palindrome)판별하기

- 회문이랑 순서를 뒤집어도 내용이 같은 것을 의미한다.
- "noon", "level", "civic"등은 회문이다.
- 본 문제에서는 리스트에 정수가 담겨 있으니, 1->2->3->2->1와 같은 경우 회문으로 판별한다.


- 내 답안. Stack으로 맞게 구현한 것 같은데, 어디서 오류가 나는지 종잡을 수가 없다. 

- ```java
  import java.util.Stack;

  public class MyList {
      private Node head;

      public void addToHead(int n) {
          Node newNode = new Node();
          newNode.data = n;
          newNode.next = head;
          head = newNode;
      }

      public boolean isPalindrome() {
          
          Stack stack = new Stack();
          
          //stack에 모두 추가
          for(Node n=head; n!=null; n=n.next){
              stack.push(n);
          }
          
          //stack에서 꺼내면서 다시 list의 처음부터 비교
          for(Node n=head; n!=null; n=n.next){
              if(n != stack.pop()){
                  return false;
              }
          }        

          return true;
          
          //이 두상태가 같으면 true, 다르면 false
      }
  }
  ```

- 모범답안
  Stack도 써야하고, List도 써야하므로 둘 다 확인이 가능하여 자주 출제된다.
  현재 문제에서는 Node.java의 멤버 변수가 String이 아니라 Integer이므로 숫자로 생각하면 되고, <u>스택에 하나씩 넣었다가 중간부터 빼야하므로 홀수 일 때 중간이 어딘지도 알아야한다.</u>-> 내가 몰랐던 부분이 이부분이네. 중간부터 빼야하나? 왜? 스택은 위에서 부터 빼는거 아닌가..?
  그냥 총체적으로 내가 너무 쉽게 생각하고 있었다. 코드 자체를 다시 봐야 할 듯.

- ```java
  import java.util.Stack;

  public class MyList {
      private Node head;

      public void addToHead(int n) {
          Node newNode = new Node();
          newNode.data = n;
          newNode.next = head;
          head = newNode;
      }

      public boolean isPalindrome() {
          //더블 러너 기법 사용
          Node n1 = head; 
          Node n2 = head;
          
          //Integer를 받는 스택 생성
          Stack<Integer> s = new Stack<Integer>();
          
          //loop를 한 번 돈다. n1은 한 칸씩, n2는 두 칸씩 가므로 차이가 절반이 난다. 따라서 n2가 마지막에 도달았을 때는 n1이 절반만 들어간 상태이다. 그림으로 그려서 설명을 해주면 좀 이해가 될텐데 말로 이해하려니 좀 어렵다. 책을 찾아봐야 할 듯 아하 이해했다. 1:2, 2:4, 3:6, 4:8 이런 식으로 2배씩 커지니까 두 배차이가 나는 것이 맞다! 따라서 n2과 n1의 차이는 절반! 
          while(n2 != null && n2.next != null){
              s.push(n1.data);
              n1 = n1.next;
              n2 = n2.next.next;
          }
          //그리고 홀수일 때는 반복문이 돌아가지 않고 종료되므로 한칸 더 다음 으로 이동시켜야 정확히 중간에 n1이 위치한다.
          if(n2 != null){
              n1 = n1.next;
          }
          
          //이제 스택에 넣은 중간 지점을 제외한 절반의 값을 위에서 부터 하나씩 빼면서 기존의 절반의 값과 처음부터 순서대로 비교하면 된다. 만약 이 값이 틀리면 false 반환이고 while문이므로 다음 값으로 기준점 이동하기 위해 n1을 n1.next로 변경!
          while(n1 != null){
              if(s.pop() != n1.data){
                  return false;
              }else{
                  n1 = n1.next;
              }
          }
          return true;
      }
  }
  ```

### 