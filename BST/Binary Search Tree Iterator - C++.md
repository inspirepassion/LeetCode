```c
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class BSTIterator {
public:
    BSTIterator(TreeNode *root) {
        if (root == NULL);
        else{
            TreeNode* cur=root;
            while (cur != NULL){
                node_stack.push(cur);
                cur = cur->left;
            }
        }
    }

    /** @return whether we have a next smallest number */
    bool hasNext() {
        return !node_stack.empty();
    }

    /** @return the next smallest number */
    int next() {
        TreeNode *node = node_stack.top();
        node_stack.pop();
        int node_val = node->val;
        node = node->right;
        while(node != NULL){
            node_stack.push(node);
            node = node->left;
        }
        return node_val;
    }
private:
    stack <TreeNode *> node_stack;
};

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```