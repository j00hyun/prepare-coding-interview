# 이진 트리의 직경 - leetcode 543

- 내 풀이 (노드 양쪽이 채워져 있을 때만 직경 계산, 예외처리)
``` python
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        result = 0
        
        # 재귀를 통해서 트리 깊이를 계산 
        def dfs(node: TreeNode, depth: int) -> int:
            rtn_left = rtn_right = depth
            
            if node.left:
                rtn_left = dfs(node.left, depth+1)
            
            if node.right:
                rtn_right = dfs(node.right, depth+1)
                
            # 노드가 모두 채워져있을 때, 노드 기준 거리를 계산
            if node.left and node.right:
                nonlocal result
                result = max(result, rtn_left + rtn_right - depth*2)
            
            return max(rtn_left, rtn_right)
           
        depth = dfs(root, 0)
                
        # [2, 3, null, 1] 과 같이 node.left와 node.right가 모두 채워져 있는 경우가 없을 때 return depth
        return max(result, depth)
```

- 다른 풀이 (모든 노드의 직경 검사를 통해 예외 처리 생략)
``` python
class Solution:
    longest: int = 0

    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        def dfs(node: TreeNode) -> int:
            if not node:
                return -1

            # 왼쪽, 오른쪽의 각 리프 노드까지 탐색
            left = dfs(node.left)
            right = dfs(node.right)

            # 가장 긴 경로
            self.longest = max(self.longest, left+right+2)

            # 상태값
            return max(left, right) + 1

        dfs(root)
        return self.longest
```
