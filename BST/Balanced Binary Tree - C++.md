Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

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
    bool isBalanced(TreeNode* root) {
        if(!root){return true;}
        else{
            int l = depth(root->left);
            int r = depth(root->right);
            return abs(l-r)<=1 && isBalanced(root->left) && isBalanced(root->right);
        }
    }
    int depth(TreeNode* root){
        if (root == NULL){return 0;}
        else{
            return max(depth(root->left), depth(root->right))+1;
        }
    }
};
```