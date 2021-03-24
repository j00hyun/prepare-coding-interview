# 이진 탐색 트리(BST)를 더 큰 수 합계 트리로 - leetcode 1038

- 내 풀이
``` python
class Solution:
    child_sum = 0
    
    def bstToGst(self, root: TreeNode) -> TreeNode:
        # 리프 노드에 닿을때까지 오른쪽 아래로 계속 이동 
        if root.right:
            self.bstToGst(root.right)
            
        # 부모 노드로 올라오며 값을 더함
        root.val += self.child_sum
        self.child_sum = root.val
        
        # 부모 노드로 올라오다가 왼쪽 아래 자식노드가 존재하면 왼쪽으로 내려감 
        if root.left:
            self.bstToGst(root.left)
            
        return root
```

- 다른 풀이 (처음부터 노드가 존재하는지 계산하는 방식으로 if 문을 여러개 쓰지 않음)
``` python
class Solution:
    child_sum = 0

    def bstToGst(self, root: TreeNode) -> TreeNode:
        # 중위 순회 노드 값 누적 
        if root:
            self.bstToGst(root.right)
            root.val += self.child_sum
            self.child_sum = root.val
            self.bstToGst(root.left)

        return root
```
