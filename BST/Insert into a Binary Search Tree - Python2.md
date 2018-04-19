```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def insertIntoBST(self, root, val):
        """
        :type root: TreeNode
        :type val: int
        :rtype: TreeNode
        """
        if (root == None):  root.val = val
        elif (val <= root.val and root.left == None):
            root.left = TreeNode(val)
        elif (val > root.val and root.right == None):
            root.right = TreeNode(val)
        elif (val <= root.val and root.left != None):
            self.insertIntoBST(root.left, val)
        elif (val > root.val and root.right != None):
            self.insertIntoBST(root.right, val)
        return root
            
```