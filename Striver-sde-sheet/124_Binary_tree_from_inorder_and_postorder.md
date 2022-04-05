# Construct Binary Tree from Inorder and Postorder Traversal

## Problem statement

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return the **binary tree**.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
TreeNode* solve(int inStart, int inEnd, int postIdx, vector<int> &inorder, vector<int> &postorder) {
    if(inStart > inEnd) return NULL;
    TreeNode* root = new TreeNode(postorder[postIdx]);
    int i;
    for(i=inStart; i<=inEnd; i++) {
        if(inorder[i] == root->val)
            break;
    }
    root->left = solve(inStart, i-1, postIdx-1-(inEnd-i), inorder, postorder);
    root->right = solve(i+1, inEnd, postIdx-1, inorder, postorder);
    return root;
}
TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
    return solve(0, inorder.size()-1, postorder.size()-1, inorder, postorder);
}
```
