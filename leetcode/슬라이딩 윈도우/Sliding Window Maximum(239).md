# leetcode 239번 Sliding Window Maximum
[leetcode 239번](https://leetcode.com/problems/sliding-window-maximum/description/?source=submission-noac)
```java
import java.util.*;

class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int[] answer = new int[nums.length - k + 1];
        // 인덱스 저장하기 위한 Deque
        Deque<Integer> dq = new LinkedList<>();
        int lt = 0;
        for (int rt = 0; rt < nums.length; rt++) {
            // 현재 위치의 값과 비교했을 때, 작다면 Deque에서 제거
            while (!dq.isEmpty() && nums[rt] > nums[dq.peekLast()]) {
                dq.pollLast();
            }

            dq.offer(rt);

            // 윈도우 범위에서 넘어갔을 때, 왼쪽 인덱스 제거
            if (!dq.isEmpty() && dq.peekFirst() < lt) {
                dq.pollFirst();
            }

            // 윈도우 크기가 k이상 일 때 부터, answer에 대입
            if (rt + 1 >= k) {
                answer[lt] = nums[dq.peekFirst()];
                lt++;
            }
        }

        return answer;
    }
}
```