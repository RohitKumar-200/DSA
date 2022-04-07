# Construct Binary Search Tree from Preorder Traversal

## Problem statement

Given an array of integers `preorder`, which represents the **preorder traversal** of a BST (i.e., **binary search tree**), construct the tree and return its `root`.

## Solution 1 (Through preorder and inorder)

Time complexity : O(N\*log(N) + O(N))  
Space complexity : O(N)  
Auxiliary space : O(N)

```cpp
TreeNode* buildTree(int preStart, int inStart, int inEnd, vector<int> &preorder, vector<int> &inorder){
    if(preStart > preorder.size()-1 || inStart > inEnd)
        return NULL;
    TreeNode *root = new TreeNode(preorder[preStart]);
    int i;
    for(i=inStart; i<=inEnd; i++) {
        if(inorder[i] == root->val)
            break;
    }
    root->left = buildTree(preStart+1, inStart, i-1, preorder, inorder);
    root->right = buildTree(preStart+1+(i-inStart), i+1, inEnd, preorder, inorder);
    return root;
}
TreeNode* bstFromPreorder(vector<int>& preorder) {
    vector<int> inorder(preorder.begin(), preorder.end());
    sort(inorder.begin(), inorder.end());
    return buildTree(0, 0, inorder.size()-1, preorder, inorder);
}
```

## Solution 2 (Upper and lower limit in preorder)

Time complexity : O(N)  
Space complexity : O(1)  
Auxiliary space : O(N)

```cpp
TreeNode* createBST(int i, int j, vector<int> &preorder) {
    if(i > j) return NULL;
    if(i == j) return new TreeNode(preorder[i]);
    int left_start = i+1;
    int right_start = i;
    while(right_start < preorder.size() && preorder[right_start] <= preorder[i])
        right_start++;
    int left_end = right_start -1;
    int right_end = j;
    TreeNode* root = new TreeNode(preorder[i]);
    root->left = createBST(left_start, left_end, preorder);
    root->right = createBST(right_start, right_end, preorder);
    return root;
}
TreeNode* bstFromPreorder(vector<int>& preorder) {
    return createBST(0, preorder.size()-1, preorder);
}
```

## Solution 3 (Using upper bound in preorder)

Time complexity : O(N)  
Space complexity : O(1)  
Auxiliary space : O(N)

```cpp
TreeNode* createBST(int &curr, int ub, vector<int> &preorder) {
    if(curr == preorder.size() || preorder[curr] > ub) return NULL;
    TreeNode* root = new TreeNode(preorder[curr]);
    curr++;
    root->left = createBST(curr, root->val, preorder);
    root->right = createBST(curr, ub, preorder);
    return root;
}
TreeNode* bstFromPreorder(vector<int>& preorder) {
    int curr = 0;
    return createBST(curr, INT_MAX, preorder);
}
```
