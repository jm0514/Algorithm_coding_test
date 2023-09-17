# 백준 9251번 LCS
[백준 9251번](https://www.acmicpc.net/problem/9251)
```java
import java.io.*;

class Main {
    static char[] ch1, ch2;
    static Integer[][] dp;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str1 = br.readLine();
        String str2 = br.readLine();
        int str1Len = str1.length();
        int str2Len = str2.length();
        dp = new Integer[str1Len][str2Len];
        ch1 = str1.toCharArray();
        ch2 = str2.toCharArray();

        System.out.println(LCS(str1Len - 1, str2Len - 1));
    }

    // 최대 길이를 구하는 것이다.(개수가 아님)
    private static int LCS(int idx1, int idx2){

        // 해당 자리가 0보다 작아질 경우 0으로 리턴
        if (idx1 < 0 || idx2 < 0) {
            return 0;
        }

        // 해당 자리가 정해지지 않은 경우
        if (dp[idx1][idx2] == null) {
            // 비교하는 자리의 알파벳이 같다면
            if (ch1[idx1] == ch2[idx2]) {
                // 배열의 해당 위치에서 대각선 방향에 있는 길이에 +1을 한다.
                dp[idx1][idx2] = LCS(idx1 - 1, idx2 - 1) + 1;
            } else {
                // 배열의 해당 위치에서 왼쪽 또는 위에 위치한 길이 중 큰 것을 선택한다. 
                dp[idx1][idx2] = Math.max(LCS(idx1 - 1, idx2), LCS(idx1, idx2 - 1));
            }
        }
        // 해당 자리의 최대 길이 리턴
        return dp[idx1][idx2];
    }
}
```
* 그냥 길이가 아닌 최대 길이를 찾아내는 것이 중요하다.
* 표를 그려 규칙성을 찾아내는 것이 중요하다.
* 규칙성은 다른 사람들이 잘 정리둔 [블로그](https://infodon.tistory.com/78) 를 참조했다.