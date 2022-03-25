# Minimum characters needed to be inserted in the beginning to make it palindromic

## Problem Statement

Given an string `A`. The only operation allowed is to insert characters in the beginning of the string.

Find how many minimum characters are needed to be inserted to make the string a palindrome string.

## Solution (Using LPS Array)

```cpp
vector<int> lps(string s) {
    int n = s.length();
    vector<int> lps(n, 0);
    for(int i=1, len=0; i<n;) {
        if(s[i] == s[len]) {
            lps[i] = len + 1;
            i++, len++;
        } else if(len > 0) {
            len = lps[len-1];
        } else {
            i++;
        }
    }
    return lps;
}
int Solution::solve(string A) {
    string B = A;
    reverse(B.begin(), B.end());
    string s = A + '$' + B;
    vector<int> lpsArr = lps(s);
    return A.size() - *lpsArr.rbegin();
}
```
