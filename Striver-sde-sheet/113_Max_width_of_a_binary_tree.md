# Maximum width of a binary tree

## Problem statement

Given the `root` of a binary tree, return the **maximum width** of the given tree.

The **maximum width** of a tree is the maximum width **among all levels**.

The **width** of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes that would be present in a complete binary tree extending down to that level are also counted into the length calculation.

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int widthOfBinaryTree(TreeNode* root) {
    long res = 0;
    queue<pair<TreeNode*, long>> q;
    q.push({root, 0});
    while(!q.empty()) {
        long left = q.front().second;
        int sz = q.size();
        while(sz--) {
            TreeNode* node = q.front().first;
            long curr = q.front().second;
            q.pop();
            if(node -> left)
                q.push({node->left, 2*curr+1-left});
            if(node -> right)
                q.push({node->right, 2*curr+2-left});
            res = max(res, curr - left + 1);
        }
    }
    return res;
}
```
