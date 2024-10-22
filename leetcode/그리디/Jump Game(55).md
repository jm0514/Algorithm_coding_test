# leetcode 55번 Jump Game
[leetcode 55번](https://leetcode.com/problems/jump-game/description/)
```java
import java.util.*;

class Solution {
    public boolean canJump(int[] nums) {
        int maxIdx = 0;
        for (int i = 0; i < nums.length; i++) {
            maxIdx = Math.max(maxIdx, nums[i] + i);
            
            if (maxIdx >= nums.length - 1) return true;
            else if (maxIdx == i) return false;
        }

        return true;
    }
}
```