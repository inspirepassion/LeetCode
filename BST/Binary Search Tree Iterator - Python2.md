```python
# Definition for a  binary tree node
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator(object):
    def __init__(self, root):
        """
        :type root: TreeNode
        """
        self.stack=[]
        cur = root
        if (root == None):
            return None
        else:
            while (cur != None):
                self.stack.append(cur)
                cur = cur.left

    def hasNext(self):
        """
        :rtype: bool
        """
        if (self.stack.__len__()>0): return True
        else: return False
        
        

    def next(self):
        """
        :rtype: int
        """
        node = self.stack.pop()
        node_val = node.val
        cur = node.right
        while (cur != None):
            self.stack.append(cur)
            cur = cur.left
        return node_val
        

# Your BSTIterator will be called like this:
# i, v = BSTIterator(root), []
# while i.hasNext(): v.append(i.next())
```