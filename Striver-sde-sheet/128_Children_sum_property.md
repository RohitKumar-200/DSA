# Children sum property

## Problem statement

Given a binary tree of nodes `N`, you need to modify the value of its nodes, such that the tree holds the **Children sum property**.

A binary tree is said to follow the children sum property if, for every node of that tree, the value of that node is equal to the sum of the value(s) of all of its children nodes( left child and the right child).

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
void changeTree(BinaryTreeNode < int > * root) {
    if(root == NULL) return;
    int childSum = 0;
    if(root->left) childSum += root->left->data;
    if(root->right) childSum += root->right->data;
    if(childSum < root->data) {
        if(root->left) root->left->data = root->data;
        if(root->right) root->right->data = root->data;
    }
    changeTree(root->left);
    changeTree(root->right);
    childSum = 0;
    if(root->left) childSum += root->left->data;
    if(root->right) childSum += root->right->data;
    if(root->left || root->right)
        root->data = childSum;
}
```
