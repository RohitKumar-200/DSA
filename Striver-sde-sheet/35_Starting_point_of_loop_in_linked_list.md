# Find starting point of loop in linked list

## Problem statement

Given the `head` of a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (0-indexed). It is `-1` if there is no cycle. Note that pos is not passed as a parameter.

## Approach 1 (Hasing)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
ListNode *detectCycle(ListNode *head) {
    unordered_set<ListNode*> st;
    while(head != NULL) {
        if(st.find(head) != st.end())
            return head;
        st.insert(head);
        head = head->next;
    }
    return NULL;
}
```

## Approach 2 (Tortoise hare method)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode *detectCycle(ListNode *head) {
    if(head == NULL || head->next == NULL) return NULL;
    ListNode *slow = head, *fast = head;
    do {
        if(fast->next == NULL || fast->next->next == NULL)
            return NULL;
        slow = slow->next;
        fast = fast->next->next;
    } while(slow != fast);
    fast = head;
    while(slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```
