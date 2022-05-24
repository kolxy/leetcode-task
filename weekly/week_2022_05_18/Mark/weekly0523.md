# Index

| Date | Day | Status |
| ----------- | ----------- | ----------- |
| 05/23 | Monday | [Done](#0523) |
| 05/24 | Tuesday | [Not yet](#0524) |
| 05/25 | Monday | [Not yet](#0525) |
| 05/26 | Tuesday | [Not yet](#0526) |
| 05/27 | Monday | [Not yet](#0527) |
| 05/28 | Tuesday | [Not yet](#0528) |
| 05/29 | Tuesday | [Not yet](#0529) |

# 05/23
## 39. [Combination Sum](https://leetcode.com/problems/combination-sum/)
### Python
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
#         res = []
#         self.bfs(candidates, target,[],res)
#         return res
    
#     def bfs(self,candidates, target,path, res):
#         if target < 0:
#             return
#         if target == 0:
#             res.append(path)
#             return
#         for i in range(len(candidates)):
#             self.bfs(candidates[i:], target-candidates[i],path+[candidates[i]],res)
        
        # Backtracking
        def bt(rem, tem, ini, N):
            if rem == 0:
                res.append(list(tem))  
                return
            if rem > 0:
                for i in range(ini, N):
                    tem.append(candidates[i])
                    bt(rem - candidates[i], tem, i, N)
                    tem.pop()
        res = []
        bt(target, [], 0, len(candidates))
        return res         
```
