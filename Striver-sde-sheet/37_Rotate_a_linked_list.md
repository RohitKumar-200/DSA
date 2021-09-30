# Rotate a linked list

## Problem statement

Given the `head` of a linked list, rotate the list to the right by `k` places.

## Approach 1 (Brute force)

Time complexity : O(N\*K)  
Space complexity : O(1)

```cpp
ListNode* rotateRight(ListNode* head, int k) {
    if(head == NULL || head->next == NULL || k==0) return head;
    while(k--) {
        ListNode* temp = head;
        while(temp -> next -> next != NULL)
            temp = temp -> next;
        temp -> next -> next = head;
        head = temp -> next;
        temp -> next = NULL;
    }
    return head;
}
```

## Approach 2 (Linear solution)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* rotateRight(ListNode* head, int k) {
    if(head == NULL || k==0) return head;
    int n = 1;
    ListNode* temp = head;
    while(temp -> next != NULL) {
        temp = temp -> next;
        n++;
    }
    temp -> next = head;
    temp = head;
    k%=n;
    for(int i=1; i<n-k; i++)
        temp = temp -> next;
    head = temp -> next;
    temp -> next = NULL;
    return head;
}
```
