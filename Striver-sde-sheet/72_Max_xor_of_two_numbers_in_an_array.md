# Maximum XOR of two numbers in an array

## Problem statement

Given an integer array `nums`, return the maximum result of `nums[i] XOR nums[j]`, where `0 <= i <= j < n`.

## Solution

Time complexity : O(N\*M) (M = Average word length)

```cpp
class Trie {
    struct Node {
        Node* links[2];
    };
    Node* root;
public:
    Trie() {
        root = new Node();
    }
    void insert(int num) {
        int pow2 = 1<<30;
        Node* temp = root;
        for(int i=30; i>=0; i--) {
            bool bit = (num >> i) & 1;
            if(temp -> links[bit] == NULL)
                temp -> links[bit] = new Node();
            temp = temp -> links[bit];
        }
    }
    int findMaxXor(int num) {
        int res = 0;
        Node* temp = root;
        for(int i=30; i>=0; i--) {
            bool reqdBit = !((num >> i) & 1);
            if(temp -> links[reqdBit] != NULL) {
                res = res | (1<<i);
                temp = temp -> links[reqdBit];
            } else if(temp -> links[!reqdBit] != NULL) {
                temp = temp -> links[!reqdBit];
            }
        }
        return res;
    }
};
int findMaximumXOR(vector<int>& nums) {
    Trie* t = new Trie();
    for(auto it:nums)
        t -> insert(it);
    int res = 0;
    for(auto it:nums)
        res = max(res, t -> findMaxXor(it));
    return res;
}
```
