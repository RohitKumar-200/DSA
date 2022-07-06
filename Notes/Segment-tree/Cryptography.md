# Cryptography

## Problem statement

Given n matrices A1,A2,…,An of size 2×2. You need to calculate the product of the matrices Ai,Ai+1,…,Aj for several queries. All calculations are performed modulo r.

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

struct matrix {
    ll a, b, c, d;
};

class SegTree {
private:
    int sz, mod;
    vector<matrix> t;
    matrix multiply(matrix m1, matrix m2) {
        matrix res;
        res.a = (m1.a*m2.a + m1.b*m2.c)%mod;
        res.b = (m1.a*m2.b + m1.b*m2.d)%mod;
        res.c = (m1.c*m2.a + m1.d*m2.c)%mod;
        res.d = (m1.c*m2.b + m1.d*m2.d)%mod;
        return res;
    }
    void init(vector<matrix> &v, int x, int lx, int rx) {
        if(lx == rx) {
            t[x] = v[lx];
            return;
        }
        int m = lx + (rx-lx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        t[x] = multiply(t[2*x+1], t[2*x+2]);
    }
    matrix calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return {1, 0, 0, 1};
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2;
        return multiply(calc(l, r, 2*x+1, lx, m), calc(l, r, 2*x+2, m+1, rx));
    }
public:
    SegTree(int n, int r) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, {1, 0, 0, 1});
        sz = n;
        mod = r;
    }
    void init(vector<matrix> &v) {
        init(v, 0, 0, sz-1);
    }
    matrix calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int r, n, m;
    cin>>r>>n>>m;
    vector<matrix> v(n);
    for(auto &i:v) {
        cin>>i.a>>i.b>>i.c>>i.d;
    }
    SegTree sg(n, r);
    sg.init(v);
    while(m--) {
        int l, r;
        cin>>l>>r;
        matrix mat = sg.calc(l-1, r-1);
        cout<<mat.a<<' '<<mat.b<<'\n';
        cout<<mat.c<<' '<<mat.d<<'\n';
        cout<<'\n';
    }
}
```
