# 프로그래머스 PCCP 기출문제 1번(붕대 감기)
[붕대 감기](https://school.programmers.co.kr/learn/courses/30/lessons/250137)
```java
class Solution {
    public int solution(int[] bandage, int health, int[][] attacks) {
        int maxHealth = health;
        int idx = 0;
        int con = 0;
        for (int i = 1; i <= attacks[attacks.length - 1][0]; i++) {
            // 공격 받았을 때
            if (i == attacks[idx][0]) {
                health -= attacks[idx][1];
                if(health <= 0) return -1;
                idx++;
                con = 0;
                continue;
            }
            // 시간이 지나서 회복
            health += bandage[1];
            if (health >= maxHealth) health = maxHealth;
            con++;
            // 연속 회복시간을 통한 회복
            if (con == bandage[0]) {
                health += bandage[2];
                if (health >= maxHealth) health = maxHealth;
                con = 0;
            }
        }

        return health;
    }
}
```
* 시간 복잡도를 고려하지 않아도 되는 크기이기 때문에 2중 for문을 사용했다.
* 문제에서 주어진 조건을 잘 읽고 모두 반영해야 한다. (공격을 받았을 때, 연속 회복 시간을 초기화하지 않아서 처음에 틀림)