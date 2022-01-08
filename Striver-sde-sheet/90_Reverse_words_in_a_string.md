# Reverse words in a string

## Problem statement

Given an input string `s`, reverse the order of the **words**.

A word is defined as a sequence of non-space characters. The words in `s` will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

## Approach 1 (Stack)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
string reverseWords(string s) {
    s += ' ';
    stack<string> st;
    string temp, res;
    int n = s.size(), start=-1, end=-1;
    for(int i=0; i<n; i++) {
        if(s[i] != ' ') temp += s[i];
        else {
            if(temp != "") st.push(temp);
            temp = "";
        }
    }
    while(!st.empty()) {
        res += st.top();
        st.pop();
        if(!st.empty())
            res += ' ';
    }
    return res;
}
```

## Approach 2

Time complexity : O(N)  
Space complexity : O(1)

```cpp
string reverseWords(string s) {
    int i=0, j=0, l, r, n=s.size();
    while(j<n && s[j]==' ') j++;
    while(j<n) {
        if(s[j] == ' ') {
            while(j+1<n && s[j+1]==' ')
                j++;
        }
        s[i++] = s[j++];
    }
    if(i-1<n && s[i-1]==' ') i--;
    s = s.substr(0, i);
    n = i, i=n-1, j=n-1;
    while(i >= -1) {
        if(i == -1 || s[i] == ' ') {
            l = i+1, r = j;
            while(l<r) swap(s[l++], s[r--]);
            j = i-1, i = j;
        } else i--;
    }
    reverse(s.begin(), s.end());
    return s;
}
```
