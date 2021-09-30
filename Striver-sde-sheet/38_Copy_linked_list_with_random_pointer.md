# Copy linked list with random pointer

## Problem statement

A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.

Construct a deep copy of the list. The deep copy should consist of exactly n brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

## Approach 1 (Hash)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
Node* copyRandomList(Node* head) {
    map<Node*, Node*> hash;
    Node* temp = head;
    while(temp) {
        hash[temp] = new Node(temp->val);
        temp = temp -> next;
    }
    temp = head;
    while(temp) {
        hash[temp] -> next = temp -> next ? hash[temp->next] : NULL;
        hash[temp] -> random = temp -> random ? hash[temp->random] : NULL;
        temp = temp -> next;
    }
    return hash[head];
}
```

## Approach 2 (Altering given linked list)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
Node* copyRandomList(Node* head) {
    if(head == NULL) return head;
    Node* iter = head;
    while(iter != NULL) {
        Node* temp = new Node(iter->val);
        temp->next = iter->next;
        iter->next = temp;
        iter = temp->next;
    }
    iter = head;
    while(iter != NULL) {
        if(iter->random != NULL)
            iter->next->random = iter->random->next;
        iter = iter->next->next;
    }
    iter = head;
    Node* copyIter = head->next;
    Node* copyHead = head->next;
    while(iter->next->next != NULL) {
        iter->next = iter->next->next;
        copyIter->next = copyIter->next->next;
        iter = iter->next;
        copyIter = copyIter->next;
    }
    iter->next = NULL;
    return copyHead;
}
```
