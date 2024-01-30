# 프로그래머스 k진수에서 소수 개수 구하기
[프로그래머스 k진수에서 소수 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/92335)
```java
import java.util.*;

class Solution {
    public int solution(int n, int k) {
        String K = makeK(n, k);
        return stringToken(K);
    }
    
    // k진수로 변환
    private static String makeK(int n, int k) {
        StringBuilder sb = new StringBuilder();
        while (n > 0) {
            int mod = n % k;
            n = n / k;
            sb.append(Integer.toString(mod));
        }
        
        return sb.reverse().toString();
    }
    
    // 소수인지 판단
    private static boolean isPrimeNum(Long num) {
        if (num <= 1) return false;
        
        for (int i = 2; i <= (int)Math.sqrt(num); i++) {
            if (num % i == 0) {
                return false;   
            }
        }
        return true;
    }
    
    // 0을 기준으로 문자를 자름
    private static int stringToken(String K) {
        StringTokenizer st = new StringTokenizer(K, "0");
        List<Long> list = new ArrayList<>();
        while (st.hasMoreTokens()) {
            list.add(Long.parseLong(st.nextToken()));
        }
        
        int count = 0;
        for (Long num : list) {
            if (isPrimeNum(num)) {
                System.out.println(num);
                count++;
            }
        }
        
        return count;
    }
}
// int -> Long
// sqrt(제곱근)
// st.hasMoreTokens()
```
* 정수 n을 k진수로 변환할 때, 1,000,000을 k진수로 바꾼다면 int 범위를 벗어날 수 있어 Long을 사용
* StringTokenizer의 개수를 파악하기 어렵다면 hasMoreTokens()를 이용해 토큰이 없을 때 까지 반복