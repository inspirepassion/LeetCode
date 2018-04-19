My code:

```python
#  Time Limit Exceeded
class Node:
    def __init__(self, val=None, cnt = None):
        self.val = val
        self.cnt = cnt
        self.left = None
        self.right = None
        
class KthLargest(object):
    root = Node()
    m_k = int()

    def __init__(self, k, nums):
        """
        :type k: int
        :type nums: List[int]
        """
        
        KthLargest.m_k = k
        KthLargest.root = None
        # i = nums.__len__()
        # j=0
        # while (i>0):
        #     KthLargest.root = self.insert(KthLargest.root, nums[j])
        #     j+=1
        #     i-=1
        for i in nums:
            KthLargest.root = self.insert(KthLargest.root, i)
            
        
    def insert(self, root, val):
        if(root==None): return Node(val, 1)
        if(val <= root.val):    root.left = self.insert(root.left, val)
        else:   root.right = self.insert(root.right, val)
        root.cnt += 1
        return root
    
    def findK(self, root, key):
        # m=(root.right).cnt if root.right!=None else 0
        if (not root.right):  m = 0
        else:   m = (root.right).cnt
            
        if(m+1 == key):   return root.val
        elif(key <m+1):   return self.findK(root.right, key)
        else:   return  self.findK(root.left, key-m-1)

    def add(self, val):
        """
        :type val: int
        :rtype: int
        """
        KthLargest.root = self.insert(KthLargest.root, val)
        return self.findK(KthLargest.root, KthLargest.m_k)
        


# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)
```