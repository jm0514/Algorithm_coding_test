# 프로그래머스 PCCP 기출문제 2번 (시추관)
[시추관](https://school.programmers.co.kr/learn/courses/30/lessons/250136)
```java
import java.util.*;

class Solution {
    static class Point {
        int r, c;
        Point(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }
    static int[] dr = {0, 1, 0, -1};
    static int[] dc = {1, 0, -1, 0};
    static int n, m, nameCount = 1;
    static int[][] name;
    static boolean[][] check;
    public int solution(int[][] land) {
        int answer = 0;
        n = land.length;
        m = land[0].length;
        name = new int[n][m];
        check = new boolean[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (land[i][j] == 1 && !check[i][j]) {
                    // BFS를 통해 석유의 총량을 알아내고 원래 배열(land)을 석유의 총량을 나타내는 배열로 바꾼다.
                    changeArr(i, j, BFS(i, j, land), land);
                }
            }
        }
        
        // 시추관이 땅을 지나가며 캘 수 있는 석유의 총량을 더해야한다.
        int result = 0;
        // 송유관을 위에서 아래로 꽂을 때 같은 이름의 석유 위치를 뽑으면 안되기 때문에 boolean 배열로 판단한다.
        // boolean 배열에 이미 지나간 name의 석유 위치는 지나간다. 처음 지나가는 경우 result에 해당 위치의 석유 총량을 더한다.
        boolean[] named = new boolean[nameCount + 1];
        for (int i = 0; i < m; i++) {
            named[name[0][i]] = true;
            result += land[0][i];
            for (int j = 0; j < n; j++) {
                // 이름이 있는 경우만 구한다.
                if (name[j][i] > 0) {
                    if (!named[name[j][i]]) {
                        named[name[j][i]] = true;
                        result += land[j][i];
                    }
                }
            }
            
            // 시추관이 내려오면서 캘 수 있는 석유의 총량을 최대 값과 비교한다.
            answer = Math.max(answer, result);
            result = 0;
            // 체크한 구역의 이름들을 초기화
            named = new boolean[nameCount + 1];
        }
        return answer;
    }
    
    // 석유를 찾고 석유의 총량을 구한다.
    private static int BFS(int r, int c, int[][] land) {
        Queue<Point> Q = new LinkedList<>();
        Q.add(new Point(r, c));
        check[r][c] = true;
        int max = 1;
        
        while (!Q.isEmpty()) {
            Point p = Q.poll();
            int nowR = p.r;
            int nowC = p.c;
            for (int i = 0; i < 4; i++) {
                int nextR = nowR + dr[i];
                int nextC = nowC + dc[i];
                if (nextR < 0 || nextC < 0 || nextR >= n || nextC >= m) continue;
                if (land[nextR][nextC] == 1 && !check[nextR][nextC]) {
                    Q.add(new Point(nextR, nextC));
                    max++;
                    check[nextR][nextC] = true;
                }
            }
        }
        
        // 공간에 있는 석유의 총량이다.
        return max;
    }
    
    // 석유가 있는 위치를 확인하고 석유가 있는 자리를 석유의 총량으로 바꾸고 해당 위치에 이름을 부여한다.
    private static void changeArr(int r, int c, int max, int[][] land) {
        Queue<Point> Q = new LinkedList<>();
        Q.add(new Point(r, c));
        land[r][c] = max;
        name[r][c] = nameCount;
        
        while (!Q.isEmpty()) {
            Point p = Q.poll();
            int nowR = p.r;
            int nowC = p.c;
            for (int i = 0; i < 4; i++) {
                int nextR = nowR + dr[i];
                int nextC = nowC + dc[i];
                if (nextR < 0 || nextC < 0 || nextR >= n || nextC >= m) continue;
                // 이미 지나갔으며 석유가 있는 자리를 지나가야 한다.
                if (land[nextR][nextC] == 1 && check[nextR][nextC]) {
                    land[nextR][nextC] = max;
                    name[nextR][nextC] = nameCount;
                    Q.add(new Point(nextR, nextC));
                }
            }
        }
        
        // 다음 석유가 위치한 공간의 이름이다. 현재 위치의 이름과 중복되지 않게 +1 한다.
        nameCount++;
    } 
}
```
* 해당 구역의 석유 총량 구하기, 해당 구역의 이름을 지정하기(중복된 값을 더하지 않기 위해), 시추관이 지나가며 캘 수 있는 석유의 총량을 차례로 구해 답을 도출해냈다.