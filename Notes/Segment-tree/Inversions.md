# Inversions

## Problem Statement

Given a permutation pi of `n` elements, find for each i the number of j such that `j<i` and `pj>pi`.

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<int> t;
    void update(int p, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = 1;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, 2*x+1, lx, m);
        update(p, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    int calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return 0;
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        int res = 0;
        res += calc(l, r, 2*x+1, lx, m);
        res += calc(l, r, 2*x+2, m+1, rx);
        return res;
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, 0);
        sz = n;
    }
    void update(int p) {
        update(p, 0, 0, sz-1);
    }
    int calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n;
    cin>>n;
    vector<int> v(n);
    for(int &i:v) cin>>i, i--;
    SegTree sg(n);
    for(int i=0; i<n; i++) {
        cout<<sg.calc(v[i], n-1)<<' ';
        sg.update(v[i]);
    }
}
```
