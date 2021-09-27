# Merge to sorted linked list

## Problem statement

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

## Approach 1 (Extra space)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode* temp = new ListNode();
    ListNode* dummy = temp;
    while(l1 != NULL && l2 != NULL) {
        if(l1->val <= l2->val) {
            temp -> next = new ListNode(l1->val);
            l1 = l1->next;
        } else {
            temp -> next = new ListNode(l2->val);
            l2 = l2->next;
        }
        temp = temp->next;
    }
    while(l1 != NULL) {
        temp -> next = new ListNode(l1->val);
        temp = temp->next;
        l1 = l1->next;
    }
    while(l2 != NULL) {
        temp -> next = new ListNode(l2->val);
        temp = temp->next;
        l2 = l2->next;
    }
    return dummy -> next;
}
```

## Approach 2 (Modify given linked lists to create single sorted list)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode* temp = new ListNode();
    ListNode* dummy = temp;
    while(l1 != NULL && l2 != NULL) {
        if(l1->val <= l2->val) {
            temp -> next = l1;
            l1 = l1->next;
        } else {
            temp -> next = l2;
            l2 = l2->next;
        }
        temp = temp->next;
    }
    temp -> next = l1? l1 : l2;
    return dummy -> next;
}
```

## Approach 3 (Another way for above approach)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if(l1 == NULL) return l2;
    if(l2 == NULL) return l1;
    if(l1->val > l2->val) swap(l1, l2);
    ListNode * head = l1;
    while(l1!=NULL && l2!=NULL) {
        ListNode * temp = NULL;
        while(l1!=NULL && l1->val <= l2->val) {
            temp = l1;
            l1 = l1->next;
        }
        temp -> next = l2;
        swap(l1, l2);
    }
    return head;
}
```
