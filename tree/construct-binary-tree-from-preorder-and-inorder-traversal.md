# 전위, 중위 순회 결과로 이진 트리 구축 - leetcode 105

- 내 풀이
``` python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        queue = collections.deque(preorder)
        
        def dfs(arr: List[int]) -> TreeNode:
            if arr:
                # preorder에서 차례대로 빼 중심 노드로 저장 
                node = TreeNode(queue.popleft())
                node_idx = arr.index(node.val)
                
                # inorder를 중심노드 기준으로 나누어 왼쪽 노드, 오른쪽 노드 분리후 재귀 
                left_node = dfs(arr[:node_idx])
                right_node = dfs(arr[node_idx+1:])
                
                # 재귀 결과 노드를 각각 중심노드의 왼쪽과 오른쪽에 연결 후 중심노드 반환 
                node.left = left_node
                node.right = right_node

                return node

        return dfs(inorder)
```

- 다른 풀이 (간결하지만 데크를 쓰지않고 큐를 구현하여 시간복잡도 증가)
``` python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if inorder:
            # 전위 순회 결과는 중위 순회 분할 인덱스
            index = inorder.index(preorder.pop(0))

            # 중위 순회 결과 분할 정복
            node = TreeNode(inorder[index])
            node.left = self.buildTree(preorder, inorder[:index])
            node.right = self.buildTree(preorder, inorder[index+1:])

            return node
```
