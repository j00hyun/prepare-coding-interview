# 균형 이진 트리 - leetcode 110

**균형 이진 트리 : 노드의 왼쪽 서브트리와 오른쪽 서브트리의 차이가 1 이하인 트리 

- 내 풀이 (DFS)
``` python
import collections

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        # 재귀 함수 
        def dfs(node: TreeNode) -> int:
            left_depth = right_depth = 0
            
            # 해당 노드를 기준으로 왼쪽, 오른쪽 서브노드의 깊이를 구함 
            if node.left:
                left_depth = dfs(node.left)
            if node.right:
                right_depth = dfs(node.right)
                
            # 이미 불균형하다는 것이 밝혀졌을 경우 계속 -1 리턴 
            if left_depth == -1 or right_depth == -1:
                return -1
            
            # 서브노드의 차이가 2 이상이라면 -1 리턴
            if abs(left_depth - right_depth) > 1:
                return -1
            
            # 부모 노드를 기준으로 해당 서브노드의 깊이를 리턴
            return max(left_depth, right_depth) + 1
        
        if root:  
            if dfs(root) == -1: # 불균형트리 
                return False
        
        # 루트노드가 존재하지 않거나 균형트리일때 True 반환 
        return True
```
