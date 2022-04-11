# Flatten Binary Tree to Linked List

## Problem statement

Given the `root` of a binary tree, flatten the tree into a **linked list**:

- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a **pre-order traversal** of the binary tree.

## Solution

Time complexity : O(N)  
Space complexity : O(1)

```cpp
void flatten(TreeNode* root) {
    if(root == NULL) return;
    TreeNode* curr = root;
    while(curr) {
        if(curr -> left != NULL) {
            TreeNode* prev = curr -> left;
            while(prev->right)
                prev = prev->right;
            prev -> right = curr -> right;
            curr -> right = curr -> left;
            curr -> left = NULL;
        }
        curr = curr -> right;
    }
}
```
