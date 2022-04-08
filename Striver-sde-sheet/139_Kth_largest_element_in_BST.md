# Kth largest element in BST

## Problem statement

Given a Binary search tree. Your task is to complete the function which will return the **Kth largest element** without doing any modification in Binary Search Tree.

## Solution 1 (Using Kth smallest element)

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
int KthSmallest(Node* root, int k) {
    int res = -1;
    Node* curr = root;
    while(curr) {
        if(curr -> left == NULL) {
            if(--k == 0) res = curr->data;
            curr = curr->right;
        } else {
            Node* prev = curr->left;
            while(prev->right != NULL && prev->right != curr)
                prev = prev->right;
            if(prev->right == NULL) {
                prev->right = curr;
                curr = curr->left;
            } else {
                prev->right = NULL;
                if(--k == 0) res = curr->data;
                curr = curr->right;
            }
        }
    }
    return res;
}
int countNodes(Node* root) {
    if(root == NULL) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}
int kthLargest(Node *root, int k) {
    int nodes = countNodes(root);
    return KthSmallest(root, nodes-k+1);
}
```

## Solution 2 (Reverse Morris Inorder traversal)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int kthLargest(Node *root, int k) {
    int res = -1;
    Node* curr = root;
    while(curr) {
        if(curr -> right == NULL) {
            if(--k == 0) res = curr->data;
            curr = curr->left;
        } else {
            Node* prev = curr->right;
            while(prev->left != NULL && prev->left != curr)
                prev = prev->left;
            if(prev->left == NULL) {
                prev->left = curr;
                curr = curr->right;
            } else {
                prev->left = NULL;
                if(--k == 0) res = curr->data;
                curr = curr->left;
            }
        }
    }
    return res;
}
```
