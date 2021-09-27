# Find middle of linked list

## Problem statement

Given the `head` of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return **the second middle** node.

## Approach 1 (Two iterations)

Time complexity : O(N+N/2) = O(N)  
Space complexity : O(1)

```cpp
ListNode* middleNode(ListNode* head) {
    int n=0;
    ListNode* temp = head;
    while(temp) {
        temp = temp->next;
        n++;
    }
    n = (n&1)? (n+1)/2 : n/2+1;
    temp = head;
    while(temp) {
        if(--n == 0)
            break;
        temp = temp->next;
    }
    return temp;
}
```

## Approach 2 (One iteration)

Time complexity : O(N/2) = O(N)  
Space complexity : O(1)

```cpp
ListNode* middleNode(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while(fast!=NULL && fast->next!=NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```
