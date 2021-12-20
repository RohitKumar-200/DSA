# Implement queue using stack

## Approach 1

Push : O(N)  
Pop : O(1)

```cpp
class MyQueue {
    stack<int> s1;
    stack<int> s2;
public:
    void push(int x) {
        while(!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(x);
        while(!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
    }

    int pop() {
        int front = s1.top();
        s1.pop();
        return front;
    }

    int peek() {
        return s1.top();
    }

    bool empty() {
        return s1.empty();
    }
};
```

## Approach 2

Push : O(1)  
Pop : Amortized O(1)

```cpp
class MyQueue {
    stack<int> s1;
    stack<int> s2;
    int front;
public:
    void push(int x) {
        if(s1.empty())
            front = x;
        s1.push(x);
    }

    int pop() {
        if(s2.empty()) {
            while(!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }
        int popped = s2.top();
        s2.pop();
        return popped;
    }

    int peek() {
        if(!s2.empty())
            return s2.top();
        return front;
    }

    bool empty() {
        return s1.empty() && s2.empty();
    }
};
```
