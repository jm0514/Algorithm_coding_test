# 백준 13144번 List of Unique Numbers
[백준 13144번](https://www.acmicpc.net/problem/13144)
```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N + 1];
        // 해당 숫자를 몇 번 사용했는지 체크하는 용도
        int[] count = new int[100000 + 1];

        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        // 0 부터 시작하지 않고 rt를 생각하면 1부터 시작해야 한다.
        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        int lt = 1;
        int rt = 0;
        long result = 0;
        while (lt <= N) {
            // 검증 단계부터 다음 위치를 생각해서 rt는 0부터 시작하는 것이 맞다.
            // rt의 다음 위치가 N과 같거나 작은 경우와 rt의 다음 위치를 한번도 세지 않았을 경우
            while (rt + 1 <= N && count[arr[rt + 1]] == 0) {
                rt++; // 위에서 검증했기 때문에 증가
                count[arr[rt]]++; // 해당 숫자 카운트
            }

            result += rt - lt + 1;
            // 다음 위치의 연산에서 제외해야 함
            count[arr[lt]]--;
            // 다음 lt
            lt++;
        }

        System.out.println(result);
    }
}

```