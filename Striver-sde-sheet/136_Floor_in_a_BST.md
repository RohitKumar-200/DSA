# Floor in BST

## Problem statement

You are given a **BST** (Binary search tree) with `N` number of nodes and a value `X`. Your task is to find the greatest value node of the BST which is smaller than or equal to `X`.

## Solution

Time complexity : O(H)  
Space complexity : O(1)

```cpp
int floorInBST(TreeNode<int> * root, int x) {
    int res = -1;
	while(root != NULL) {
		if(x >= root->val) {
			res = root->val;
			root = root->right;
		} else {
			root = root->left;
		}
	}
	return res;
}
```
