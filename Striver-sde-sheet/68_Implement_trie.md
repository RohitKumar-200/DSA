# Implement Trie (Prefix Tree)

## Problem statement

A trie (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if the string word is in the trie (i.e., was inserted before), and `false` otherwise.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

## Solution

```cpp
class Trie {
private:
    struct Node {
        Node *links[26];
        bool flag = false;
    };
    Node* root;

public:
    Trie() {
        root = new Node();
    }

    void insert(string word) {
        Node *temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                temp -> links[ind] = new Node();
            temp = temp -> links[ind];
        }
        temp -> flag = true;
    }

    bool search(string word) {
        Node *temp = root;
        for(char ch:word) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                return false;
            temp = temp -> links[ind];
        }
        return temp -> flag;
    }

    bool startsWith(string prefix) {
        Node *temp = root;
        for(char ch:prefix) {
            int ind = ch - 'a';
            if(temp -> links[ind] == NULL)
                return false;
            temp = temp -> links[ind];
        }
        return true;
    }
};
```
