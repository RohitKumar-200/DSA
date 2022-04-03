# Path to given node

## Problem statement

Given a Binary Tree `A` containing `N` nodes.

You need to find the path from `Root` to a given node `B`.

**NOTE:**

- No two nodes in the tree have same data values.
- You can assume that B is present in the tree A and a path always exists.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
bool getPath(TreeNode* A, int B, vector<int> &path) {
    if(A == NULL) return false;
    path.push_back(A->val);
    if(A->val == B) return true;
    if(getPath(A->left, B, path) || getPath(A->right, B, path))
        return true;
    path.pop_back();
    return false;
}
vector<int> Solution::solve(TreeNode* A, int B) {
    vector<int> path;
    getPath(A, B, path);
    return path;
}
```
