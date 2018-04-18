Python2

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    

        
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if (root==None): return True
        else:
            nums = []
            self.insert(root, nums)
            for i in range(nums.__len__()-1):
                if nums[i]>=nums[i+1]: return False
            return True
        
    def insert(self, root, nums):
        if (root != None):
            self.insert(root.left, nums)
            nums.append(root.val)
            self.insert(root.right, nums)
```