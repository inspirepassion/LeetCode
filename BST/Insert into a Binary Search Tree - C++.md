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
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (root->val == NULL){
            root->val = val;
            return root;
        }
        else if(val <= root->val){
            if(root->left == NULL){
                TreeNode* node=new TreeNode(val);
                root->left= node ;
                //node->left->val = val;
                //root->left->val = val;
            }
            else{
                insertIntoBST(root->left, val);
            }
        }
        else{
            if(root->right == NULL){
                TreeNode* node=new TreeNode(val);
                root->right= node ;
                //node->right->val = val;
                //root->right->val = val;
            }
            else{
                insertIntoBST(root->right, val);
            }
        }
        return root;
    }
};
```