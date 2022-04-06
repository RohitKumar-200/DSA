# Convert Sorted Array to Binary Search Tree

## Problem statement

Given an integer array `nums` where the elements are sorted in **ascending order**, convert it to a **height-balanced** binary search tree.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
TreeNode* solve(int start, int end, vector<int> &nums) {
    if(start > end) return NULL;
    int mid = (start+end)/2;
    TreeNode* root = new TreeNode(nums[mid]);
    root -> left = solve(start, mid-1, nums);
    root -> right = solve(mid+1, end, nums);
    return root;
}
TreeNode* sortedArrayToBST(vector<int>& nums) {
    return solve(0, nums.size()-1, nums);
}
```
