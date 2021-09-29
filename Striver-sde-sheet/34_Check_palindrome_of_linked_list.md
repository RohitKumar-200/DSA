# Check if linked list is palindrome or not

## Problem statement

Given the `head` of a singly linked list, return `true` if it is a palindrome.

## Approach 1 (Recursion with passing address as reference)

Time complexity : O(N)  
space complexity : O(1) (But uses implicit stack memory)

```cpp
bool compare(ListNode* &start, ListNode* end) {
    if(end == NULL) return true;
    if(compare(start, end->next) == false || start->val != end->val)
        return false;
    start = start->next;
    return true;
}
bool isPalindrome(ListNode* head) {
    return compare(head, head);
}
```

## Approach 2 (Extra space)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
bool isPalindrome(ListNode* head) {
    vector<int> v;
    ListNode* temp = head;
    while(temp) {
        v.push_back(temp->val);
        temp = temp->next;
    }
    for(int i=0, j=v.size()-1; i<j; i++, j--)
        if(v[i] != v[j])
            return false;
    return true;
}
```

## Approach 3 (Reversing second half)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
ListNode* reverseList(ListNode* node) {
    ListNode* prev = NULL;
    while(node) {
        ListNode* next = node -> next;
        node -> next = prev;
        prev = node;
        node = next;
    }
    return prev;
}
bool isPalindrome(ListNode* head) {
    if(head -> next == NULL) return true;
    ListNode *slow = head, *fast = head;
    while(fast->next != NULL && fast->next->next != NULL) {
        slow = slow -> next;
        fast = fast -> next -> next;
    }
    slow -> next = reverseList(slow -> next);
    slow = slow->next;
    ListNode* temp = head;
    while(slow) {
        if(temp->val != slow->val)
            return false;
        temp = temp -> next;
        slow = slow -> next;
    }
    return true;
}
```
