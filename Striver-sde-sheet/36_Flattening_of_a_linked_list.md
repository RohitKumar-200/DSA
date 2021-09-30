# Flattening of a linked list

## Problem statement

Given a Linked List of size N, where every node represents a sub-linked-list and contains two pointers:

- a next pointer to the next node,
- a bottom pointer to a linked list where this node is head.

Each of the sub-linked-list is in sorted order.

Flatten the Link List such that all the nodes appear in a single level while maintaining the sorted order.

**Note:** The flattened list will be printed using the bottom pointer instead of next pointer.

## Solution

Time complexity : O(N\*M) [O(No. of nodes)]  
Space complexity : O(1)

```cpp
Node* mergeList(Node *l1, Node *l2) {
    Node * dummy = new Node(0);
    Node * temp = dummy;
    while(l1 != NULL && l2 != NULL) {
        if(l1 -> data <= l2 -> data) {
            temp -> bottom = l1;
            l1 = l1 -> bottom;
        } else {
            temp -> bottom = l2;
            l2 = l2 -> bottom;
        }
        temp = temp -> bottom;
    }
    temp -> bottom = l1==NULL ? l2 : l1;
    return dummy -> bottom;
}

Node *flatten(Node *root)
{
   if(root == NULL || root->next == NULL) return root;
   Node * right = flatten(root -> next);
   root -> next = NULL;
   return mergeList(root, right);
}
```
