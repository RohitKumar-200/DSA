# Diameter of Binary Tree

## Problem statement

Given the `root` of a binary tree, return the length of the **diameter** of the tree.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
int findMaxDiameter(TreeNode* root, int &diameter) {
    if(root == NULL) return 0;
    int l = findMaxDiameter(root->left, diameter);
    int r = findMaxDiameter(root->right, diameter);
    diameter = max(diameter, l+r);
    return 1 + max(l, r);
}
int diameterOfBinaryTree(TreeNode* root) {
    int diameter = 0;
    findMaxDiameter(root, diameter);
    return diameter;
}
```
