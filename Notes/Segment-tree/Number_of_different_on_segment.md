# Number of Different on Segment

## Problem statement

Given an array a, consisting of small integers (1≤ai≤40). You need to build a data structure that processes two types of queries:

1. find the number of different elements on a segment,
2. change the element of the array.

## Solution

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<vector<int>> t;
    vector<int> merge(vector<int> a, vector<int> b) {
        int i=0, j=0, n=a.size(), m=b.size();
        vector<int> res;
        while(i<n && j<m) {
            if(a[i] == b[j]) {
                res.push_back(a[i]);
                i++, j++;
            } else if(a[i] < b[j]) {
                res.push_back(a[i]);
                i++;
            } else {
                res.push_back(b[j]);
                j++;
            }
        }
        while(i<n) res.push_back(a[i++]);
        while(j<m) res.push_back(b[j++]);
        return res;
    }
    void init(vector<int> &v, int x, int lx, int rx) {
        if(lx == rx) {
            t[x] = {v[lx]};
            return;
        }
        int m = lx + (rx-lx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        t[x] = merge(t[2*x+1], t[2*x+2]);
    }
    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = {q};
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        t[x] = merge(t[2*x+1], t[2*x+2]);
    }
    vector<int> calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) {
            return {};
        }
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        return merge(calc(l, r, 2*x+1, lx, m), calc(l, r, 2*x+2, m+1, rx));
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.resize(2*sz);
        sz = n;
    }
    void init(vector<int> &v) {
        init(v, 0, 0, sz-1);
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    int calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1).size();
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
            cout<<sg.calc(b-1, c-1)<<'\n';
        } else {
            sg.update(b-1, c);
        }
    }
}
```
