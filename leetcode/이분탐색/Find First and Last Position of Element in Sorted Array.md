# leetcode 34번 Find First and Last position of Element in Sorted Array
[leetcode 34번](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int start = binarySearch(nums, target);
        if (start == nums.length || nums[start] != target) {
            return new int[]{-1, -1};
        }
        int end = binarySearch(nums, target + 1) - 1;
        return new int[]{start, end};
    }

    private int binarySearch(int[] nums, int target) {
        int lt = 0, rt = nums.length;
        while (lt < rt) {
            int mid = (lt + rt) / 2;
            if (nums[mid] < target) {
                lt = mid + 1;
            } else {
                rt = mid;
            }
        }
        return lt;
    }
}
```