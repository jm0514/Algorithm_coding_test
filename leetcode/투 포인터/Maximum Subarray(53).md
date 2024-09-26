# leetcode 53번 Maximum Subarray
[leetcode 53번](https://leetcode.com/problems/maximum-subarray/description/)
```java
class Solution {
    public int maxSubArray(int[] nums) {
        
        int len = nums.length;
        int lt = 0, max = nums[0], sum = 0;
        for (int rt = 0; rt < len; rt++) {
            sum += nums[rt];
            max = Math.max(max, sum);

            while (sum < 0 && lt <= rt) {
                sum -= nums[lt];
                lt++;
            }
        }

        return max;
    }
}
```