# Segment Tree for the Minimum

## Problem Statement

Now change the code of the segment tree so that the minimum on the segment is calculated instead of the sum.

The first line contains two integers n and m, the size of the array and the number of operations. The next line contains n numbers ai, the initial state of the array. The following lines contain the description of the operations. The description of each operation is as follows:

- 1 i v: set the element with index i to v.
- 2 l r: calculate the minimum of elements with indices from l to r−1.

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<int> t;
    void init(vector<int> &v, int x, int lx, int rx) {
        if(lx == rx) {
            t[x] = v[lx];
            return;
        }
        int m = lx + (rx-lx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        t[x] = min(t[2*x+1], t[2*x+2]);
    }
    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = q;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        t[x] = min(t[2*x+1], t[2*x+2]);
    }
    int calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return INT_MAX;
        if(lx >= l && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        return min(calc(l, r, 2*x+1, lx, m), calc(l, r, 2*x+2, m+1, rx));
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, INT_MAX);
        sz = n;
    }
    void init(vector<int> &v) {
        init(v, 0, 0, sz-1);
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    int calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n, m;
    cin>>n>>m;
    vector<int> v(n);
    for(int &i:v) cin>>i;
    SegTree sg(n);
    sg.init(v);
    while(m--) {
        int a, b, c;
        cin>>a>>b>>c;
        if(a == 1) {
            sg.update(b, c);
        } else {
            cout<<sg.calc(b, c-1)<<'\n';
        }
    }
}
```
