# Search in a Binary Search Tree

## Problem statement

You are given the `root` of a binary search tree (BST) and an integer `val`.

Find the node in the BST that the node's value equals `val` and return the subtree rooted with that node. If such a node does not exist, return `NULL`.

## Solution 1 (Recursion)

Time complexity : O(H)  
Auxiliary space : O(H)

```cpp
TreeNode* searchBST(TreeNode* root, int val) {
    if(root == NULL) return NULL;
    if(root->val == val) return root;
    if(val <= root->val) return searchBST(root->left, val);
    return searchBST(root->right, val);
}
```

## Solution 2 (Iterative)

Time complexity : O(H)  
Space complexity : O(1)

```cpp
TreeNode* searchBST(TreeNode* root, int val) {
    while(root != NULL && root->val!=val) {
        root = val < root->val ? root->left : root->right;
    }
    return root;
}
```
