# Boundary traversal of binary tree

## Problem statement

Given a Binary Tree, find its Boundary Traversal. The traversal should be in the following order:

- **Left boundary nodes**: defined as the path from the root to the left-most node ie- the leaf node you could reach when you always travel preferring the left subtree over the right subtree.
- **Leaf nodes**: All the leaf nodes except for the ones that are part of left or right boundary.
- **Reverse right boundary nodes**: defined as the path from the right-most node to the root. The right-most node is the leaf node you could reach when you always travel preferring the right subtree over the left subtree. Exclude the root from this as it was already included in the traversal of left boundary nodes.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
bool isLeaf(Node* node) {
    return node->left == NULL && node->right == NULL;
}
void addLeftBoundary(Node* root, vector<int> &res) {
    Node* curr = root->left;
    if(curr == NULL) return;
    while(!isLeaf(curr)) {
        res.push_back(curr -> data);
        if(curr -> left) curr = curr->left;
        else if(curr -> right) curr = curr->right;
    }
}
void addRightBoundary(Node* root, vector<int> &res) {
    Node* curr = root->right;
    if(curr == NULL) return;
    int n = res.size();
    while(!isLeaf(curr)) {
        res.push_back(curr -> data);
        if(curr -> right) curr = curr->right;
        else if(curr -> left) curr = curr->left;
    }
    reverse(res.begin()+n, res.end());
}
void addLeaves(Node* root, vector<int> &res) {
    if(root == NULL) return;
    if(isLeaf(root))
        return res.push_back(root->data);
    addLeaves(root->left, res);
    addLeaves(root->right, res);
}
vector <int> boundary(Node *root) {
    vector<int> res;
    res.push_back(root->data);
    if(isLeaf(root))
        return res;
    addLeftBoundary(root, res);
    addLeaves(root, res);
    addRightBoundary(root, res);
    return res;
}
```
