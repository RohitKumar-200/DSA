# Word break (Print all ways)

## Problem statement

Given a string `s` and a dictionary of words `dict` of length `n`, add spaces in `s` to construct a **sentence** where each word is a valid dictionary word. Each dictionary word can be used **more than once**. Return all such possible sentences.

## Solution

Time complexity : O((N^2)\*n) where N = |s|  
Auxiliary space : O(N^2)

```cpp
void wordBreakUtil(string s, string currRes, vector<string> &res, vector<string> &dict) {
    int n = s.size();
    for(int i=1; i<=n; i++) {
        string prefix = s.substr(0, i);
        if(find(dict.begin(), dict.end(), prefix) != dict.end()) {
            if(i == n) {
                currRes += prefix;
                res.push_back(currRes);
                return;
            }
            wordBreakUtil(s.substr(i, n-i), currRes+prefix+" ", res, dict);
        }
    }
}
vector<string> wordBreak(int n, vector<string>& dict, string s) {
    vector<string> res;
    wordBreakUtil(s, "", res, dict);
    return res;
}
```
