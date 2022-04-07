# Inorder Predecessor and Successor of a given key in BST

## Problem statement

There is BST given with root node with `key` part as integer only. You need to find the **inorder successor and predecessor** of a given key. In case, if the either of predecessor or successor is not found return `NULL`.

## Solution

Time complexity : O(H)  
Space complexity : O(1)

```cpp
Node* successor(Node* root, int key) {
    Node* suc = NULL;
    while(root != NULL) {
        if(root->key > key) {
            suc = root;
            root = root->left;
        } else {
            root = root->right;
        }
    }
    return suc;
}

Node* predecessor(Node* root, int key) {
    Node* pre = NULL;
    while(root != NULL) {
        if(root->key < key) {
            pre = root;
            root = root->right;
        } else {
            root = root->left;
        }
    }
    return pre;
}

void findPreSuc(Node* root, Node*& pre, Node*& suc, int key) {
    pre = predecessor(root, key);
    suc = successor(root, key);
}
```
