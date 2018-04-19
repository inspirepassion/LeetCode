Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k.

Using BST

```python
class Node(object):
    
    def __init__(self, val=None):
        self.val = val
        self.left = None
        self.right = None
        
class BST(object):
    
    def __init__(self):
        self.root = None
    
    def insert(self, root, val):
        if(not root): root = Node(val)
        elif(val <= root.val):   root.left = self.insert(root.left, val)
        else:   root.right = self.insert(root.right, val)
        return root
    
    def delete(self, root, val):
        if(not root): return False
        elif(val < root.val):   root.left = self.delete(root.left, val)
        elif(val > root.val):   root.right = self.delete(root.right, val)
        else:
            if(not root.left or not root.right):    root = root.left if root.left else root.right
            else:
                temp = root.right
                while(temp.left):   temp = temp.left
                root.val = temp.val
                root.right = self.delete(root.right, temp.val)
        return root
    
    def search(self, root, key, dif):
        if(not root):   return False
        elif(abs(key - root.val) <= dif): return True
        elif(key - root.val > dif): return self.search(root.right, key, dif)
        else:   return self.search(root.left, key, dif)

    
class Solution(object):
    
    def containsNearbyAlmostDuplicate(self, nums, k, t):
        """
        :type nums: List[int]
        :type k: int
        :type t: int
        :rtype: bool
        """
        bst = BST()
        if(nums.__len__() == 0 or k==0): return False
        else:
            for i in range(nums.__len__()-1):
                bst.root = bst.insert(bst.root, nums[i])
                if (i+1 > k):   bst.root = bst.delete(bst.root, nums[i-k])
                if (bst.search(bst.root, nums[i+1], t)):    return True
        return False
```