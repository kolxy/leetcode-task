# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/09 | Monday | [Done](#0519) |
| 05/10 | Tuesday | |
| 05/11 | Wedensday |  |
| 05/12 | Thursday | |
| 05/13 | Friday |  |
| 05/14 | Saturday | |
| 05/15 | Sunday |  |
| 05/16 | Monday | |
| 05/17 | Tuesday | |

# 05/09

## 912. [Sort an Array](https://leetcode.com/problems/sort-an-array/)

Simply quicksort

You may also add images to help with your explanation.

![fig1](./img/Quicksort.png)

### Java
```java
class Solution {
    public int[] sortArray(int[] nums) {
        sort(nums, 0, nums.length - 1);
        return nums;
    }

    public void sort(int[] nums, int left, int right) {
        if (left >= right) {
            return;
            
        }
        random_pivot(nums, left, right);
        int pointer = left;
        for (int i = left; i < right; i++) {
            if (nums[i] <= nums[right]) {
                swap(nums, pointer, i);
                pointer++;
            }
        }
        swap(nums, pointer, right);
        sort(nums, left, pointer - 1);
        sort(nums, pointer + 1, right);
    }
    
    public void random_pivot(int[] nums, int left, int right) {
        int pivot = new Random().nextInt(right - left + 1) + left;
        swap(nums, pivot, right);
    }
    
    public void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```

### Python
```python
class Solution:
    def randomized_partition(self, nums, l, r):
        pivot = random.randint(l, r)
        nums[pivot], nums[r] = nums[r], nums[pivot]
        i = l - 1
        for j in range(l, r):
            if nums[j] < nums[r]:
                i += 1
                nums[j], nums[i] = nums[i], nums[j]
        i += 1
        nums[i], nums[r] = nums[r], nums[i]
        return i

    def randomized_quicksort(self, nums, l, r):
        if r - l <= 0:
            return
        mid = self.randomized_partition(nums, l, r)
        self.randomized_quicksort(nums, l, mid - 1)
        self.randomized_quicksort(nums, mid + 1, r)

    def sortArray(self, nums: List[int]) -> List[int]:
        self.randomized_quicksort(nums, 0, len(nums) - 1)
        return nums
```

# 05/10 
还没开始