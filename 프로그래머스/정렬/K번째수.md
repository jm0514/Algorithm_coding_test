# 프로그래머스 K번째 수
[프로그래머스 K번째 수](https://school.programmers.co.kr/learn/courses/30/lessons/42748?language=java)
```java
import java.util.*;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        
        int[] answer = new int[commands.length]; //결과는 commands의 행의 크기
        for(int i = 0; i < commands.length; i++) {
            ArrayList<Integer> list = new ArrayList<>(); //for문이 돌때마다 새로운 ArrayList를 생성해야함 
            for (int j = commands[i][0] - 1; j < commands[i][1]; j++) { //commands에 있는 원소들은 인덱스를 나타내기 때문에 -1를 해야 함 
                list.add(array[j]);
            }
            Collections.sort(list); //ArrayList에 값을 담고 정렬
            answer[i] = list.get(commands[i][2] - 1); //또한 인덱스를 나타내기 때문에 1을 뺀다
        }
        return answer;
    }
}
```