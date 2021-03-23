# 이진 트리의 최대 깊이 - leetcode 104

- 내 풀이 (DFS 이용)
``` python
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        # 루트가 없을 경우         
        if root is None:
            return 0
        
        # 재귀를 통해 가장 큰 깊이 측정 
        def dfs(node: TreeNode, deep: int) -> int:
            d_left = d_right = deep
            
            if node.left is not None:
                d_left = dfs(node.left, deep + 1)
            if node.right is not None:
                d_right = dfs(node.right, deep + 1)
                
            return max(d_left, d_right)
        
        return dfs(root, 1)
```

- 다른 풀이 (BFS 이용)
``` python
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        # 예외처리
        if root is None:
            return 0
        queue = collections.deque([root])
        depth = 0

        while queue:
            depth += 1
            # 큐 연산 추출 노드의 자식 노드 삽입
            for _ in range(len(queue)):
                cur_root = queue.popleft()

                if cur_root.left:
                    queue.append(cur_root.left)

                if cur_root.right:
                    queue.append(cur_root.right)

        # BFS 반복 횟수 == 깊이
        return depth
```
