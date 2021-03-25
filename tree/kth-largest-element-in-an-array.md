# 배열의 K번째 큰 요소 - leetcode 215

**1. heapq.nlargest: n번째 큰값까지 배열에 차례대로 저장**


**2. 파이썬의 내부 정렬 함수(sort, sorted)는 대부분의 경우 성능이 가장 좋다**

- 내 풀이 (heap 모듈의 heapify 이용)
``` python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums) # 리스트 -> 최소 힙 
        # 예외처리 
        if len(nums) is 1:
            return heapq.heappop(nums)
        # k번째 가장 큰 요소 -> [len(nums)-k + 1]번째 가장 작은 요소 
        min_k = len(nums) - k + 1
    
        for _ in range(min_k):
            result = heapq.heappop(nums)
            
        return result
```

- 다른 풀이 (heap 모듈의 nlargest 이용)
``` python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return heapq.nlargest(k, nums)[-1]
```

- 다른 풀이 (배열 정렬 이용)
``` python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return sorted(nums, reverse=True)[k - 1]
```
