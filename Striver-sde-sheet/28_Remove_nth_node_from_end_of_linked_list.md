# Remove nth node from end of linked list

## Problem statement

Given the head of a linked list, remove the n<sup>th</sup> node from the end of the list and return its head.

## Approach 1 (Finding length)

Time complexity : O(2N)  
Space complexity : O(1)

```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode * temp = head;
    int len = 0;
    while(temp) {
        temp = temp -> next;
        len++;
    }
    n = len - n;
    if(n==0) return head -> next;
    temp = head;
    while(--n) temp = temp -> next;
    temp -> next = temp -> next -> next;
    return head;
}
```

## Approach 2 (Recursion)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* remove(ListNode* head, int &n) {
    if(head == NULL) return NULL;
    head->next = remove(head->next, n);
    if(--n == 0)
        return head->next;
    return head;
}
```

## Approach 3 (Two pointers)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0, head);
    ListNode* l = dummy;
    ListNode* r = dummy;
    while(n--)
        r = r->next;
    while(r->next != NULL) {
        l = l->next;
        r = r->next;
    }
    l->next = l->next->next;
    return dummy -> next;
}
```
