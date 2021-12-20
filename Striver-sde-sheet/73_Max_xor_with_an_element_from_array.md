# Maximum Xor with an element from array

## Problem statement

You are given an array `nums` consisting of non-negative integers. You are also given a `queries` array, where `queries[i] = [xi, mi]`.

The answer to the i<sup>th</sup> query is the maximum bitwise `XOR` value of **x<sub>i</sub>** and any element of nums that does not exceed **m<sub>i</sub>**. In other words, the answer is `max(nums[j] XOR xi)` for all `j` such that `nums[j] <= mi`. If all elements in nums are larger than mi, then the answer is `-1`.

Return an integer array answer where `answer.length == queries.length` and `answer[i]` is the answer to the i<sup>th</sup> query.

## Approach 1

```cpp
class Trie {
    struct Node {
        Node* links[2];
        int minN[2] = {INT_MAX, INT_MAX};
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
            bool bit = num & (1<<i);
            if(temp -> links[bit] == NULL)
                temp -> links[bit] = new Node();
            temp -> minN[bit] = min(temp->minN[bit], num);
            temp = temp -> links[bit];
        }
    }
    int findMaxXor(int num, int m) {
        if(root->minN[0] > m && root->minN[1] > m) return -1;
        int res = 0;
        Node* temp = root;
        for(int i=30; i>=0; i--) {
            bool reqdBit = !(num & (1<<i));
            if(temp->links[reqdBit]!=NULL && temp->minN[reqdBit]<=m) {
                res |= (1<<i);
                temp = temp -> links[reqdBit];
            } else if(temp->links[!reqdBit]!=NULL && temp->minN[!reqdBit]<=m) {
                temp = temp -> links[!reqdBit];
            }
        }
        return res;
    }
};
vector<int> maximizeXor(vector<int>& nums, vector<vector<int>>& queries) {
    Trie* t = new Trie();
    for(auto it:nums)
        t -> insert(it);
    vector<int> res;
    for(auto it:queries)
        res.push_back(t->findMaxXor(it[0], it[1]));
    return res;
}
```

## Approach 2 (Offline queries)

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
vector<int> maximizeXor(vector<int>& nums, vector<vector<int>>& queries) {
    vector<vector<int>> offlineQueries;
    int i = 0, n = nums.size();
    for(auto it:queries)
        offlineQueries.push_back({it[1], it[0], i++});
    sort(offlineQueries.begin(), offlineQueries.end());
    sort(nums.begin(), nums.end());
    vector<int> res(queries.size());
    Trie t;
    i=0;
    for(auto it:offlineQueries) {
        while(i<n && nums[i]<=it[0])
            t.insert(nums[i++]);
        res[it[2]] = i!=0 ? t.findMaxXor(it[1]) : -1;
    }
    return res;
}
```
