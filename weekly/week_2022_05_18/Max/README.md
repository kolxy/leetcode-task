# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/18 | Wednesday | [Done](#0518) |
| 05/19 | Thursday | [Not started](#0519) |

# 05/18

## 215. [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Priority Queue

Time complexity: O(nlogn)

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

### Quick Select
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, 0, nums.length - 1, k - 1);
    }
    
    public int quickSelect(int[] nums, int left, int right, int target) {
        if (left == right) {
            return nums[left];
        }
        int pointer = left;
        for (int i = left; i < right; i++) {
            if (nums[i] >= nums[right]) {
                swap(nums, i, pointer);
                pointer++;
            }
        }
        swap(nums, pointer, right);
        if (pointer == target) {
            return nums[target];
        } else if (pointer > target) {
            return quickSelect(nums, left, pointer - 1, target);
        } else {
            return quickSelect(nums, pointer + 1, right, target);
        }
    }
    
    public void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```



# 05/19 
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        List<Integer>[] counts = new ArrayList[nums.length];
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int count = entry.getValue();
            if (counts[count - 1] == null) {
                counts[count - 1] = new ArrayList<>();
            }
            counts[count - 1].add(entry.getKey());
        }
        
        List<Integer> res = new ArrayList<>();
        for (int i = counts.length - 1; i >= 0; i--) {
            if (counts[i] != null) {
                res.addAll(counts[i]);
            }
            if (res.size() >= k) {
                return res.stream().mapToInt(Integer::intValue).toArray();
            }
        }
        return res.stream().mapToInt(Integer::intValue).toArray();
    }
}
```