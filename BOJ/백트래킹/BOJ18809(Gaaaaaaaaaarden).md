# 백준 18809번 Gaaaaaaaaaarden
[백준 18809번](https://www.acmicpc.net/problem/18809)

```java
import java.util.*;
import java.io.*;

class Main {
    static List<int[]> baeyang;
    static int N,M,G,R;
    static int[][] garden;
    static int[] selectBaeyang;
    static int[] selectGR;
    static boolean[] checkedBeayang;
    static int[] spotG, spotR;
    static int[] dx = {0, 1, 0, -1};
    static int[] dy = {1, 0, -1, 0};
    static int max = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        G = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());

        garden = new int[N][M];
        baeyang = new ArrayList<int[]>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < M; j++) {
                garden[i][j] = Integer.parseInt(st.nextToken());

                if (garden[i][j] == 2) {
                    baeyang.add(new int[]{i, j});
                }
            }
        }

        checkedBeayang = new boolean[baeyang.size()];
        spotG = new int[G];
        spotR = new int[R];

        Arrays.fill(spotG, -1);
        Arrays.fill(spotR, -1);

        findSpotG(0);

        System.out.println(max);
    }

    static void findSpotG(int k) {
        if (k == G) {
            findSpotR(0);
            return;
        }

        for (int i = 0; i < baeyang.size(); i++) {
            if (checkedBeayang[i]) continue;
            if (k > 0 && spotG[k - 1] > i) continue;
            checkedBeayang[i] = true;
            spotG[k] = i;
            findSpotG(k + 1);
            spotG[k] = -1;
            checkedBeayang[i] = false;
        }
    }

    static void findSpotR(int k) {
        if (k == R) {
            bfs();
            return;
        }

        for (int i = 0; i < baeyang.size(); i++) {
            if (checkedBeayang[i]) continue;
            if (k > 0 && spotR[k - 1] > i) continue;
            checkedBeayang[i] = true;
            spotR[k] = i;
            findSpotR(k + 1);
            spotR[k] = -1;
            checkedBeayang[i] = false;
        }
    }

    static void bfs() {
        int flower = 0;
        int[][] dist = new int[N][M];
        char[][] flw = new char[N][M];

        Queue<int[]> Q = new LinkedList<int[]>();

        for (int g : spotG) {
            int[] tmp = baeyang.get(g);
            int x = tmp[0];
            int y = tmp[1];

            flw[x][y] = 'G';
            dist[x][y] = 1;
            Q.add(new int[]{x, y, 0, 1});
        }

        for (int r : spotR) {
            int[] tmp = baeyang.get(r);
            int x = tmp[0];
            int y = tmp[1];

            flw[x][y] = 'R';
            dist[x][y] = 1;
            Q.add(new int[]{x, y, 1, 1});
        }

        while (!Q.isEmpty()) {
            int[] cur = Q.poll();
            int x = cur[0];
            int y = cur[1];
            char color = cur[2] == 0 ? 'G' : 'R';
            int time = cur[3];

            if (flw[x][y] == 'F') continue;

            for (int i = 0; i < 4; i++) {
                int nx = dx[i] + x;
                int ny = dy[i] + y;

                if (nx < 0 || ny < 0 || nx >= N || ny >= M) continue;
                if (garden[nx][ny] == 0) {
                    flw[nx][ny] = 'H';
                    continue;
                }
                if (flw[nx][ny] == 'F') continue;
                if (flw[nx][ny] == color) continue;

                if ((color == 'G' && flw[nx][ny] == 'R')
                        || (color == 'R' && flw[nx][ny] == 'G')) {
                    if (dist[nx][ny] == time + 1) {
                        flw[nx][ny] = 'F';
                        flower++;
                    }
                    continue;
                }

                flw[nx][ny] = color;
                dist[nx][ny] = time + 1;

                Q.add(new int[]{nx, ny, cur[2], time + 1});
            }
        }

        max = Math.max(flower, max);
    }
}
```