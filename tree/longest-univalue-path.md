# 가장 긴 동일 값의 경로 - leetcode 687

- 내 풀이 (DFS 사용)
``` python
class Solution:
    longest: int = 0
        
    def longestUnivaluePath(self, root: TreeNode) -> int:
        def dfs(node: TreeNode) -> int:
            left = right = 0
            # 왼쪽 노드가 존재한다면 해당 노드의 경로값을 가져옴
            if node.left:
                left = dfs(node.left)
                # 노드값이 서로 동일하다면 경로값 + 1
                if node.val == node.left.val:
                    left += 1
                else: # 노드값이 동일하지 않다면 경로값 0으로 리셋 
                    left = 0
            # 오른쪽 노드도 동일하게 진행 
            if node.right:
                right = dfs(node.right)
                
                if node.val == node.right.val:
                    right += 1
                else:
                    right = 0
            # 가장 긴 경로값을 저장   
            self.longest = max(self.longest, left + right)
            # 현재 노드의 왼쪽 오른쪽 중 최대 경로값을 리턴 
            return max(left, right)
        
        if root:
            dfs(root)
            
        return self.longest
```
