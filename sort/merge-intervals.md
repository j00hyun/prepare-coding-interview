# 구간 병합 - leetcode 56

- 내 풀이 
``` python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # 입력 함수 오름차순 정렬 
        intervals.sort()
        result = [intervals[0]]
        
        for idx in range(1, len(intervals)):
            end = result[-1][1]
            # 이전 끝 값과 현재 앞 값이 겹치는 구간이 발생 
            if end >= intervals[idx][0]:
                # 이전 끝 값과 현재 끝 값 중 큰 값을 끝 값으로 선택 
                result[-1][1] = max(end, intervals[idx][1])
            else:
                # 겹치지 않으면 그대로 result 배열에 복사 
                result.append(intervals[idx])
                
        return result
```

- 다른 풀이 (콤마 연산자 사용)
``` python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        merged = []

        for i in sorted(intervals, key=lambda x: x[0]):
            if merged and i[0] <= merged[-1][1]:
                merged[-1][1] = max(merged[-1][1], i[1])
            else:
                merged += i,

        return merged
```
