# Postorder Traversal

## Problem statement

Given the `root` of a binary tree, return the **postorder traversal** of its nodes' values.

## Solution 1 (Recursive)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
vector<int> postorderTraversal(TreeNode* root) {
    if(root == NULL) return vector<int>();
    vector<int> l = postorderTraversal(root->left);
    vector<int> r = postorderTraversal(root->right);
    vector<int> res;
    for(auto it:l) res.push_back(it);
    for(auto it:r) res.push_back(it);
    res.push_back(root->val);
    return res;
}
```

## Solution 2 (Iterative with 2 stacks)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> res;
    if(root == NULL) return res;
    stack<TreeNode*> st1, st2;
    st1.push(root);
    while(!st1.empty()) {
        TreeNode* curr = st1.top();
        st1.pop();
        st2.push(curr);
        if(curr->left) st1.push(curr->left);
        if(curr->right) st1.push(curr->right);
    }
    while(!st2.empty()) {
        res.push_back(st2.top()->val);
        st2.pop();
    }
    return res;
}
```

## Solution 3 (Iterative)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> st;
    TreeNode* curr = root;
    while(!st.empty() || curr != NULL) {
        while(curr != NULL) {
            st.push(curr);
            curr = curr -> left;
        }
        curr = st.top();
        if(curr -> right != NULL) {
            curr = curr -> right;
        } else {
            st.pop();
            res.push_back(curr -> val);
            while(!st.empty() && curr == st.top() -> right) {
                curr = st.top();
                st.pop();
                res.push_back(curr -> val);
            }
            curr = NULL;
        }
    }
    return res;
}
```
