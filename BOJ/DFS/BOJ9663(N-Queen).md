# 백준 9663번 N-Queen
[백준 9663번](https://www.acmicpc.net/submit/9663/61025525)
```java
import java.io.*;

public class Main {
    static int[] arr;
    static int N, count;
    public static void main(String[] args) throws IOException{

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(br.readLine());
        arr = new int[N];

        count = 0;
        DFS(0);

        System.out.println(count);
    }

    public static void DFS(int now){
        // now는 x 좌표, arr[]는 y좌표
        if(now == N){
            count++;
            return;
        }

        for (int i = 0; i < N; i++) {
            arr[now] = i;
            if(check(now)){
                DFS(now + 1);
            }
        }
    }
    public static boolean check(int now) {

        for (int i = 0; i < now; i++) {
            if (arr[now] == arr[i]) {
                return false;
            }
            if (now - i == Math.abs(arr[now] - arr[i])) {
                return false;

            }
        }
        return true;
    }
}
```
