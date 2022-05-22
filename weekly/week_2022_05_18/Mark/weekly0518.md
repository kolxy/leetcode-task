# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/21 | Saturday | [Done](#0521) |
| 05/22 | Saturday Sunday | [Done](#0522) |

# 05/21
## 162. [Find Peak Element](https://leetcode.com/problems/find-peak-element/)
### Python
```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
#         l, r = 0, len(nums)-1
#         while l< r:
#             mid = l + (r-l)//2
#             if nums[mid] > nums[mid+1]:
#                 r = mid
#             else: # nums[mid] < nums[mid + 1]
#                 l = mid + 1
#         return l
    
#     def binary_search(array) -> int:
#         # def condition(value) -> bool:
#         #     pass

        left, right = 0, len(nums) - 1
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] > nums[mid + 1]: 
                right = mid #[l, mid]
            else:
                left = mid + 1
        return left



    
    # [1,2,3,1,4] --> not include R
    
    # [9,2,1,3,5,6,4]
    
    # [1,2]
            
```
## 528. [Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)
### Python
```python
class Solution:
    def __init__(self, w: List[int]):

        for i in range(1, len(w)):
            w[i] += w[i-1]
        self.w = w
        
    def pickIndex(self) -> int:
        pic = random.randint(1,self.w[-1])
        # l, r = 0, len(self.w)-1
        # while l < r:
        #     mid = l + (r-l)//2
        #     if self.w[mid] >= pic: # condition(mid)
        #         r = mid # 
        #     else: # self.w[mid] < pic:
        #         l = mid + 1 # first index >= pic
        # return r
    
    
        left, right = 0, len(self.w) - 1
        while left < right:
            mid = left + (right - left) // 2
            if self.w[mid] >= pic:
                right = mid
            else:
                left = mid + 1
        return right

        # Your Solution object will be instantiated and called as such:
        # obj = Solution(w)
        # param_1 = obj.pickIndex()


        # [1,3] 25% 75%
        # [1,3,2] 1/6 3/6 2/6 [#1,2,*3,#4,5,#6] --> 1, [1,4,6]        
```

## 1011. [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
### Python
```python
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
#         l, r = max(weights), sum(weights)
        
#         while l < r:
#             mid = l + (r-l)//2
#             d = 0
#             tem = 0
#             for weight in weights:
#                 tem += weight
#                 if tem > mid:
#                     d += 1
#                     tem = weight
#             d += 1
            
#             if d <= days:
#                 r = mid
#             else:
#                 l = mid + 1 
                
        left, right = max(weights), sum(weights)
        while left < right:
            mid = left + (right - left) // 2
            
            d = 0
            tem = 0
            for weight in weights:
                tem += weight
                if tem > mid:
                    d += 1
                    tem = weight
            d += 1
            
            
            if d <= days:
                right = mid
            else:
                left = mid + 1
        return left                      
```


# 05/22
## 881. [Boats to Save People](https://leetcode.com/problems/boats-to-save-people/)
### Python
```python
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        people.sort()
        
        l, r, res = 0, len(people) - 1, 0
        while l <= r:
            if people[l] + people[r] <= limit:
                l += 1
            r -= 1
            res += 1
        return res        
```
## 141. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
### Python
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if head is None:
            return False
        slow, fast = head, head.next
        while slow != fast:
            if fast is None or fast.next is None:
                return False
            slow = slow.next
            fast = fast.next.next
        return True      
```
## 11. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
### Python
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r, res = 0, len(height) - 1, 0
        while l < r:
            a, b = height[l], height[r]
            tem = (r-l)*min(a, b)
            res = max(res, tem)
            if a < b:
                l += 1
            else:
                r -= 1
        return res        
```
## 986. [Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/)
### Python
```python
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        # # two list -- > two list
        # i, j = 0, 0 
        # res = []
        # while i < len(firstList) and j < len(secondList):
        #     a = firstList[i]
        #     b = secondList[j]
        #     lo = max(a[0],b[0])
        #     hi = min(a[1],b[1])
        #     if hi >= lo:
        #         res.append([lo, hi])
        #     if b[1] > a[1]:
        #         i += 1
        #     else:
        #         j += 1
        # return res
    
        f, s = 0, 0 
        res = []
        while f < len(firstList) and s < len(secondList):
            a, b = firstList[f], secondList[s]
            lo, hi = max(a[0], b[0]), min(a[1], b[1])
            if lo <= hi:
                res.append([lo, hi])
            if b[1] > a[1]:
                f += 1
            else:
                s += 1
        return res      
```
