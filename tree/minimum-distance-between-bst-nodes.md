# 이진 탐색 트리(BST) 노드 간 최소 거리

- 내 풀이 (배열로 flatting해서 비교)
``` python
class Solution:
    def minDiffInBST(self, root: TreeNode) -> int:
        stack = [root]
        tree_arr = []
        min_diff = 100000 # 조건으로 주어진 노드간 최대 거리
        
        # 이진트리를 배열로 플랫팅
        while stack:
            node = stack.pop()
            if node:
                tree_arr.append(node.val)
                stack.append(node.left)
                stack.append(node.right)
        
        # 노드값 정렬 
        tree_arr.sort()
        
        # 노드간 최소 거리 찾기 
        for idx in range(len(tree_arr) - 1):
            min_diff = min(abs(tree_arr[idx+1] - tree_arr[idx]), min_diff)
            
        return min_diff
```

- 다른 풀이 (중위 순회 - 재귀)
``` python
class Solution:
    prev = -sys.maxsize
    result = sys.maxsize

    # 재귀 구조 중위 순회 비교 결과
    def minDiffInBST(self, root: TreeNode) -> int:
        if root.left:
            self.minDiffInBST(root.left)

        self.result = min(self.result, root.val - self.prev)
        self.prev = root.val

        if root.right:
            self.minDiffInBST(root.right)

        return self.result
```

- 다른 풀이 (중위 순회 - 반복)
``` python
class Solution:
    def minDiffInBST(self, root: TreeNode) -> int:
        prev = -sys.maxsize
        result = sys.maxsize

        stack = []
        node = root

        # 반복 구조 중위 순회 비교 결과
        while stack or node:

            while node:
                stack.append(node)
                node = node.left

            node = stack.pop()

            result = min(result, node.val - prev)
            prev = node.val

            node = node.right
```
