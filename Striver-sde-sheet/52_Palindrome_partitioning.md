# Palindrome partitioning

## Problem statement

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

## Solution

Time complexity : O(N^3)  
Space complexity : O(N^2)

```cpp
bool isPalindrome(int i, int j, string &s) {
    while(i<j) if(s[i++] != s[j--]) return false;
    return true;
}
void dfs(int index, string &s, vector<string> &path, vector<vector<string>> &res) {
    if(index == s.size()) {
        res.push_back(path);
        return;
    }
    for(int i=index; i<s.size(); i++) {
        if(isPalindrome(index, i, s)) {
            path.push_back(s.substr(index, i-index+1));
            dfs(i+1, s, path, res);
            path.pop_back();
        }
    }
}
vector<vector<string>> partition(string s) {
    vector<vector<string>> res;
    vector<string> vs;
    dfs(0, s, vs, res);
    return res;
}
```
