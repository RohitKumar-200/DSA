# Ceil in a BST

## Problem statement

You are given a **BST** (Binary search tree) with `N` number of nodes and a value `X`. Your task is to find the smallest value node of the BST which is greater than or equal to `X`.

## Solution

Time complexity : O(H)  
Space complexity : O(1)

```cpp
int findCeil(BinaryTreeNode<int> *node, int x){
    int res = -1;
	while(node != NULL) {
		if(x <= node->data) {
			res = node->data;
			node = node->left;
		} else {
			node = node->right;
		}
	}
	return res;
}
```
