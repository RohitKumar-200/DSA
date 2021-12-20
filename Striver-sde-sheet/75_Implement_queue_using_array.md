# Implement queue using an array

## Solution

```cpp
class Queue {
    int *arr;
    int start, end, currSize, maxSize;
public:
    Queue() {
        maxSize = 100;
        arr = new int[maxSize];
        start = end = -1;
    }
    Queue(int size) {
        maxSize = size;
        arr = new int[maxSize];
        start = end = -1;
    }
    void push(int newElement) {
        if(currSize == maxSize) {
            cout<<"Queue is full";
            return;
        }
        if(end == -1)
            start = end = 0;
        else
            end = (end + 1) % maxSize;
        arr[end] = newElement;
        cout << "The element pushed is " << newElement << endl;
        currSize++;
    }
    int pop() {
        if(start == -1) {
            cout<<"Queue is empty\nExiting...";
            exit(1);
        }
        int popped = arr[start];
        if(currSize == 1)
            start = end = -1;
        else
            start = (start + 1) % maxSize;
        currSize--;
        return popped;
    }
    int top() {
        if(start == -1) {
            cout<<"Queue is empty\nExiting...";
            exit(1);
        }
        return arr[start];
    }
    int size() {
        return currSize;
    }
};

int main()
{
    Queue q(6);
    q.push(4);
    q.push(14);
    q.push(24);
    q.push(34);
    cout << "The peek of the queue before deleting any element " << q.top() << endl;
    cout << "The size of the queue before deletion " << q.size() << endl;
    cout << "The first element to be deleted " << q.pop() << endl;
    cout << "The peek of the queue after deleting an element " << q.top() << endl;
    cout << "The size of the queue after deleting an element " << q.size() << endl;
    return 0;
}
```
