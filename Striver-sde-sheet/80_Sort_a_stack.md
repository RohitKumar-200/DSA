# Sort a Stack

## Problem statement

Given a stack, the task is to sort it such that the top of the stack has the greatest element.

## Approach 1 (Recursion)

Time complexity : O(N^2)  
Auxiliary space : O(N)

```cpp
void insertInStack(stack<int> &st, int x) {
    if(st.empty() || st.top() <= x) {
        st.push(x);
        return;
    }
    int top = st.top();
    st.pop();
    insertInStack(st, x);
    st.push(top);
}
void sortStack(stack<int> &st) {
    if(st.empty()) return;
    int top = st.top();
    st.pop();
    sortStack(st);
    insertInStack(st, top);
}
void SortedStack :: sort() {
   sortStack(s);
}
```

## Approach 2 (Using 2 extra stacks)

Time complexity : O(N^2)  
Space complexity : O(N)

```cpp
void SortedStack :: sort() {
    stack<int> sRes, sTemp;
    while(!s.empty()) {
        int x = s.top();
        while(!sRes.empty() && sRes.top() > x) {
            sTemp.push(sRes.top());
            sRes.pop();
        }
        sRes.push(x);
        while(!sTemp.empty()) {
            sRes.push(sTemp.top());
            sTemp.pop();
        }
        s.pop();
    }
    s = sRes;
}
```
