# Morris Inorder Traversal

## Problem statement

Given the `root` of a binary tree, return the **inorder traversal** of its nodes' values using Morris algorithm.

## Solution

Time complexity : O(N)  
Space complexity : O(1)

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> inorder;
    TreeNode* curr = root;
    while(curr != NULL) {
        if(curr -> left == NULL) {
            inorder.push_back(curr -> val);
            curr = curr -> right;
        } else {
            TreeNode* prev = curr -> left;
            while(prev->right != NULL && prev->right != curr) {
                prev = prev -> right;
            }
            if(prev->right == NULL) {
                prev->right = curr;
                curr = curr -> left;
            } else {
                prev->right = NULL;
                inorder.push_back(curr -> val);
                curr = curr -> right;
            }
        }
    }
    return inorder;
}
```
