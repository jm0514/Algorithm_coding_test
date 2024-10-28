# leetcode 46번 Permutations
[leetcode 46번](https://leetcode.com/problems/permutations/description/)
```java
class Solution {
    static boolean[] check;
    static int[] arr;
    static List<List<Integer>> answer;
    public List<List<Integer>> permute(int[] nums) {
        int len = nums.length;
        answer = new ArrayList<>();
        arr = new int[len];
        check = new boolean[len];
        perm(0, len, nums);
        return answer;
    }

    private static void perm(int depth, int len, int[] nums) {
        if (depth == len) {
            List<Integer> list = new ArrayList<>();
            for (int i = 0; i < len; i++) {
                list.add(arr[i]);
            }
            answer.add(list);
            return;
        }

        for (int i = 0; i < len; i++) {
            if (!check[i]) {
                check[i] = true;
                arr[depth] = nums[i];
                perm(depth + 1, len, nums);
                check[i] = false;
            }
        }
    }
}
```