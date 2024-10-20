# leetcode 11번 Container With Most Water
[leetcode 11번](https://leetcode.com/problems/container-with-most-water/description/)
```java
import java.util.*;

class Solution {
    public int maxArea(int[] height) {
        int answer = 0;
        int lt = 0, rt = height.length - 1;
        while (lt < rt) {
            answer = Math.max(answer, (rt - lt) * Math.min(height[lt], height[rt]));
            if (height[lt] <= height[rt]) {
                lt++; 
            } else {
                rt--;
            }
        }

        return answer;
    }
}
```