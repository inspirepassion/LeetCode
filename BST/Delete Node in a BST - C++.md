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
    TreeNode* deleteNode(TreeNode* root, int key) {
        if (!root)  return NULL;
        else{
            if(key < root->val) root->left = deleteNode(root->left, key);
            else if (key > root->val)   root->right = deleteNode(root->right, key);
            else{
                if (!root->left || !root->right)    root = (root->left)? root->left:root->right;
                else{
                    TreeNode* candidate = root->right;
                    while (candidate->left)   candidate = candidate->left;
                    root->val = candidate->val;
                    root->right = deleteNode(root->right, candidate->val);
                }
            }
        }
        return root;
        
    }
};
```

Not figure out yet the below one

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

static auto x = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        if (!root) {
            return nullptr;
        }
        auto left = deleteNode(root->left, key);
        auto right = deleteNode(root->right, key);
        if (root->val == key) {
            if (root->left && root->right) {
                auto p = root->left;
                while (p->right != nullptr) {
                    p = p->right;
                }
                p->right = root->right;
                return root->left;
            }
            return (root->left == nullptr ? root->right : root->left);
        }
        root->left = left;
        root->right = right;
        return root;
    }
};
```