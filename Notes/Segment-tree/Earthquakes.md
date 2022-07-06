# Earthquakes

## Problem statement

A city is a sequence of n cells numbered from 0 to n−1. Initially, all cells are empty. Then m events of one of two types occur sequentially:

- a building with the strength h is being constructed in the cell i (if the building already existed in this cell, it is demolished and replaced with a new one),
- in the interval from l to r−1 an earthquake of power p happens, it destroys all buildings whose strength is not more than p.
  Your task is for each earthquake to say how many buildings it will destroy.

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

struct item {
    int mn, idx;
};

class SegTree {
private:
    int sz;
    vector<item> t;
    item merge(item a, item b) {
        if(a.mn < b.mn) return a;
        return b;
    }
    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = {q, lx};
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        t[x] = merge(t[2*x+1], t[2*x+2]);
    }
    item calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return {INT_MAX, 0};
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        return merge(calc(l, r, 2*x+1, lx, m), calc(l, r, 2*x+2, m+1, rx));
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, {INT_MAX, 0});
        sz = n;
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    item calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n, m;
    cin>>n>>m;
    SegTree sg(n);
    while(m--) {
        int a;
        cin>>a;
        if(a == 1) {
            int b, c;
            cin>>b>>c;
            sg.update(b, c);
        } else {
            int b, c, p, res = 0;
            cin>>b>>c>>p;
            item it = sg.calc(b, c-1);
            while(it.mn <= p) {
                sg.update(it.idx, INT_MAX);
                it = sg.calc(b, c-1);
                res++;
            }
            cout<<res<<'\n';
        }
    }
}
```
