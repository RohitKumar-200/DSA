# Addition to Segment

## Problem statement

There is an array of n elements, initially filled with zeros. You need to write a data structure that processes two types of queries:

- add to the segment from l to r−1 the number v,
- find the current value of element i.

You may have heard that such requests can be made using the tree of segments with mass change operations (we will talk about it in the next lesson), but this problem can be solved using a regular segment tree.

## Solution

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<int> t;
    void update(int l, int r, int val, int x, int lx, int rx) {
        if(r < lx || l > rx) return;
        if(l <= lx && rx <= r) {
            t[x] += val;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(l, r, val, 2*x+1, lx, m);
        update(l, r, val, 2*x+2, m+1, rx);
    }
    int calc(int p, int x, int lx, int rx) {
        if(p < lx || p > rx) return 0;
        if(lx == rx) return t[x];
        int m = lx + (rx-lx)/2;
        return calc(p, 2*x+1, lx, m) + calc(p, 2*x+2, m+1, rx) + t[x];
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, 0);
        sz = n;
    }
    void update(int l, int r, int val) {
        update(l, r, val, 0, 0, sz-1);
    }
    int calc(int p) {
        return calc(p, 0, 0, sz-1);
    }
};

signed main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n, m;
    cin>>n>>m;
    SegTree sg(n);
    while(m--) {
        int a;
        cin>>a;
        if(a == 1) {
            int x, y, z;
            cin>>x>>y>>z;
            sg.update(x, y-1, z);
        } else {
            int p;
            cin>>p;
            cout<<sg.calc(p)<<'\n';
        }
    }
}
```
