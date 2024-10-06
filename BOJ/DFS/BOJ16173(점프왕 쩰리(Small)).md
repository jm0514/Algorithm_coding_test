# 백준 16173번 점프왕 쩰리(Small)
[백준 16173번](https://www.acmicpc.net/problem/16173)
```java
import java.io.*;
import java.util.*;

public class Main {
    static int[][] arr;
    static boolean[][] check;
    static int N;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        arr = new int[N][N];
        check = new boolean[N][N];
        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < N; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        if (dfs(0,0)) {
            System.out.println("HaruHaru");
        } else {
            System.out.println("Hing");
        }
    }

    private static boolean dfs(int i, int j) {
        if (i < 0 || i >= N || j < 0 || j >= N) return false;
        if (check[i][j]) return false;
        if (i == N - 1 && j == N - 1) return true;
        check[i][j] = true;
        int move = arr[i][j];

        boolean goDown = dfs(i + move, j);
        if (goDown) return true;

        boolean goRight = dfs(i, j + move);
        if (goRight) return true;

        return false;
    }
}

```