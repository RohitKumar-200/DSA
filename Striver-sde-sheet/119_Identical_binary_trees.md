# Identical binary trees

## Problem statement

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

## Solution

Time complexity : O(N)  
Auxiliary Space : O(N)

```cpp
bool isSameTree(TreeNode* p, TreeNode* q) {
    if(!p || !q) return p==q;
    bool f = p->val == q->val;
    f = f && isSameTree(p->left, q->left);
    f = f && isSameTree(p->right, q->right);
    return f;
}
```
