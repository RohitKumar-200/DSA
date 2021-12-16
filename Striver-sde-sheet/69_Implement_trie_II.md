# Implement Trie II (Prefix tree)

## Problem statement

1. Trie(): Initialize the object of this “TRIE” data structure.

2. insert(“WORD”): Insert the string “WORD” into this “TRIE” data structure.

3. countWordsEqualTo(“WORD”): Return how many times this “WORD” is present in this “TRIE”.

4. countWordsStartingWith(“PREFIX”): Return how many words are there in this “TRIE” that have the string “PREFIX” as a prefix.

5. erase(“WORD”): Delete this string “WORD” from the “TRIE”.

**Note:**

1. If erase(“WORD”) function is called then it is guaranteed that the “WORD” is present in the “TRIE”.
2. If you are going to use variables with dynamic memory allocation then you need to release the memory associated with them at the end of your solution.

## Solution

Time complexity : O(N\*M) (Word length \* No. of words)  
Space complexity : O(N\*M)

```cpp
class Trie {
	struct Node {
        Node * links[26];
        int cntEndWith = 0;
        int cntPrefix = 0;
    };
    Node *root;

public:

    Trie() {
        root = new Node();
    }

    void insert(string &word) {
        Node *temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                temp -> links[ind] = new Node();
            temp = temp -> links[ind];
            temp -> cntPrefix++;
        }
        temp -> cntEndWith++;
    }

    int countWordsEqualTo(string &word) {
        Node *temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                return 0;
            temp = temp -> links[ind];
        }
        return temp -> cntEndWith;
    }

    int countWordsStartingWith(string &word) {
        Node *temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                return 0;
            temp = temp -> links[ind];
        }
        return temp -> cntPrefix;
    }

    void erase(string &word) {
        Node *temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            temp = temp -> links[ind];
            temp -> cntPrefix--;
        }
        temp -> cntEndWith--;
    }
};
```
