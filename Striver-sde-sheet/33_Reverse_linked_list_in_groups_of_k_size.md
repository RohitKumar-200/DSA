# Reverse a linked list in groups of k size

## Problem statement

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

## Solution

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    if(head == NULL || k == 1) return head;

    ListNode* dummy = new ListNode();
    dummy -> next = head;

    ListNode *cur = dummy, *nex = dummy, *pre = dummy;
    int n=0;

    while(cur->next != NULL) {
        n++;
        cur = cur->next;
    }

    while(n>=k) {
        cur = pre->next;
        nex = cur->next;
        for(int i=1; i<k; i++) {
            cur -> next = nex -> next;
            nex -> next = pre -> next;
            pre -> next = nex;
            nex = cur -> next;
        }
        n -= k;
        pre = cur;
    }

    return dummy -> next;
}
```
