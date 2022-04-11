# Largest BST in a Binary tree

## Problem statement

Given a binary tree. Find the size of its **largest subtree that is a Binary Search Tree**.
**Note:** Here Size is equal to the number of nodes in the subtree.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
vector<int> solve(Node *root) {
    if(root == NULL) return {0, INT_MAX, INT_MIN};
    vector<int> l = solve(root -> left);
    vector<int> r = solve(root -> right);
    if(l[2] < root->data && root->data < r[1]) {
        return {l[0]+r[0]+1, min(root->data, l[1]), max(root->data, r[2])};
    }
    return {max(l[0], r[0]), INT_MIN, INT_MAX};
}
int largestBst(Node *root) {
	return solve(root)[0];
}
```
