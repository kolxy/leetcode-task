# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/18 | Wednesday | [Done](#0518) |
| 05/19 | Thursday | [Done](#0519) |
| 05/20 | Friday | [Done](#0520) |
| 05/21 | Saturday | [Done](#0521) |
| 05/22 | Sunday | [Done](#0522) |

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

## 215. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
Bucket sort 
Time complexity: O(n)
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

# 05/20

## 162. [Find Peak Element](https://leetcode.com/problems/find-peak-element/)

Binary Search

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if ((mid - 1) >= left && nums[mid - 1] > nums[mid]) {
                right = mid - 1;
            } else if ((mid + 1) <= right && nums[mid + 1] > nums[mid]) {
                left = mid + 1;
            } else {
                return mid;
            }
        }
        return left;
    }
}
```

# 05/21

## 11. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

Two pointer

Time complexity: O(n)
```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int maxWater = 0;
        while (left < right) {
            int water = Math.min(height[left], height[right]) * (right - left);
            maxWater = Math.max(water, maxWater);
            if (height[left] < height[right])
                left++;
            else
                right--;
        }
        return maxWater;
    }
}
```

# 05/22

## 39. [Combination Sum](https://leetcode.com/problems/combination-sum/)

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        backtrack(candidates, target, 0);
        return res;
    }
    
    List<Integer> track = new ArrayList<>();
    public void backtrack(int[] candidates, int target, int index) {
        if (target == 0) {
            res.add(new ArrayList<>(track));
            return;
        }
        if (target < 0) {
            return;
        }
        for (int i = index; i < candidates.length; i++) {
            track.add(candidates[i]);
            backtrack(candidates, target - candidates[i], i);
            track.remove(track.size() - 1);
        }
    }
}
```