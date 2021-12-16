# Longest string with all prefixes

## Problem statement

A string is called a complete string if every prefix of this string is also present in the array `A`. Ninja is challenged to find the longest complete string in the array `A`.If there are multiple strings with the same length, return the **lexicographically smallest** one and if no string exists, return "None".

## Solution

Time complexity : O(N\*M) (Word length \* No. of words)  
Space complexity : O(N\*M)

```cpp
class Trie {
private:
    struct Node {
        Node* links[26];
        bool end = false;
    };
    Node* root;
public:
    Trie() {
        root = new Node();
    }
    void insert(string word) {
        Node* temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                temp -> links[ind] = new Node();
            temp = temp -> links[ind];
        }
        temp -> end = true;
    }
    bool isCompleteString(string word) {
        Node* temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            temp = temp -> links[ind];
            if(!temp->end) return false;
        }
       	return true;
    }
};

string completeString(int n, vector<string> &a){
    Trie* t = new Trie();
    for(string s:a) t -> insert(s);
    string res = "";
    for(string s:a) {
        if(t -> isCompleteString(s)) {
            if(res == "" || s.size() > res.size() || (s.size() == res.size() && s < res))
                res = s;
        }
    }
    return res == "" ? "None" : res;
}
```
