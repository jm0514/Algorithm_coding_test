# 프로그래머스 귤 고르기
[프로그래머스 귤 고르기](https://school.programmers.co.kr/learn/courses/30/lessons/138476)
```java
import java.util.ArrayList;
import java.util.HashMap;

class Solution {
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i : tangerine){ // 배열에 담긴 중복된 수를 카운트
            map.put(i, map.getOrDefault(i ,0) + 1);
        }
        
        ArrayList<Integer> list = new ArrayList<>(map.keySet()); // 리스트에 map의 키를 담는다.
        list.sort((o1, o2) -> map.get(o2) - map.get(o1)); // map의 value끼리 비교해서 내림차순으로 정렬한다.(람다식)
        
        int i = 0; // index 역할
        while(k>0){ 
            k -= map.get(list.get(i)); // map의 value를 내림차순으로 정렬한 것을 0번째부터 k에 빼준다.
            i++; // index 추가
            answer++; // while문 돌 때 카운트
        }
        return answer;
    }
}
```
### 다른 방식의 정렬
```java
    list.sort(new Comparator<Integer>(){
    @Override
    public int compare(Integer o1, Ingeger o2){
        int o1 = map.get(o1);
        int o2 = map.get(o2);
        
        if(o1 == o2)return 0;
        else if(o1 < o2)return 1;
        else return -1;
        }
     });
     
```
```java
    list.sort(new Comparator<Integer>(){
        @Override
        public int compare(Integer o1, Integer o2){
        return map.get(o2) - map.get(o1);
        }
    });
```
```java
    list.sort(new Comparator<Integer>(){
        @Override
        public int compare(Integer o1, Integer o2){
        return map.get(o2).compareTo(map.get(o1));
        }
    });
```
* `compareTo`는 숫자의 비교 같은 경우는 단순히 크다(1), 같다(0), 작다(-1) 의 관한 결과값을 리턴