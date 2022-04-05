# Invert a binary tree

## Problem statement

Given a Binary Tree, convert it into its mirror.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
void mirror(Node* node) {
    if(node == NULL) return;
    swap(node->left, node->right);
    mirror(node->left);
    mirror(node->right);
}
```
