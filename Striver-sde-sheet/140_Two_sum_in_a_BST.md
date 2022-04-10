# Two Sum IV - Input is a BST

## Problem statement

Given the `root` of a Binary Search Tree and a target number `k`, return `true` if there exist two elements in the BST such that their sum is equal to the given target.

## Solution 1

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> getInorder(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> st;
    TreeNode* curr = root;
    while(curr != NULL || !st.empty()) {
        while(curr != NULL) {
            st.push(curr);
            curr = curr->left;
        }
        curr = st.top();
        st.pop();
        res.push_back(curr->val);
        curr = curr->right;
    }
    return res;
}
bool findTarget(TreeNode* root, int k) {
    vector<int> inorder = getInorder(root);
    int i=0, j=inorder.size()-1;
    while(i<j) {
        int sum = inorder[i] + inorder[j];
        if(sum == k) return true;
        if(sum < k) i++;
        else j--;
    }
    return false;
}
```

## Solution 2

Time complexity : O(N)  
Space complexity : O(H)

```cpp
class BSTIterator {
    stack<TreeNode*> st;
    bool reverse;
    void pushAll(TreeNode* root) {
        while(root) {
            st.push(root);
            root = reverse ? root->right : root->left;
        }
    }
public:
    BSTIterator(TreeNode* root, bool _reverse) {
        reverse = _reverse;
        pushAll(root);
    }
    int next() {
        TreeNode* temp = st.top();
        st.pop();
        if(!reverse) pushAll(temp->right);
        else pushAll(temp->left);
        return temp->val;
    }
};

class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        BSTIterator l(root, false);
        BSTIterator r(root, true);
        int i = l.next(), j = r.next();
        while(i < j) {
            if(i + j == k) return true;
            if(i + j < k) i = l.next();
            else j = r.next();
        }
        return false;
    }
};
```
