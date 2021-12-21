# Check for balanced parentheses

## Problem statement

Given a string s containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

## Approach 1 (Stack)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
bool isValid(string s) {
    stack<char> st;
    for(char ch:s) {
        if(ch=='(' || ch=='{' || ch=='[')
            st.push(ch);
        else if(!st.empty() && ((ch==')' && st.top()=='(') || (ch==']' && st.top()=='[') || (ch=='}' && st.top()=='{')))
            st.pop();
        else
            return false;
    }
    return st.empty() ? true : false;
}
```

## Approach 2 (Without stack)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
bool isValid(string s) {
    int i=-1;
    for(char ch:s) {
        if(ch == '(' || ch == '{' || ch == '[')
            s[++i] = ch;
        else if(i>-1 && ((ch=='}'&&s[i]=='{') || (ch==')'&&s[i]=='(') || (ch==']'&&s[i]=='[')))
            i--;
        else
            return false;
    }
    return i==-1;
}
```
