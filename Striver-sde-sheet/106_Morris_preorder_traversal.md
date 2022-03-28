# Morris Preorder Traversal

## Problem statement

Given the `root` of a binary tree, return the **preorder traversal** of its nodes' values using Morris algorithm.

## Solution

Time complexity : O(N)  
Space complexity : O(1)

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> preorder;
    TreeNode* curr = root;
    while(curr != NULL) {
        if(curr -> left == NULL) {
            preorder.push_back(curr -> val);
            curr = curr -> right;
        } else {
            TreeNode* prev = curr -> left;
            while(prev->right != NULL && prev->right != curr) {
                prev = prev -> right;
            }
            if(prev->right == NULL) {
                prev->right = curr;
                preorder.push_back(curr -> val);
                curr = curr -> left;
            } else {
                prev->right = NULL;
                curr = curr -> right;
            }
        }
    }
    return preorder;
}
```
