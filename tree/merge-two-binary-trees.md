# 두 이진 트리 병합 - leetcode 617

**둘중에 한 노드가 None이면 그 밑부터는 비교할 필요 없음!!**

- 내 풀이 (가장 깊은 곳 까지 모두 비교)
``` python
class Solution:
    def mergeTrees(self, root1: TreeNode, root2: TreeNode) -> TreeNode:
        def dfs(node1: TreeNode, node2: TreeNode):
            # 현재 노드의 왼쪽 자식노드 검사 
            if node1.left or node2.left:
                # 현재 노드의 자식노드가 적어도 1개 존재하면 존재하지 않는 자식노드 생성해주기 
                if not node1.left:
                    node1.left = TreeNode()
                if not node2.left:
                    node2.left = TreeNode()
                # 자식노드끼리 더해서 저장 
                node1.left.val += node2.left.val
                # 그 다음 노드로 이동 
                dfs(node1.left, node2.left)
            # 현재 노드의 오른쪽 자식노드 검사 
            if node1.right or node2.right:
                if not node1.right:
                    node1.right = TreeNode()
                if not node2.right:
                    node2.right = TreeNode()
                    
                node1.right.val += node2.right.val
                dfs(node1.right, node2.right)
        
        # 첫번째 노드 검사 
        if root1 or root2:
            if not root1:
                root1 = TreeNode()
            if not root2:
                root2 = TreeNode()
            
            root1.val += root2.val
            dfs(root1, root2)
        
        return root1
```

- 다른 풀이 (둘중 한 노드가 존재하지 않으면 그 밑으로 비교 X)
``` python
class Solution:
    def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
        if t1 and t2:
            node = TreeNode(t1.val + t2.val)
            node.left = self.mergeTrees(t1.left, t2.left)
            node.right = self.mergeTrees(t1.right, t2.right)

            return node

        else: # 이 경우 이 노드 밑에 있는 자식노드들이 전부 묶여 리턴된다.
            return t1 or t2
```
