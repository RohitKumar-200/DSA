# Count distinct substrings

## Problem statement

Given a string `S`, you are supposed to return the number of distinct substrings(including empty substring) of the given string. You should implement the program using a trie.

**Note :**

A string ‘B’ is a substring of a string ‘A’ if ‘B’ that can be obtained by deletion of, several characters(possibly none) from the start of ‘A’ and several characters(possibly none) from the end of ‘A’.

Two strings ‘X’ and ‘Y’ are considered different if there is at least one index ‘i’ such that the character of ‘X’ at index ‘i’ is different from the character of ‘Y’ at index ‘i’(X[i]!=Y[i]).

## Solution

Time complexity : O(N^2)  
Space complexity : O(N^2)

```cpp
class TrieNode
{
public:
    TrieNode *links[26];

    TrieNode() {
        for (int i = 0; i < 26; i++)
            links[i] = NULL;
    }

    ~TrieNode() {
        for (int i = 0; i < 26; i++) {
            if (links[i] != NULL)
                delete links[i];
        }
    }
};

int countDistinctSubstrings(string &s) {
    TrieNode* root = new TrieNode();
    int res = 1, n = s.size();

    for(int i=0; i<n; i++) {
        TrieNode* temp = root;
        for(int j=i; j<n; j++) {
            int ind = s[j] - 'a';
            if(temp -> links[ind] == NULL) {
                temp -> links[ind] = new TrieNode();
                res ++;
            }
            temp = temp -> links[ind];
        }
    }

    delete root;
    return res;
}
```
