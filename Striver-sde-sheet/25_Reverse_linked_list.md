# Reverse Linked List

## Problem statement

Given the `head` of a singly linked list, reverse the list, and return the reversed list.

## Approach 1 (Recursion)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* reverseList(ListNode* head) {
    if(!head || !(head -> next))
        return head;
    ListNode* node = reverseList(head->next);
    head -> next -> next = head;
    head -> next = NULL;
    return node;
}
```

## Approach 2 (Iterative)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = NULL;
    while(head) {
        ListNode* next = head->next;
        head->next = prev;
        prev = head;
        head = next;
    }
    return prev;
}
```
