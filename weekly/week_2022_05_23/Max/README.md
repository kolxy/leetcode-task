# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/23 | Monday | 请假 |
| 05/24 | Tuesday | [Done](#0524) |
| 05/25 | Wednesday | [Not yet](#0525) |
| 05/26 | Thursday | [Not yet](#0526) |
| 05/27 | Friday | [Not yet](#0527) |
| 05/28 | Saturday | [Not yet](#0528) |
| 05/29 | Sunday | [Not yet](#0529) |

# 05/24

## 739. [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/submissions/)

Monotonic Stack

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] res = new int[n];
        Stack<Integer> s = new Stack<>();
        for (int i = n - 1; i >= 0; i--) {
            while (!s.isEmpty() && temperatures[s.peek()] <= temperatures[i]) {
                s.pop();
            }
            res[i] = s.isEmpty() ? 0 : (s.peek() - i); 
            s.push(i); 
        }
        return res;
    }
}
```

# 05/25

## 3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Two pointer + HashSet

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int res = 0;
        int left = 0;
        int right = 0;
        Set<Character> set = new HashSet<>();
        while (right < s.length()) {
           if (set.contains(s.charAt(right))) {
               set.remove(s.charAt(left));
               left++;
           } else {
               set.add(s.charAt(right));
               res = Math.max(set.size(), res);
               right++;
           }
        }
        return res;
    }
}
```