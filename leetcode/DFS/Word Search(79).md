# leetcode 79번 Word Search
[leetcode 79번](https://leetcode.com/problems/word-search/description/)
```java
class Solution {
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};
    static boolean[][] check;
    static int N, M;
    public boolean exist(char[][] board, String word) {
        N = board.length;
        M = board[0].length;
        
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                check = new boolean[N][M];
                if (dfs(i, j, 0 ,board, word, check)) {
                    return true;
                }
            }
        }

        return false;
    }

    private static boolean dfs(int x, int y, int idx, char[][] board, String word, boolean[][] check) {
        // board의 단어와 word의 idx번째 단어가 다르면 false 리턴
        if (board[x][y] != word.charAt(idx)) {
            return false;
        }

        // 단어 마지막 인덱스 일 때, board의 단어와 word의 마지막 단어가 일치해야 함
        if (idx == word.length() - 1 && board[x][y] == word.charAt(idx)) { 
            return true;  
        }
        
        check[x][y] = true;
        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];
            if (nx < 0 || nx >= N || ny < 0 || ny >= M) continue;
            if (!check[nx][ny] && dfs(nx, ny, idx + 1, board, word, check)) {
                // exist 메서드의 if문에 true만 보내기 위해서 true 리턴
                return true;
            }
        }

        check[x][y] = false;

        return false;
    }
}
```
* 각 상태마다 개별적인 방문 배열이 필요하기 때문에 BFS는 부적절하다.