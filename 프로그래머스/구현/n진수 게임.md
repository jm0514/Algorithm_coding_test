# 프로그래머스 n진수 게임
[프로그래머스 n진수 게임](https://school.programmers.co.kr/learn/courses/30/lessons/17687)

```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    public String solution(int n, int t, int m, int p) {
        String str = "";
        List<Character> list = new ArrayList<>();
        // 미리 구해야 할 개수와 게임 인원을 곱하면 여유있는 글자 수의 n진수 문자열 완성 
        for (int i = 0; i < t * m; i++) {
            str += Integer.toString(i, n).toUpperCase();
        }
        // 순서는 p-1 으로 시작해서 m 씩 증가하면 튜브의 순서만 골라짐 
        for (int i = p - 1; i < str.length(); i += m) {
            // list의 크기가 t보다 작을 때 까지만 넣음
            if (list.size() < t) {
                list.add(str.charAt(i));
            }
        }
        // list 문자열로 변환
        return list.stream()
                .map(String::valueOf)
                .collect(Collectors.joining());
    }
}
```