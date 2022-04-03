# Balanced binary tree

## Problem statement

Given a **binary tree**, determine if it is **height-balanced**.

A height-balanced binary tree is defined as:

A binary tree in which the left and right subtrees of every node differ in height by no more than 1.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
int check(TreeNode* root, bool &res) {
    if(root == NULL) return 0;
    int lh = check(root->left, res);
    int rh = check(root->right, res);
    if(abs(lh-rh) > 1) res = false;
    return 1 + max(lh, rh);
}
bool isBalanced(TreeNode* root) {
    bool res = true;
    check(root, res);
    return res;
}
```
