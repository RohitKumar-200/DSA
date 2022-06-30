# Number of Minimums on a Segment

## Problem statement

Now change the code of the segment tree so that, in addition to the minimum on a segment, it also counts the number of elements equal to the minimum.

The first line contains two integers n and m, the size of the array and the number of operations. The next line contains n numbers ai, the initial state of the array. The following lines contain the description of the operations. The description of each operation is as follows:

- 1 i v: set the element with index i to v.
- 2 l r: calculate the minimum and number of elements equal to minimum of elements with indices from l to r−1.

## Solution

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<pair<int, int>> t;
    void init(vector<int> &v, int x, int lx, int rx) {
        if(lx == rx) {
            t[x] = {v[lx], 1};
            return;
        }
        int m = lx + (rx-lx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        pair<int, int> p1 = t[2*x+1], p2 = t[2*x+2];
        if(p1.first == p2.first) t[x] = {p1.first, p1.second+p2.second};
        else if(p1.first < p2.first) t[x] = p1;
        else t[x] = p2;
    }
    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = {q, 1};
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        pair<int, int> p1 = t[2*x+1], p2 = t[2*x+2];
        if(p1.first == p2.first) t[x] = {p1.first, p1.second+p2.second};
        else if(p1.first < p2.first) t[x] = p1;
        else t[x] = p2;
    }
    pair<int, int> calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return {INT_MAX, 0};
        if(lx >= l && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        pair<int, int> p1 = calc(l, r, 2*x+1, lx, m);
        pair<int, int> p2 = calc(l, r, 2*x+2, m+1, rx);
        if(p1.first == p2.first) return {p1.first, p1.second+p2.second};
        else if(p1.first < p2.first) return p1;
        else return p2;
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, {INT_MAX, 0});
        sz = n;
    }
    void init(vector<int> &v) {
        init(v, 0, 0, sz-1);
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    pair<int, int> calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1);
    }
};

signed main() {
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
            pair<int, int> p = sg.calc(b, c-1);
            cout<<p.first<<' '<<p.second<<'\n';
        }
    }
}
```
