# 프로그래머스 이웃한 칸
[프로그래머스 이웃한 칸](https://school.programmers.co.kr/learn/courses/30/lessons/250125)
```java
class Solution {
    static int[] dh = {0, 1, -1, 0};
    static int[] dw = {1, 0, 0, -1};
    public int solution(String[][] board, int h, int w) {
        int count = 0;
        int n = board[0].length;
        for (int i = 0; i < 4; i++) {
            int h_check = h + dh[i];
            int w_check = w + dw[i];
            if (h_check < 0 || h_check >= n || w_check < 0 || w_check >= n) continue;
            if (board[h][w].equals(board[h_check][w_check])) {
                count++;
            }
        }
        return count;
    }
}
```