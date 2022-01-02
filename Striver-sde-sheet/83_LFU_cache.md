# LFU Cache (Least Frequently Used)

## Problem satement

Design and implement a data structure for a **Least Frequently Used (LFU)** cache.

Implement the **LFUCache** class:

- `LFUCache(int capacity)` Initializes the object with the `capacity` of the data structure.
- `int get(int key)` Gets the value of the `key` if the `key` exists in the cache. Otherwise, returns `-1`.
- `void put(int key, int value)` Update the value of the `key` if present, or inserts the `key` if not already present. When the cache reaches its `capacity`, it should invalidate and remove the **least frequently used** key before inserting a new item. For this problem, when there is a **tie** (i.e., two or more keys with the same frequency), the **least recently used** `key` would be invalidated.

## Solution

Time complexity : O(1) for every action  
Space complexity : O(N)

```cpp
struct Node {
    int key, val, freq;
    Node* next = NULL;
    Node* prev = NULL;
    Node(int _key, int _val) {
        key = _key;
        val = _val;
        freq = 1;
    }
};

struct List {
    Node* head;
    Node* tail;
    int size;
    List() {
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head -> next = tail;
        tail -> prev = head;
        size = 0;
    }
    void addFront(Node* node) {
        node->next = head->next;
        node->prev = head;
        head->next->prev = node;
        head->next = node;
        size++;
    }
    void removeNode(Node* node) {
        node->prev->next = node->next;
        node->next->prev = node->prev;
        size--;
    }
};

class LFUCache {
    unordered_map<int, Node*> keyNode;
    unordered_map<int, List*> freqList;
    int minFreq, sz, cap;

    void touch(Node* node) {
        int freq = node->freq;
        freqList[freq] -> removeNode(node);
        if(freq == minFreq && freqList[freq] -> size == 0)
            minFreq++;
        freq++;
        node->freq++;
        if(freqList.find(freq) == freqList.end())
            freqList[freq] = new List();
        freqList[freq] -> addFront(node);
    }
public:
    LFUCache(int capacity) {
        cap = capacity;
        minFreq = 0;
        sz = 0;
        freqList[1] = new List();
    }

    int get(int key) {
        if(keyNode.find(key) != keyNode.end()) {
            touch(keyNode[key]);
            return keyNode[key]->val;
        }
        return -1;
    }

    void put(int key, int value) {
        if(cap == 0) return;
        if(keyNode.find(key) != keyNode.end()) {
            keyNode[key] -> val = value;
            touch(keyNode[key]);
            return;
        }
        if(sz == cap) {
            Node* temp = freqList[minFreq]->tail->prev;
            freqList[minFreq] -> removeNode(temp);
            keyNode.erase(temp -> key);
            delete temp;
            sz--;
        }
        Node* temp = new Node(key, value);
        freqList[1] -> addFront(temp);
        keyNode[key] = temp;
        minFreq = 1;
        sz++;
    }
};
```
