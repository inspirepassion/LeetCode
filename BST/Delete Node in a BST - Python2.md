```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def deleteNode(self, root, key):
        """
        :type root: TreeNode
        :type key: int
        :rtype: TreeNode
        """
        if (root == None): return None
        else:
            if (key < root.val):   root.left = self.deleteNode(root.left, key)
            elif (key > root.val):    root.right = self.deleteNode(root.right, key)
            else:
                if(root.left==None or root.right==None):
                    #root = root.left if root.left!=None else root.right
                    if (root.left!=None): root = root.left 
                    else:   root = root.right
                else:
                    # candidate = TreeNode()
                    candidate = root.right
                    while( candidate.left != None):  candidate = candidate.left
                    root.val = candidate.val
                    root.right = self.deleteNode(root.right, candidate.val)
        return root
```

Not check out yet

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):  
    def deleteNode(self, root, key):
        """
        :type root: TreeNode
        :type key: int
        :rtype: TreeNode
        """
        if not root:
            return None
        if key < root.val:
            root.left = self.deleteNode(root.left, key)
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else: # already found then delete
            if not root.left:
                return root.right
            elif not root.right:
                return root.left
            
            minNode = self.findMin(root.right)
            root.val = minNode.val
            root.right = self.deleteNode(root.right, root.val)
        
        return root
        
    def findMin(self, node):
        while node.left != None:
            node = node.left
        return node
```