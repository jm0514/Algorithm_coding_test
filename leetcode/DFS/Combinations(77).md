# leetcode 77번 Combinations
[leetcode 77번](https://leetcode.com/problems/combinations/description/)
```java
class Solution {
    static int[] nums;
    static List<List<Integer>> answer;
    public List<List<Integer>> combine(int n, int k) {
        nums = new int[k];
        answer = new ArrayList<>();
        com(0, 1, n, k);

        return answer;
    }

    private static void com(int count, int start, int n, int k) {
        List<Integer> list = new ArrayList<>();
        if (count == k) {
            for (int i = 0; i < k; i++) {
                list.add(nums[i]);
            }

            answer.add(list);
            return;
        }

        for (int i = start; i <= n; i++) {
            nums[count] = i;
            com(count + 1, i + 1, n, k); 
        }
    }
}
```