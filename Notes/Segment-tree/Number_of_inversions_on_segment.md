# Number of Inversions on Segment

## Problem statement

Given an array a, consisting of small integers (1≤ai≤40). You need to build a data structure that processes two types of queries:

1. find the number of inversions on a segment,
2. change the element of the array.

## Solution

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

struct item {
    int invCount = 0;
    int freq[40] = {0};
};

class SegTree {
private:
    int sz;
    vector<item> t;
    item merge(item a, item b) {
        item res;
        res.invCount = a.invCount + b.invCount;
        int suf = 0;
        for(int i=0; i<40; i++) {
            suf += a.freq[i];
        }
        for(int i=0; i<40; i++) {
            suf -= a.freq[i];
            res.invCount += b.freq[i] * suf;
            res.freq[i] = a.freq[i] + b.freq[i];
        }
        return res;
    }
    void init(vector<int> &v, int x, int lx, int rx) {
        if(lx == rx) {
            item i;
            i.freq[v[lx]]++;
            t[x] = i;
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
            item i;
            i.freq[q]++;
            t[x] = i;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        t[x] = merge(t[2*x+1], t[2*x+2]);
    }
    item calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) {
            item i;
            return i;
        }
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        return merge(calc(l, r, 2*x+1, lx, m), calc(l, r, 2*x+2, m+1, rx));
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        item i;
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
        return calc(l, r, 0, 0, sz-1).invCount;
    }
};

signed main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n, m;
    cin>>n>>m;
    vector<int> v(n);
    for(int &i:v) cin>>i, i--;
    SegTree sg(n);
    sg.init(v);
    while(m--) {
        int a, b, c;
        cin>>a>>b>>c;
        if(a == 1) {
            cout<<sg.calc(b-1, c-1)<<'\n';
        } else {
            sg.update(b-1, c-1);
        }
    }
}
```
