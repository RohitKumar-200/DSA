# Sign Alteration

## Problem statement

Implement data structure of n elements a1,a2…an, with the following operations:

- assign the element ai value j;
- find alternating sign sum in the range from l to r inclusive (al−al+1+al+2− … ±ar).

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<ll> t;
    void init(vector<int> &v, int x, int lx, int rx) {
        if(lx == rx) {
            t[x] = v[lx];
            if(lx&1) t[x] *= -1;
            return;
        }
        int m = lx + (rx-lx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = q;
            if(lx&1) t[x] *= -1;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    ll calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return 0;
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        return calc(l, r, 2*x+1, lx, m) + calc(l, r, 2*x+2, m+1, rx);
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, 0);
        sz = n;
    }
    void init(vector<int> &v) {
        init(v, 0, 0, sz-1);
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    ll calc(int l, int r) {
        if(l & 1) return -1LL * calc(l, r, 0, 0, sz-1);
        return calc(l, r, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n;
    cin>>n;
    vector<int> v(n);
    for(int &i:v) cin>>i;
    int m;
    cin>>m;
    SegTree sg(n);
    sg.init(v);
    while(m--) {
        int a, b, c;
        cin>>a>>b>>c;
        if(a == 0) {
            sg.update(b-1, c);
        } else {
            cout<<sg.calc(b-1, c-1)<<'\n';
        }
    }
}
```
