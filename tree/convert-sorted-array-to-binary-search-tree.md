# 정렬된 배열의 이진 탐색 트리 변환 - leetcode 108

- 내 풀이 
``` python
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        def makeBST(node: TreeNode, left_nums: List[int], right_nums: List[int]):
            # 왼쪽 노드에 넣을 숫자가 존재하는 경우 왼쪽 노드에 넣어주고 왼쪽 노드로 이동 
            if left_nums:
                left_half = len(left_nums) // 2
                node.left = TreeNode(left_nums[left_half])
                makeBST(node.left, left_nums[:left_half], left_nums[left_half + 1:])
            
            # 오른쪽 노드에 넣을 숫자가 존재하는 경우 오른쪽 노드에 넣어주고 오른쪽 노드로 이동 
            if right_nums:
                right_half = len(right_nums) // 2
                node.right = TreeNode(right_nums[right_half])
                makeBST(node.right, right_nums[:right_half], right_nums[right_half + 1:])

        # 리스트의 가운데 값을 루트로 설정 
        half = len(nums) // 2
        root = TreeNode(nums[half])
        left_nums, right_nums = nums[:half], nums[half+1:]
        # 모든 리스트의 숫자를 써서 BST를 만들떄 까지 가운데 값을 노드로 설정하는 것 반복
        makeBST(root, left_nums, right_nums)
        
        return root
```

- 다른 풀이 (자기 자신을 재귀함으로써 중복되지 않고 짧은 코드 구현)
``` python
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if not nums:
            return None

        mid = len(nums) // 2

        # 분할 정복으로 이진 검색 결과 트리 구성
        node = TreeNode(nums[mid])
        node.left = self.sortedArrayToBST(nums[:mid])
        node.right = self.sortedArrayToBST(nums[mid+1:])

        return node
```
