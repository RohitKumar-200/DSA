# Populating Next Right Pointers in Each Node

## Problem statement

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children.

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
Node* connect(Node* root) {
    if(root == NULL) return NULL;
    queue<Node*> q;
    q.push(root);
    while(!q.empty()) {
        int sz = q.size();
        while(sz--) {
            Node* node = q.front();
            q.pop();
            node->next = sz ? q.front() : NULL;
            if(node->left) q.push(node->left);
            if(node->right) q.push(node->right);
        }
    }
    return root;
}
```
