# Segment Tree for the sum

## Problem statement

The first line contains two integers n and m, the size of the array and the number of operations. The next line contains n numbers ai, the initial state of the array.  
The following lines contain the description of the operations. The description of each operation is as follows:

- 1 i v: set the element with index i to v.
- 2 l r: calculate the sum of elements with indices from l to r−1.

## Solution

Time Complexity : O(log(N))

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<int> v;
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz *= 2;
        v.resize(2*sz, 0LL);
        sz=n;
    }

    void build(vector<int> &a, int x, int lx, int rx) {
        if(lx == rx) {
            v[x] = a[lx];
            return;
        }
        int m = (lx + rx) / 2;
        build(a, 2*x+1, lx, m);
        build(a, 2*x+2, m+1, rx);
        v[x] = v[2*x+1] + v[2*x+2];
    }
    void build(vector<int> &a) {
        build(a, 0, 0, sz-1);
    }

    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            v[x] = q;
            return;
        }
        int m = (lx + rx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        v[x] = v[2*x+1] + v[2*x+2];
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }

    int rangeSum(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return 0;
        if(lx >= l && rx <= r) return v[x];
        int m = (lx+rx)/2;
        return rangeSum(l, r, 2*x+1, lx, m) + rangeSum(l, r, 2*x+2, m+1, rx);
    }
    int rangeSum(int l, int r) {
        return rangeSum(l, r, 0, 0, sz-1);
    }
};

signed main() {
    int n, m;
    cin>>n>>m;
    vector<int> v(n);
    for(int &i:v) cin>>i;
    SegTree sg(n);
    sg.build(v);
    while(m--) {
        int t, p, q;
        cin>>t>>p>>q;
        if(t == 1) {
            sg.update(p, q);
        } else {
            cout<<sg.rangeSum(p, q-1)<<'\n';
        }
    }
}
```
