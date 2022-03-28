# Left View of Binary Tree

## Problem statement

Given a Binary Tree, print **Left view** of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side.

## Solution

Time complexity : O(N)  
Auxiliary space : O(H)

```cpp
void dfs(Node *root, int level, vector<int> &res) {
    if(root == NULL) return;
    if(res.size() == level) res.push_back(root->data);
    dfs(root->left, level+1, res);
    dfs(root->right, level+1, res);
}
vector<int> leftView(Node *root) {
   vector<int> res;
   dfs(root, 0, res);
   return res;
}
```
