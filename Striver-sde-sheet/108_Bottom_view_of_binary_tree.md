# Bottom View of Binary Tree

## Problem statement

Given a binary tree, print the **bottom view** from left to right.
A node is included in bottom view if it can be seen when we look at the tree from bottom.

## Solution

Time complexity : O(N\*log(N))  
Space complexity : O(N)

```cpp
vector <int> bottomView(Node *root) {
    map<int, int> mp;
    queue<pair<Node*, int>> q;
    q.push({root, 0});
    while(!q.empty()) {
        Node* node = q.front().first;
        int v = q.front().second;
        mp[v] = node->data;
        q.pop();
        if(node->left) q.push({node->left, v-1});
        if(node->right) q.push({node->right, v+1});
    }
    vector<int> res;
    for(auto it:mp) res.push_back(it.second);
    return res;
}
```
