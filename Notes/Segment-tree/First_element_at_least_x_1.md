# First element at least X - 2

## Problem statement

In this task, you need to add to the segment tree the operation of finding for the given x and l the minimum index j such that `j≥l` and `a[j]≥x`.

The first line contains two integers n and m, the size of the array and the number of operations. The next line contains n numbers ai, the initial state of the array (0≤ai≤109). The following lines contain the description of the operations. The description of each operation is as follows:

- 1 i v: change the item with index i to v.
- 2 x l: find the minimum index j such that `j≥l` and `a[j]≥x`. If there is no such element, print −1. Indices start from 0.

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
        t[x] = max(t[2*x+1], t[2*x+2]);
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
        t[x] = max(t[2*x+1], t[2*x+2]);
    }
    int calc(int val, int l, int x, int lx, int rx) {
        if(lx == rx) {
            if(t[x] >= val && l <= rx) return lx;
            return -1;
        }
        int m = lx + (rx-lx)/2, res = -1;
        if(t[2*x+1] >= val && l <= m)
            res = calc(val, l, 2*x+1, lx, m);
        if(res == -1)
            res = calc(val, l, 2*x+2, m+1, rx);
        return res;
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, -1);
        sz = n;
    }
    void init(vector<int> &v) {
        init(v, 0, 0, sz-1);
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    int calc(int val, int l) {
        return calc(val, l, 0, 0, sz-1);
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
            cout<<sg.calc(b, c)<<'\n';
        }
    }
}
```
