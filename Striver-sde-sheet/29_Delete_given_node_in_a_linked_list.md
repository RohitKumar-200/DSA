# Delete given node in a linked list

## Problem statement

Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

## Approach 1 (One iteration)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
void deleteNode(ListNode* node) {
    while(1) {
        node->val = node->next->val;
        if(node->next->next == NULL)
            break;
        node = node->next;
    }
    node->next = NULL;
}
```

## Approach 2 (Constant time)

Time complexity : O(1)  
Space complexity : O(1)

```cpp
void deleteNode(ListNode* node) {
    node -> val = node -> next -> val;
    node -> next = node -> next -> next;
}
```
