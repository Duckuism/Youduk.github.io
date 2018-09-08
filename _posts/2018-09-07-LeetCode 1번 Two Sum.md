---
layout: post
title: Leet code 1번 Two Sum
excerpt: "Brute Force, Two-pass Hash Table, One-pass Hash Table"
tags: [Brute force]
categories: [Algorithm]
link:
comments: true
pinned: true
image:
  feature: algorithms.png

---



최근 취업준비를 하면서 모 스타트업 테스트를 위해 LeetCode라는 사이트를 이용해보는 중인데, 기존에 사용하던 백준과 달리 Java로 모범답안이 나와있어서 정말 좋다. 문제를 풀어보고 모범 답안을 번역해서 올려보겠다.

### 문제

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

주어진 정수들의 배열은 특정 타겟 값이 될때까지 더한 두 숫자의 인덱스들을 반환합니다.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

각 출력당 하나의 정답만 있다고 가정하고, 같은 숫자는 중복되어 쓰이지 않습니다.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### 나의 답안 (Java, JavaScript ES6)

~~~java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for(int i = 0; i<nums.length; i++){
            for(int j = i+1; j<nums.length; j++){
                if(nums[i]+nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                }
            }
        }
        return result;
    }
}
~~~

~~~javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
const twoSum = (nums, target)=>{
    for(let i = 0; i<nums.length; i++){
        for(let j = i+1; j<nums.length; j++){
            if((nums[i]+nums[j]) == target){
                return [i,j];
            }
        }
    }
};
~~~

### Leet Code 모범 답안 해석

1. Brute Force (완전 탐색)

   The brute force approach is simple. Loop through each element $x$ and find if there is another value that equals to $$target - x$$.

   완전 탐색 접근은 간단합니다. 각 요소 $$x$$에 대해 loop를 돌고 $$target-x$$와 같은 값이 있는지를 찾습니다.

   ~~~java
   public int[] twoSum(int[] nums, int target) {
       for (int i = 0; i < nums.length; i++) {
           for (int j = i + 1; j < nums.length; j++) {
               if (nums[j] == target - nums[i]) {
                   return new int[] { i, j };
               }
           }
       }
       throw new IllegalArgumentException("No two sum solution");
   }
   ~~~

   **Complexity Analysis** (복잡도 분석)

   - Time complexity : $$O(n^2)$$. For each element, we try to find its complement by looping through the rest of array which takes $$O(n)$$ time. Therefore, the time complexity is $$O(n^2)$$.

     시간 복잡도 : $$O(n^2)$$. 우리는 각각의 요소에 대해 $$O(n)$$ 시간을 소요하여 해당 요소를 제외한 배열의 나머지 전체를 탐색함으로써 보완 요소를 찾으려고 시도한다. 따라서 시간 복잡도는 $$O(n^2)$$ 이다.

   - Space complexity : $$O(1)$$. 

2. Two-pass Hash Table (두 번의 해시 테이블 사용)

   To improve our run time complexity, we need a more efficient way to check if the complement exists in the array. If the complement exists, we need to look up its index. What is the best way to maintain a mapping of each element in the array to its index? A hash table.

   우리의 런타임 시간 복잡도를 개선하기 위해 우리는 보완 요소가 배열안에 존재하는지를 체크하는 좀 더 효율적인 방법을 찾을 필요가 있다. 만일 보완 요소가 존재한다면 우리는 그것의 인덱스를 찾을 필요가 있다. 배열 안의 각 요소들과 해당 요소 인덱스와의 연결 관계를 유지하는 가장 좋은 방법은 무엇일까? 해쉬테이블이다.

   We reduce the look up time from $$O(n)$$ to $$O(1)$$ by trading space for speed. A hash table is built exactly for this purpose, it supports fast look up in *near* constant time. I say "near" because if a collision occurred, a look up could degenerate to $$O(n)$$ time. But look up in hash table should be amortized $$O(1)$$ time as long as the hash function was chosen carefully.

   우리는 빠른 공간 교환에 의해서 찾는 시간을 $$O(n)$$에서 $$O(1)$$까지 감소시킬 수 있다. 하나의 해쉬 테이블은 정확히 이 목적을 위해 만들어지며, 이 해쉬 테이블은 *거의* ​ 일정한빠른 탐색속도를 지원한다. *거의* 라고 말을 하는 이유는 한 번 충돌이 일어나면 탐색 속도는 $$O(n)$$ 까지 악화될 수 있기 때문이다. 그러나 해쉬 테이블에서의 탐색은 해쉬 함수가 주의깊게 선택되는 한은 $$O(1)$$로 분할 상황 된다.

   A simple implementation uses two iterations. In the first iteration, we add each element's value and its index to the table. Then, in the second iteration we check if each element's complement ($$target - nums[i]$$) exists in the table. Beware that the complement must not be $$nums[i]$$ itself!

   간단한 코드 실행은 두 번의 반복 횟수를 사용한다. 첫 번째 반복에서 우리는 각 요소의 값과 인덱스를 해쉬 테이블에 추가한다. 그리고 두 번째 박복에서 우리는 각 요소의 보완 요소인 $$target - nums[i]$$의 값이 테이블안에 존재하는지를 체크한다. $$nums[i]$$ 자기 자신은 보완 요소가 될 수 없다는 것을 잊어먹지 말아라!

   ~~~java
   public int[] twoSum(int[] nums, int target) {
       Map<Integer, Integer> map = new HashMap<>();
       for (int i = 0; i < nums.length; i++) {
           map.put(nums[i], i);
       }
       for (int i = 0; i < nums.length; i++) {
           int complement = target - nums[i];
           if (map.containsKey(complement) && map.get(complement) != i) {
               return new int[] { i, map.get(complement) };
           }
       }
       throw new IllegalArgumentException("No two sum solution");
   }
   ~~~

   **Complexity Analysis:**

   - Time complexity : $$O(n)$$. We traverse the list containing $$n$$ elements exactly twice. Since the hash table reduces the look up time to $$O(1)$$, the time complexity is $$O(n)$$.

     시간 복잡도 : $$O(n)$$. 우리는 $$n$$개의 요소들을 포함하는 리스트를 정확히 두 번 가로지른다. 해쉬테이블은 탐색시간을 $$O(1)$$로 감소시키므로 시간복잡도는 $$O(n)$$.

   - Space complexity : $$O(n)$$. The extra space required depends on the number of items stored in the hash table, which stores exactly $$n$$ elements. 

     공간 복잡도 : $$O(n)$$. 해쉬테이블 안에 $$n$$개의 요소들을 저장하기 위해 필요한 아이템들(key 값은 각 요소의 값, value값은 각 요소의 index 값)의 개수만큼 추가 공간이 요구된다.

3. One-pass Hash Table (한 번의 해쉬테이블 사용)

   It turns out we can do it in one-pass. While we iterate and inserting elements into the table, we also look back to check if current element's complement already exists in the table. If it exists, we have found a solution and return immediately.

   우리가 위 과정을 한 번에 할 수 있다는 것은 명백하다. 우리는 반복하면서 해쉬테이블에 요소들을 삽입하는 동시에 현재 요소들의 보완 요소들이 테이블 안에 이미 존재하는지를 다시 체크해볼 수 있다. 만일 존재한다면 우리는 답을 찾고 즉시 반환한다.

   ~~~java
   public int[] twoSum(int[] nums, int target) {
       Map<Integer, Integer> map = new HashMap<>();
       for (int i = 0; i < nums.length; i++) {
           int complement = target - nums[i];
           if (map.containsKey(complement)) {
               return new int[] { map.get(complement), i };
           }
           map.put(nums[i], i);
       }
       throw new IllegalArgumentException("No two sum solution");
   }
   ~~~

   **Complexity Analysis:**

   - Time complexity : $$O(n)$$. We traverse the list containing $n$ elements only once. Each look up in the table costs only $$O(1)$$ time.

     시간 복잡도 : $$O(n)$$. 우리는 $$n$$ 개의 요소를 가진 리스트를 딱 한 번 가로지른다. 테이블에서의 각 탐색은 $$O(1)$$ 만큼의 시간을 소비한다.

   - Space complexity : $$O(n)$$. The extra space required depends on the number of items stored in the hash table, which stores at most $$n$$ elements.

     해쉬테이블 안에 $$n$$개의 요소들을 저장하기 위해 필요한 아이템들(key 값은 각 요소의 값, value값은 각 요소의 index 값)의 개수만큼 추가 공간이 요구된다.