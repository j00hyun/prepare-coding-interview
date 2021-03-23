# 이진 트리 반전 - leetcode 226

- 내 풀이 (BFS 사용)
``` python
import collections

class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        queue = collections.deque([root])
        
        # 리프까지 BFS
        while queue:
            node = queue.popleft()
            # node가 존재할 때, 왼쪽노드와 오른쪽노드를 서로 바꿔준 후 큐에 저장 반복 
            if node:
                node.left, node.right = node.right, node.left
                queue.append(node.left)
                queue.append(node.right)
                
        return root
```

- 다른 풀이 (짧고 간결)
``` python
class Solution:
    def invertTree(self, root:TreeNode) -> TreeNode:
        if root:
            root.left, root.right = \
                self.invertTree(root.right), self.invertTree(root.left)
            return root
```
