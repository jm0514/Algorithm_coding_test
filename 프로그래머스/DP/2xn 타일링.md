# 프로그래머스 2xn 타일링
[프로그래머스 2xn 타일링](https://school.programmers.co.kr/learn/courses/30/lessons/12900)
```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        int dp[] = new int[60001];
        
        dp[1] = 1;
        dp[2] = 2;
        
        for(int i = 3; i < 60001; i++){
            dp[i] = (dp[i - 1] + dp[i - 2]) % 1000000007;
        }
        answer = dp[n];
        return answer;
    }
}
```
* 규칙성을 파악하는 것이 중요