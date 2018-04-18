C++

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        if(!root) return true;
        vector<int> nums;
        insert(root, nums);
        for(int i=nums.size()-1; i>0; i--){
            if(nums[i]<=nums[i-1]) return false;
        }
        return true;
    }
    void insert(TreeNode* node, vector<int> &nums){
        if(node){
            insert(node->left, nums);
            nums.push_back(node->val);
            insert(node->right, nums);
        }
        
    }
};
```