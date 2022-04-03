# Vertical Order Traversal of a Binary Tree

## Problem statement

Given the root of a binary tree, calculate the **vertical order traversal** of the binary tree.

For each node at position `(row, col)`, its left and right children will be at positions `(row + 1, col - 1)` and `(row + 1, col + 1)` respectively. The root of the tree is at `(0, 0)`.

The vertical order traversal of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.

Return the **vertical order traversal** of the binary tree.

## Solution

Time complexity : O(N\*log(a)\*log(b))  
Space compelxity : O(N)

```cpp
vector<vector<int>> verticalTraversal(TreeNode* root) {
    map<int, map<int, multiset<int>>> mp;
    queue<pair<TreeNode*, pair<int, int>>> q;
    q.push({root, {0, 0}});
    while(!q.empty()) {
        TreeNode* node = q.front().first;
        pair<int, int> p = q.front().second;
        mp[p.first][p.second].insert(node->val);
        q.pop();
        if(node -> left)
            q.push({node->left, {p.first-1, p.second+1}});
        if(node -> right)
            q.push({node->right, {p.first+1, p.second+1}});
    }
    vector<vector<int>> res;
    for(auto p:mp) {
        vector<int> col;
        for(auto q:p.second) {
            col.insert(col.end(), q.second.begin(), q.second.end());
        }
        res.push_back(col);
    }
    return res;
}
```
