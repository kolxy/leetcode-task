# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/18 | Wednesday | [Done](#0518) |
| 05/19 | Thursday | [Not started](#0519) |

# 05/18

## 215. [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Priority Queue

Time complexity: O(nlogn)

![fig1](./img/Quicksort.png)

### Heap/PriorityQueue
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue(Collections.reverseOrder());
        for (int num : nums) {
            pq.offer(num);
        }
        for (int i = 1; i < k; i++) {
            pq.poll();
        }
        return pq.poll();
    }
}
```

# 05/19 
还没开始