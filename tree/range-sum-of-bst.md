# 이진 탐색 트리(BST) 합의 범위 - leetcode 938

- 내 풀이 (DFS 재귀 구현)
``` python
class Solution:
    sum = 0

    def rangeSumBST(self, root: TreeNode, low: int, high: int) -> int:
        # 노드가 존재하는 경우 
        if root:
            # 범위안에 들어가는 노드이면 합에 추가 
            if low <= root.val <= high:
                self.sum += root.val
                self.rangeSumBST(root.left, low, high)
                self.rangeSumBST(root.right, low, high)
            # 범위보다 작으면 오른쪽 자식 노드로 이동 
            elif root.val < low:
                self.rangeSumBST(root.right, low, high)
            # 범위보다 크면 왼쪽 자식 노드로 이동 
            else:
                self.rangeSumBST(root.left, low, high)

        return self.sum
```
