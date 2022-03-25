# Count and Say

## Problem statement

The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:

- countAndSay(1) = "1"
- countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.

To determine how you "say" a digit string, split it into the minimal number of groups so that each group is a contiguous section all of the same character. Then for each group, say the number of characters, then say the character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.

Given a positive integer `n`, return the n<sup>th</sup> term of the count-and-say sequence.

## Solution

Time complexity : O(N)  
Auxiliary complexity : O(N)

```cpp
string countAndSay(int n) {
    if(n == 1) return "1";
    string s = countAndSay(n-1);
    string res;
    for(int i=0, n=s.size(); i<n; i++) {
        int c = 1;
        char ch = s[i];
        while(i<n-1 && s[i]==s[i+1])
            i++, c++;
        res += to_string(c) + ch;
    }
    return res;
}
```
