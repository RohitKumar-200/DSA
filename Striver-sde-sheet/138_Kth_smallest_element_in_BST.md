# Kth Smallest Element in a BST

## Problem statement

Given the `root` of a binary search tree, and an integer `k`, return the **kth smallest value** (1-indexed) of all the values of the nodes in the tree.

## Solution 1 (Inorder traversal)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int kthSmallest(TreeNode* root, int k) {
    stack<TreeNode*> st;
    TreeNode* curr = root;
    while(!st.empty() || curr != NULL) {
        while(curr != NULL) {
            st.push(curr);
            curr = curr -> left;
        }
        curr = st.top();
        st.pop();
        if(--k == 0) return curr->val;
        curr = curr->right;
    }
    return -1;
}
```

## Solution 2 (Morris traversal)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int kthSmallest(TreeNode* root, int k) {
    int res = -1;
    TreeNode* curr = root;
    while(curr != NULL) {
        if(curr -> left == NULL) {
            if(--k == 0) res = curr->val;
            curr = curr->right;
        } else {
            TreeNode* prev = curr -> left;
            while(prev->right != NULL && prev->right != curr) {
                prev = prev->right;
            }
            if(prev->right == NULL) {
                prev->right = curr;
                curr = curr->left;
            } else {
                prev->right = NULL;
                if(--k == 0) res = curr->val;
                curr = curr -> right;
            }
        }
    }
    return res;
}
```
