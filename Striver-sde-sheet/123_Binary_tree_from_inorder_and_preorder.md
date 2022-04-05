# Construct Binary Tree from Preorder and Inorder Traversal

## Problem statement

Given two integer arrays `preorder` and `inorder` where preorder is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
TreeNode* solve(int preStart, int inStart, int inEnd, vector<int> &preorder, vector<int> &inorder){
    if(preStart > preorder.size()-1 || inStart > inEnd)
        return NULL;
    TreeNode *root = new TreeNode(preorder[preStart]);
    int i;
    for(i=inStart; i<=inEnd; i++) {
        if(inorder[i] == root->val)
            break;
    }
    root->left = solve(preStart+1, inStart, i-1, preorder, inorder);
    root->right = solve(preStart+1+(i-inStart), i+1, inEnd, preorder, inorder);
    return root;
}
TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
    return solve(0, 0, inorder.size()-1, preorder, inorder);
}
```
