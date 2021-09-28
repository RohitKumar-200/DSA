# Intersection of two linked list

## Problem statement

Given the heads of two singly linked-lists `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return `null`.

## Approach 1 (Brute force)

Time complexity : O(N\*M)  
Space complexity : O(1)

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode* temp1 = headA;
    while(temp1) {
        ListNode* temp2 = headB;
        while(temp2) {
            if(temp1 == temp2)
                return temp1;
            temp2 = temp2->next;
        }
        temp1 = temp1->next;
    }
    return NULL;
}
```

## Approach 2 (Hashing)

Time complexity : O(N+M)  
Space complexity : O(N)

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode* temp = headA;
    unordered_set<ListNode*> hash;
    while(temp) {
        hash.insert(temp);
        temp = temp->next;
    }
    temp = headB;
    while(temp) {
        if(hash.find(temp) != hash.end())
            return temp;
        temp = temp->next;
    }
    return NULL;
}
```

## Approach 3 (Finding gap)

Time complexity : O(2N) (Assuming N>M)  
Space complexity : O(1)

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    int na=0, nb=0;
    ListNode* temp1 = headA;
    ListNode* temp2 = headB;
    while(temp1 || temp2) {
        if(temp1) {
            temp1 = temp1->next;
            na++;
        }
        if(temp2) {
            temp2 = temp2->next;
            nb++;
        }
    }
    int gap = na-nb;
    temp1 = headA, temp2 = headB;
    while(gap<0) {
        temp2 = temp2->next;
        gap++;
    }
    while(gap>0) {
        temp1 = temp1->next;
        gap--;
    }
    while(temp1 && temp2 && temp1 != temp2) {
        temp1 = temp1->next;
        temp2 = temp2->next;
    }
    return temp1;
}
```

## Approach 4 (2 Iteration, better code for above approach)

Time complexity : O(2N)  
Space complexity : O(1)

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    if(headA==NULL || headB==NULL) return NULL;
    ListNode* a = headA;
    ListNode* b = headB;
    while(a != b) {
        a = a==NULL? headB : a->next;
        b = b==NULL? headA : b->next;
    }
    return a;
}
```
