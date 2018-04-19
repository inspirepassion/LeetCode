Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if(self.depth(root) != -1): return True
        else: return False
        
    def depth(self, root):
        if (root==None):
            return 0
        l = self.depth(root.left)
        if(l==-1):  return -1
        r = self.depth(root.right)
        if(r==-1): return -1
        if(abs(l-r)>1): return -1
        return max(l, r)+1
```