# LRU Cache

## Problem statement

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the LRUCache class:

- `LRUCache(int capacity)` Initialize the LRU cache with positive size `capacity`.
- `int get(int key)` Return the value of the key if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, evict the least recently used key.

The functions **get** and **put** must each run in `O(1)` average time complexity.

## Approach 1 (Map + LinkedList)

Time complexity : O(1) for every action  
Space complexity : O(N)

```cpp
class LRUCache {
    struct Node {
        int key;
        int val;
        Node* left;
        Node* right;
        Node(int _key, int _val) {
            key = _key;
            val = _val;
        }
    };

    int cap;
    Node* head = new Node(-1, -1);
    Node* tail = new Node(-1, -1);
    unordered_map<int, Node*> mp;

    void touch(Node* temp) {
        temp -> left -> right = temp -> right;
        temp -> right -> left = temp -> left;
        temp -> left = head -> left;
        temp -> right = head;
        head -> left -> right = temp;
        head -> left = temp;
    }
public:
    LRUCache(int capacity) {
        cap = capacity;
        head -> left = tail;
        tail -> right = head;
    }

    int get(int key) {
        if(mp.find(key) != mp.end()) {
            Node* temp = mp[key];
            touch(temp);
            return temp -> val;
        }
        return -1;
    }

    void put(int key, int value) {
        if(mp.find(key) != mp.end()) {
            Node* temp = mp[key];
            temp -> val = value;
            touch(temp);
            return;
        }

        if(cap == 0) {
            Node* temp = tail -> right;
            temp -> right -> left = tail;
            tail -> right = temp -> right;
            mp.erase(temp -> key);
            delete temp;
            cap++;
        }

        Node* temp = new Node(key, value);
        temp -> left = head -> left;
        temp -> right = head;
        head -> left -> right = temp;
        head -> left = temp;
        mp[key] = head -> left;
        cap--;
    }
};
```

## Approach 2 (Map + List)

Same as above, but shorter code

Time complexity : O(1) for every action  
Space complexity : O(N)

```cpp
class LRUCache {
private:
    list<pair<int, int>> l;
    unordered_map<int, list<pair<int, int>>::iterator> mp;
    int cap;

    void touch(list<pair<int, int>>::iterator it) {
        int key = it->first;
        int value = it->second;
        l.erase(it);
        l.push_front({key, value});
        mp[key] = l.begin();
    }
public:
    LRUCache(int capacity) {
        cap = capacity;
    }

    int get(int key) {
        auto it = mp.find(key);
        if(it != mp.end()) {
            touch(it->second);
            return it->second->second;
        }
        return -1;
    }

    void put(int key, int value) {
        auto it = mp.find(key);
        if(it != mp.end()) {
            it->second->second = value;
            touch(it->second);
            return;
        }
        if(l.size() == cap) {
            mp.erase(l.back().first);
            l.pop_back();
        }
        l.push_front({key, value});
        mp[key]=l.begin();
    }
};
```
