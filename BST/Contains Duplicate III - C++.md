Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k.

My code (using BST)

```c
/**
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode* left;
 *     TreeNode* right;
 * 
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = nullptr;
 *         this->right = nullptr;
 *     }
 * };
 */

class BST{
public:
    BST(){
        root = nullptr;
    }
    
    TreeNode* insert(TreeNode* node, int val){
        if(!node){node = new TreeNode(val);}
        else if(val <= node->val) node->left = insert(node->left, val);
        else    node->right = insert(node->right, val);
        return node;
    }
    
    TreeNode* insert(int val){
        root = insert(root, val);
        return root;
    }
    
    TreeNode* delNode(TreeNode* node, int val){
        if(!node)   return nullptr;
        if(val < node->val) node->left = delNode(node->left, val);
        else if(val > node->val)    node->right = delNode(node->right, val);
        else{
            // if(!node->left || !node->right) node = node->left ? node->left:node->right;
            if(!node->left || !node->right){
                if(node->left) node = node->left;
                else node = node->right;
            }
            else{
                TreeNode* temp = node->right;
                while(temp->left)   temp = temp->left;
                node->val = temp->val;
                node->right = delNode(node->right, temp->val);
            }
        }
        return node;
    }
    
    TreeNode* delNode(int val){
        root = delNode(root, val);
        return root;
    }
    
    bool search(TreeNode* node, long val, int t){
        if(!node)   return false;
        if(abs(node->val - val) <= t)   return true;
        else if(val - t > node->val)    return search (node->right, val, t);
        else    return search (node->left, val, t);
    }
    
    bool search(int val, int t){
        return search(root, val, t);
    }
    
private:
    TreeNode* root;
};

class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        if(k<=0 || nums.size()==0)  return false;
        BST bst;
        for(int i=1; i< nums.size(); ++i){
            bst.insert(nums[i-1]); // note that we insert i-1 instead of i th element. This is might due to we want prevent from searching nums[0] when nums[0] is the root of the TreeNode, in which case it always returns true.
            
            if (i-1>k-1) bst.delNode(nums[i-1-k]);
            if(bst.search(nums[i], t))  return true; // it always compare the next one to previous one, avoiding search the first element when it happens to be the root of TreeNode.
        }
        return false;
    }
};
```

Others:

```c
/**
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode* left;
 *     TreeNode* right;
 * 
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = nullptr;
 *         this->right = nullptr;
 *     }
 * };
 */
class BST {
public:
    TreeNode* root;
    
    BST() {
        root = nullptr;
    }
    
    TreeNode* insert(int val) {
        root = insert(root, val);
        return root;
    }
    
    TreeNode* insert(TreeNode* now, int val) {
        if (!now) now = new TreeNode(val);
        else if (val > now->val) now->right = insert(now->right, val);
        else if (val < now->val) now->left = insert(now->left, val);
        return now;
    }
    
    TreeNode* remove(int val) {
        root = remove(root, val);
        return root;
    }
    
    TreeNode* remove(TreeNode* now, int val) {
        if (!now) {
            return nullptr;
        } else if (val < now->val) {
            now->left = remove(now->left, val);
        } else if (val > now->val) {
            now->right = remove(now->right, val);
        } else {
            if (!now->left) {
                TreeNode *tmp = now->right;
                delete now;
                return tmp;
            } else if (!now->right) {
                TreeNode *tmp = now->left;
                delete now;
                return tmp;
            } else {
                TreeNode *tmp = now->right;
                while (tmp->left) tmp = tmp->left;
                now->val = tmp->val;
                now->right = remove(now->right, now->val);
            }
        }
        return now;
    }
    
    bool search(int val, int t) {
        return search(root, val, t);
    }
    
    bool search(TreeNode* now, long val, int t) {
        if (!now) return false;
        else if (abs(val - now->val) <= t) return true;
        else if (now->val - t > val) return search(now->left, val, t);
        else return search(now->right, val, t);
    }
};

class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        if (nums.empty() || k == 0) return false;
        BST bst;
        for (int i = 1; i < nums.size(); ++i) {
            bst.insert(nums[i - 1]);
            if (i > k) bst.remove(nums[i - k - 1]);
            if (bst.search(long(nums[i]), t)) return true;
        }
        return false;
    }
};
```