# Inversions 2

## Problem Statement

This problem is the reversed version of the previous one. There was a permutation pi of n elements, for each i we wrote down the number ai, the number of j such that `j<i` and `pj>pi`. Restore the original permutation for the given ai.

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<int> t;
    void init(int x, int lx, int rx) {
        if(lx == rx) {
            t[x] = 1;
            return;
        }
        int m = lx + (rx-lx)/2;
        init(2*x+1, lx, m);
        init(2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    void update(int p, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = 0;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, 2*x+1, lx, m);
        update(p, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    int calc(int k, int x, int lx, int rx) {
        if(lx == rx) return lx;
        int m = lx + (rx-lx)/2;
        if(k < t[2*x+2])
            return calc(k, 2*x+2, m+1, rx);
        return calc(k-t[2*x+2], 2*x+1, lx, m);
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, 1);
        sz = n;
        init(0, 0, sz-1);
    }
    void update(int p) {
        update(p, 0, 0, sz-1);
    }
    int calc(int k) {
        return calc(k, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n;
    cin>>n;
    vector<int> v(n);
    for(int &i:v) cin>>i;
    SegTree sg(n);
    vector<int> res(n);
    for(int i=n-1; i>=0; i--) {
        res[i] = sg.calc(v[i]) + 1;
        sg.update(res[i] - 1);
    }
    for(int i:res) cout<<i<<' ';
}
```
