# 백준 11559번 Puyo Puyo
[백준 11559번](https://www.acmicpc.net/problem/11559)
```java
import java.io.*;
import java.util.*;

public class Main {
    static class Point {
        int x, y;
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    static int[] dx = {-1, 0, 1, 0};
    static int[] dy = {0, 1, 0, -1};
    static boolean[][] check;
    static char[][] arr;
    static int answer;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        arr = new char[12][6];
        answer = 0;

        for (int i = 0; i < 12; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 0; j < 6; j++) {
                arr[i][j] = input[j];
            }
        }

        while (true) {
            check = new boolean[12][6];
            boolean flag = false;

            for (int j = 0; j < 6; j++) {
                for (int i = 11; i >= 0; i--) {
                    if (arr[i][j] != '.' && !check[i][j]) {
                        // checkPop 메서드를 통해 4개 연속으로 붙어있는 블록을 '.'으로 수정
                        if (checkPop(i, j, arr[i][j])) flag = true;
                    }
                }
            }

            // 변한게 없을 경우 break
            if (!flag) break;
            
            // 변경된 블록을 아래로 내려오게 하는 로직
            down();
            // 블록을 내리고 카운트
            answer++;
        }

        System.out.println(answer);
    }

    private static boolean checkPop(int x, int y, char now) {
        // 지나온 경로를 저장하기 위해 List 사용
        ArrayList<Point> list = new ArrayList<>();
        Queue<Point> q = new LinkedList<>();
        
        check[x][y] = true;
        q.add(new Point(x, y));
        list.add(new Point(x, y));
        int qCount = 1;
        
        while (!q.isEmpty()) {
            Point p = q.poll();

            for (int i = 0; i < 4; i++) {
                int nx = dx[i] + p.x;
                int ny = dy[i] + p.y;

                if (nx >= 12|| nx < 0 || ny >= 6 || ny < 0) continue;
                if (!check[nx][ny] && now == arr[nx][ny]) {
                    q.add(new Point(nx, ny));
                    list.add(new Point(nx, ny));
                    check[nx][ny] = true;
                    qCount++;
                }
            }
        }

        if (qCount >= 4) {
            // 4개가 연속으로 존재하는 경우 지나온 경로를 '.'으로 수정
            for (Point p : list) {
                arr[p.x][p.y] = '.';
            }

            return true;
        }

        return false;
    }

    private static void down() {
        for (int i = 0; i < 6; i++) {
            Queue<Character> q = new LinkedList<>();
            for (int j = 11; j >= 0; j--) {
                if (arr[j][i] != '.') {
                    q.add(arr[j][i]);
                }
            }

            if (!q.isEmpty()) {
                int size = q.size();
                for (int k = 0; k < size; k++) {
                    // 맨 아래서 부터 큐에 담긴 문자들을 넣음
                    arr[11 - k][i] = q.poll();
                }
                
                for (int k = 11 - size; k >= 0; k--) {
                    // 큐에 담긴 것을 모두 넣고 남은 자리를 '.'으로 채움
                    arr[k][i] = '.';
                }
            }
        }

    }
}
```