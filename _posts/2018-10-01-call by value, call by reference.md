---
layout: post
title: call by value, call by reference
excerpt: "call by value의 개념, call by value의 단점, call by value를 개선하는 call by reference"
tags: []
categories: [Algorithm]
link:
comments: true
pinned: true
image:
  feature: algorithms.png
---

### call by value의 개념

* (함수를)부른다 값을 중심으로

A함수에서 B함수를 호출하면서 인자를 넘겨줄 때 scope 때문에 A함수와 B함수의 변수는 서로 공유할 수 없으므로 A함수에서 넘기려는 값 자체를 복사해서 B함수의 인자로 넘기면서 호출하는 것. 

* 장점 : 함수 사이에 서로 관여하지 않는 완벽한 분업을 할 수 있다. 즉, scope의 개념을 지키면서 코딩할 수 있다.
* 단점 : 서로 관여하지 않기 때문에 불편할 때가 많다. 



### call by value가 불편할 때

~~~C++
void swap(int a, int b){
    int temp;
    temp = a;
    a = b;
    b = temp;
}

int main(){
    int a, b;
    
    a=3;
    b=8;
    
    swap(a,b); //함수는 제대로 실행되었지만 swap 함수 scope 안에서 변수가 바뀐다고 해도 main함수 scope 내의 a,b의 변수가 바뀌는 것은 아니다.
    
    printf("%d %d\n", a, b); //3, 8
    
    return 0;
        
}
~~~

그럼 이런 경우를 어떻게 해결할 수 있을까?



### call by value 개선법 (call by reference)

* 포인터를 이용
  * 값을 넘기는 대신, 값을 갖고 있는 변수의 주소를 넘긴다.
  * a, b 변수가 저장되어 있는 메모리의 주소를 넘기면 실제 저장되어 있는 메모리 값에 접근이 가능하므로 scope를 생각하지 않고 값 자체를 바꿀 수 있다.

~~~C++
//int형 값이 아니라 주소를 받는다.
void swap(int* a, int* b){
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

int main(){
    int a, b;
    
    a=3;
    b=8;
    
    swap(&a,&b); //a, b가 가리키고 있는 값의 주소를 넘긴다.
    
    printf("%d %d\n", a, b); //8, 3
    
    return 0;
        
}
~~~

위와 같이 포인터를 사용하면 아래와 같이 함수 하나로 여러 변수를 바꿀 수 있다.

~~~C++
//int형 값이 아니라 주소를 받는다.
void swap(int* a, int* b){
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

int main(){
    int a, b, c;
    
    printf("%d %d %d", &a, &b, &c); //입력받은 값을 a, b, c에 저장
    
    swap(&a,&b);
    swap(&b,&c);    
    
    printf("%d %d %d\n", a, b, c); //입력받은 값의 순서가 b, c, a 순서로 출력된다.
    
    return 0;
        
}
~~~



### 그렇다면 포인터를 이용해서 주소를 넘기는 것은 좋은 것일까?

 * 가능하면 NO 
    * 함수의 철학을 벗어나기 때문에 => 완벽한 분업을 벗어나므로. 즉, scope를 무시하기 시작하면 굉장히 복잡해진다. 가능하면 완벽한 분업이 되게끔 함수를 디자인하는 것이 좋다.
 * BUT, 잘쓰면 YES! 
    * 예제의 swap처럼 함수의 역할이 제대로 정의가 되고, 그 정의를 벗어나지 않는다면 오히려 더 좋은 코드가 될 수 있음



