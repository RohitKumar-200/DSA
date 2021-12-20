# Implement Stack using Array

## Problem statement

Implement a stack using an array

## Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

class Stack {
    int *arr;
    int ind;
public:
    Stack() {
        arr = new int[1000];
        ind = -1;
    }
    void push(int x) {
        arr[++ind] = x;
    }
    void pop() {
        arr[ind--];
    }
    int top() {
        return arr[ind];
    }
    int size() {
        return ind+1;
    }
    bool isEmpty() {
        return ind == -1;
    }
};

int main()
{
    Stack st;
    st.push(6);
    st.push(3);
    st.push(7);
    cout << "Top of stack is before deleting any element " << st.top() << endl;
    cout << "Size of stack before deleting any element " << st.size() << endl;
    st.pop();
    cout << "Size of stack after deleting an element " << st.size() << endl;
    cout << "Top of stack after deleting an element " << st.top() << endl;
    cout << "Current value returned by isEmpty function " << st.isEmpty() <<endl;
    st.pop();
    st.pop();
    cout << "Size of stack after deleting two element " << st.size() <<endl;
    cout << "Value returned by isEmpty when stack is empty " << st.isEmpty() <<endl;
    return 0;
}
```
