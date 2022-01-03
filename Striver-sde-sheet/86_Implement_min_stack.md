# Min Stack

## Problem statement

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

## Approach 1 (Two stacks)

Time complexity : O(1)  
Space complexity : O(2N)

```cpp
class MinStack {
    stack<int> st;
    stack<int> minSt;
public:
    MinStack() {
    }

    void push(int val) {
        st.push(val);
        if(minSt.empty() || val <= minSt.top())
            minSt.push(val);
    }

    void pop() {
        if(st.top() == minSt.top())
            minSt.pop();
        st.pop();
    }

    int top() {
        return st.top();
    }

    int getMin() {
        return minSt.top();
    }
};
```

## Approach 2 (Storing pair in stack)

Time complexity : O(1)  
Space complexity : O(2N)

```cpp
class MinStack {
    stack<pair<int, int>> st;
public:
    MinStack() {
    }

    void push(int val) {
        if(st.empty())
            st.push({val, val});
        else
            st.push({val, min(val, st.top().second)});
    }

    void pop() {
        st.pop();
    }

    int top() {
        return st.top().first;
    }

    int getMin() {
        return st.top().second;
    }
};
```

## Approach 3 (One stack)

Time complexity : O(1)  
Space complexity : O(N)

```cpp
class MinStack {
    stack<long long> st;
    long long mini = INT_MAX;
public:
    MinStack() {
    }

    void push(int val) {
        if(st.empty()) {
            st.push(val);
            mini = val;
        } else if(val < mini) {
            st.push(2LL*val - mini);
            mini = val;
        } else {
            st.push(val);
        }
    }

    void pop() {
        if(st.top() < mini) {
            mini = 2*mini - st.top();
        }
        st.pop();
    }

    int top() {
        if(st.top() < mini)
            return mini;
        return st.top();
    }

    int getMin() {
        return mini;
    }
};
```
