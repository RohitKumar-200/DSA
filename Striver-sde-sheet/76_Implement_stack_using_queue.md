# Implement stack using queue

## Approach 1

Push : O(1)  
Pop : O(N)

```cpp
class MyStack {
    queue<int> q1;
    queue<int> q2;
    int stackTop;
public:
    MyStack() {
        stackTop = -1;
    }

    void push(int x) {
        q1.push(x);
        stackTop = x;
    }

    int pop() {
        int popped = stackTop;
        while(q1.size() > 1) {
            stackTop = q1.front();
            q2.push(q1.front());
            q1.pop();
        }
        q1.pop();
        swap(q1, q2);
        return popped;
    }

    int top() {
        return stackTop;
    }

    bool empty() {
        return q1.empty();
    }
};
```

## Approach 2

Push : O(N)  
Pop : O(1)

```cpp
class MyStack {
    queue<int> q1;
    queue<int> q2;
public:
    void push(int x) {
        q2.push(x);
        while(!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }
        swap(q1, q2);
    }

    int pop() {
        int popped = q1.front();
        q1.pop();
        return popped;
    }

    int top() {
        return q1.front();
    }

    bool empty() {
        return q1.empty();
    }
};
```

## Approach 3 (Using one queue)

Push : O(N)  
Pop : O(1)

```cpp
class MyStack {
    queue<int> q;
public:
    void push(int x) {
        int sz = q.size();
        q.push(x);
        while(sz--) {
            q.push(q.front());
            q.pop();
        }
    }

    int pop() {
        int popped = q.front();
        q.pop();
        return popped;
    }

    int top() {
        return q.front();
    }

    bool empty() {
        return q.empty();
    }
};
```
