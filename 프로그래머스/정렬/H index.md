#프로그래머스 H.index
[프로그래머스 H.index](https://school.programmers.co.kr/learn/courses/30/lessons/42747)
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        int len = citations.length;
        
        Arrays.sort(citations); //정렬
        for(int i = 0; i < len; i++){
            if(citations[i] >= len-i){ //최초로 citations[i]이 크거나 같을 경우
                return len-i; //리턴
            }
        }
      
        return answer;
    }
}
```
* 배열의 크기에 비해 원소값들이 크게 나오면 answer는 0이 나올 가능성이 크다.
* 그럴 경우를 빼고는 원소 값들이 배열의 크기와 비슷한 값으로 구성되어 있다고 가정
* 정렬을 한 다음 최초로 len-i(현재 기준(i)에서 맨 뒤까지 길이)보다 citations[i]가 크거나 같을 때 len-i를 리턴한다.
* len-i의 최대 값은 citations[i] 혹은 그 보다 작아야 함
* for문에서 최초로 citations[i]이 크거나 같을 경우가 지나고나면 len-i의 최대값이 변할 수 있기 때문에 바로 리턴해야 함
* **citations[i]는 최소 len-i는 최대 값을 얻어야 함**
* result는 배열(citations) 안의 원소 값으로 나와야 하는것이 아님!!(이것 때문에 잘못 생각) 