# Tree Traversals

## Problem statement

You have been given a Binary Tree of `N` nodes, where the nodes have integer values. Your task is to find the `ln-Order`, `Pre-Order`, and `Post-Order` traversals of the given **binary tree**.

## Solution

Time complexity : O(3N)  
Space complexity : O(3N)

```cpp
vector<vector<int>> getTreeTraversal(BinaryTreeNode<int> *root){
    vector<vector<int>> res;
    if(root == NULL) return res;
    stack<pair<BinaryTreeNode<int>*, int>> st;
    st.push({root, 1});
    vector<int> pre, in, post;
    while(!st.empty()) {
        BinaryTreeNode<int>* node = st.top().first;
        int x = st.top().second;
        st.pop();
        if(x == 1) {
            pre.push_back(node->data);
           	st.push({node, x+1});
            if(node->left)
            	st.push({node->left, 1});
        } else if(x == 2) {
            in.push_back(node->data);
            st.push({node, x+1});
            if(node->right)
            	st.push({node->right, 1});
        } else {
            post.push_back(node->data);
        }
    }
    res.push_back(in);
    res.push_back(pre);
    res.push_back(post);
    return res;
}
```