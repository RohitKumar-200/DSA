# Repeated String Match

## Problem statement

Given two strings `a` and `b`, return the minimum number of times you should repeat string `a` so that string `b` is a substring of it. If it is impossible for `b​​​​​​` to be a substring of `a` after repeating it, return `-1`.

**Note:** string `"abc"` repeated 0 times is `""`, repeated 1 time is `"abc"` and repeated 2 times is `"abcabc"`.

## Solution (Rabin Karp)

Time complexity : O(N) (Worst = (N\*M))  
Space complexity : O(1)

```cpp
class Solution {
    int mod = 1e9+7;
    long long power(long long x, long long y) {
        long long res = 1;
        while(y>0) {
            if(y&1) {
                res = (res*x)%mod;
                y--;
            } else {
                x = (x*x)%mod;
                y /= 2;
            }
        }
        return res;
    }
    long long rabinHash(string s) {
        long long res = 0;
        for(char &ch:s) {
            res = res*10 + (ch-'a');
            res %= mod;
        }
        return res%mod;
    }
    bool stringMatch(int i, string& a, string& b) {
        int j = 0;
        while(j < b.size())
            if(a[i++] != b[j++])
                return false;
        return true;
    }
public:
    int repeatedStringMatch(string a, string b) {
        int lenA = a.size(), lenB = b.size();
        int repeat = b.size() / a.size() + 2;
        string temp = "";
        for(int i=0; i<repeat; i++)
            temp += a;
        a = temp;

        long long bHash = rabinHash(b);
        long long currHash = rabinHash(a.substr(0, lenB));

        if(currHash == bHash && stringMatch(0, a, b)) {
            if(repeat == 2) return 1; // lenB > lenA
            return lenB%lenA==0 ? lenB/lenA : lenB/lenA+1;
        }

        for(int i=lenB; i<a.size(); i++) {
            currHash -= (power(10, lenB-1) * (a[i-lenB] - 'a'))%mod;
            currHash = (currHash*10 + (a[i] - 'a'))%mod;
            currHash %= mod;
            if(currHash == bHash && stringMatch(i-lenB+1, a, b)) {
                int len = i+1;
                return len%lenA==0 ? len/lenA : len/lenA+1;
            }
        }
        return -1;
    }
};
```
