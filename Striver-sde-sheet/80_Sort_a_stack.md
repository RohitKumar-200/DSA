# Sort a Stack

## Approach 1 (Recursion)

Time complexity : O(N^2)  
Auxiliary space : O(N)

```cpp
#include <bits/stdc++.h>
using namespace std;

void insertInStack(stack<int> &st, int x) {
    if(st.empty() || st.top() >= x) {
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

void printStack(stack<int> st) {
    while(!st.empty()) {
        cout<<st.top()<<' ';
        st.pop();
    }
    cout<<endl;
}

int main()
{
    stack<int> st;
    st.push(3);
    st.push(1);
    st.push(7);
    st.push(9);
    st.push(5);
    st.push(0);
    cout<<"Stack before sorting"<<endl;
    printStack(st);
    sortStack(st);
    cout<<"Stack after sorting"<<endl;
    printStack(st);
    return 0;
}
```

## Approach 2 (Using 3 stacks)

Time complexity : O(N^2)  
Space complexity : O(N)

```cpp
#include <bits/stdc++.h>
using namespace std;

stack<int> sortStack(stack<int> st) {
    stack<int> sRes, sTemp;
    while(!st.empty()) {
        int x = st.top();
        while(!sRes.empty() && sRes.top() < x) {
            sTemp.push(sRes.top());
            sRes.pop();
        }
        sRes.push(x);
        while(!sTemp.empty()) {
            sRes.push(sTemp.top());
            sTemp.pop();
        }
        st.pop();
    }
    return sRes;
}

void printStack(stack<int> st) {
    while(!st.empty()) {
        cout<<st.top()<<' ';
        st.pop();
    }
    cout<<endl;
}

int main()
{
    stack<int> st;
    st.push(3);
    st.push(1);
    st.push(7);
    st.push(9);
    st.push(5);
    st.push(0);
    cout<<"Stack before sorting"<<endl;
    printStack(st);
    st = sortStack(st);
    cout<<"Stack after sorting"<<endl;
    printStack(st);
    return 0;
}
```
