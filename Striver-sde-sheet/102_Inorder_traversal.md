# Inorder Traversal

## Problem statement

Given the `root` of a binary tree, return the **inorder traversal** of its nodes' values.

## Solution 1 (Recursive)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    if(root == NULL) return vector<int>();
    vector<int> l = inorderTraversal(root->left);
    vector<int> r = inorderTraversal(root->right);
    vector<int> res;
    for(auto it:l) res.push_back(it);
    res.push_back(root->val);
    for(auto it:r) res.push_back(it);
    return res;
}
```

## Solution 2 (Iterative)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> st;
    TreeNode* curr = root;
    while(!st.empty() || curr != NULL) {
        while(curr != NULL) {
            st.push(curr);
            curr = curr -> left;
        }
        curr = st.top();
        st.pop();
        res.push_back(curr -> val);
        curr = curr -> right;
    }
    return res;
}
```
