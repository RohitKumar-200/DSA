# Detect a cycle in linked list

## Problem statement

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, pos is used to denote the index of the node that tail's `next` pointer is connected to. Note that `pos` is not passed as a parameter.

Return `true` if there is a cycle in the linked list. Otherwise, return `false`.

## Solution

Time complexity : O(N)  
space complexity : O(1)

```cpp
bool hasCycle(ListNode *head) {
    ListNode* slow = head;
    ListNode* fast = head;
    do {
        if(fast==NULL || fast->next==NULL) return false;
        slow = slow -> next;
        fast = fast -> next -> next;
    } while(slow != fast);
    return true;
}
```
