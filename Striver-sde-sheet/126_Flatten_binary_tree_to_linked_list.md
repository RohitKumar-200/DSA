# Flatten Binary Tree to Linked List

## Problem statement

Given the `root` of a binary tree, flatten the tree into a **linked list**:

- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a **pre-order traversal** of the binary tree.

## Solution 1 (Implicit stack)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
class Solution {
    TreeNode* prev;
public:
    void flatten(TreeNode* root) {
        if(root == NULL) return;
        flatten(root->right);
        flatten(root->left);
        root->right = prev;
        root->left = NULL;
        prev = root;
    }
};
```

## Solution 2 (Explicit stack)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
void flatten(TreeNode* root) {
    if(root == NULL) return;
    stack<TreeNode*> st;
    st.push(root);
    while(!st.empty()) {
        TreeNode* curr = st.top();
        st.pop();
        if(curr->right) st.push(curr->right);
        if(curr->left) st.push(curr->left);
        if(!st.empty())
            curr->right = st.top();
        curr->left = NULL;
    }
}
```

## Solution 3 (Morris traversal)

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
