# Serialize and Deserialize Binary Tree

## Problem statement

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Clarification:** The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
string serialize(TreeNode* root) {
    if(root == NULL) return "#";
    string res;
    queue<TreeNode*> q;
    q.push(root);
    while(!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        if(node != NULL) {
            res += " " + to_string(node->val);
            q.push(node->left);
            q.push(node->right);
        } else {
            res += " #";
        }
    }
    return res;
}
TreeNode* deserialize(string data) {
    if(data == "#") return NULL;
    int i=0, n=data.size(), num=0;
    stringstream ss(data);
    string str;
    ss>>str;
    TreeNode* root = new TreeNode(stoi(str));
    queue<TreeNode*> q;
    q.push(root);
    while(!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        ss>>str;
        if(str != "#") {
            node -> left = new TreeNode(stoi(str));
            q.push(node->left);
        }
        ss>>str;
        if(str != "#") {
            node -> right = new TreeNode(stoi(str));
            q.push(node->right);
        }
    }
    return root;
}
```
