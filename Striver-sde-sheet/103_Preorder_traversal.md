# Preorder Traversal

## Problem statement

Given the `root` of a binary tree, return the **preorder traversal** of its nodes' values.

## Solution 1 (Recursive)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    if(root == NULL) return vector<int>();
    vector<int> l = preorderTraversal(root->left);
    vector<int> r = preorderTraversal(root->right);
    vector<int> res;
    res.push_back(root->val);
    for(auto it:l) res.push_back(it);
    for(auto it:r) res.push_back(it);
    return res;
}
```

## Solution 2 (Iterative)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> st;
    TreeNode* curr = root;
    while(curr != NULL || !st.empty()) {
        while(curr != NULL) {
            res.push_back(curr->val);
            st.push(curr);
            curr = curr -> left;
        }
        curr = st.top();
        st.pop();
        curr = curr -> right;
    }
    return res;
}
```
