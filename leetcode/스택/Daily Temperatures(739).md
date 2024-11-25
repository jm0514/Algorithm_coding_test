# leetcode 739번 Daily Temperatures
[leetcode 739번])(https://leetcode.com/problems/daily-temperatures/description/)
```java
import java.util.*;

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int[] answer = new int[temperatures.length];
        Stack<Integer> stack = new Stack();
        
        for (int i = 0; i < temperatures.length; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int tmp = stack.pop();
                answer[tmp] = i - tmp;
            }

            stack.push(i);
        }

        return answer;
    }
}
```