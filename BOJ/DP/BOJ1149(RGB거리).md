# 백준 1149번 RGB 거리
[백준 1149번](https://www.acmicpc.net/problem/1149)
```java
import java.io.*;
import java.util.*;

class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());

        int[][] dp = new int[N + 1][3];

        for(int i = 1; i <= N; i++){
            StringTokenizer st = new StringTokenizer(br.readLine(), " ");
            int red = Integer.parseInt(st.nextToken());
            int green = Integer.parseInt(st.nextToken());
            int blue = Integer.parseInt(st.nextToken());

            dp[i][0] = Math.min(dp[i - 1][1], dp[i - 1][2]) + red;
            dp[i][1] = Math.min(dp[i - 1][0], dp[i - 1][2]) + green;
            dp[i][2] = Math.min(dp[i - 1][0], dp[i - 1][1]) + blue;
        }

        System.out.println(Math.min(dp[N][0], Math.min(dp[N][1], dp[N][2])));
    }
}
```