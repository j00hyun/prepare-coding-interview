# 이진 트리 직렬화 & 역직렬화 - leetcode 297

- 내 풀이
``` python
import collections

class Codec:
    def serialize(self, root: TreeNode) -> str:
        queue = collections.deque([root])
        result_arr = []

        while queue:
            cur_arr = []
            is_leaf = True
            # 해당 깊이의 노드 길이만큼 반복 
            for _ in range(len(queue)):
                node = queue.popleft()
                # 노드가 존재하지 않는다면 'null' 추가
                if not node:
                    cur_arr.append('null')
                    continue
                # 노드가 존재한다면 노드값 추가 
                is_leaf = False
                cur_arr.append(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            # 만약 해당 깊이가 리프가 아니라면 전체 배열에 현재 노드의 값들 추가
            # 리프라면 finish
            if is_leaf is False:
                result_arr += cur_arr

        return '[' + ','.join(result_arr) + ']'
        
    def deserialize(self, data: str) -> TreeNode:
        # 루트 노드가 존재하지 않으면 None 반환
        if len(data[1:-1]) == 0:
            return None
        
        # 루트 노드가 존재 할 경우 부모노드 큐에 루트 노드 추가
        parent_nodes = collections.deque()
        tree_vals = collections.deque(data[1:-1].split(','))
        root = TreeNode(int(tree_vals.popleft()))
        parent_nodes.append(root)
            
        while parent_nodes:
            node = parent_nodes.popleft()
            # 리프까지 진행 
            if tree_vals:
                left_val = tree_vals.popleft()
                right_val = tree_vals.popleft()
                # 부모노드의 왼쪽 자식노드가 존재한다면 트리 추가 
                if left_val != 'null':
                    node.left = TreeNode(int(left_val))
                    parent_nodes.append(node.left)
                # 부모노드의 오른쪽 자식노드가 존재한다면 트리 추가 
                if right_val != 'null':
                    node.right = TreeNode(int(right_val))
                    parent_nodes.append(node.right)

        return root
```
- 직렬화를 진행할 때는 보통 배열 index 0 은 비워두고 index 1 부터 채운다 
