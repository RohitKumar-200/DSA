# Kth One

## Problem statement

In this problem, you need to add to the segment tree the operation of finding the k-th one.

The first line contains two numbers n and m, the size of the array and the number of operations. The next line contains n numbers ai, the initial state of the array. The following lines contain the description of the operations. The description of each operation is as follows:

- 1 i: change the element with index i to the opposite.
- 2 k: find the k-th one (ones are numbered from 0, it is guaranteed that there are enough ones in the array).

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
            t[x] = v[lx] == 1 ? 1 : 0;
            return;
        }
        int m = lx + (rx-lx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    void update(int p, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = (t[x] == 1 ? 0 : 1);
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, 2*x+1, lx, m);
        update(p, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    int calc(int p, int x, int lx, int rx) {
        if(lx == rx) return lx;
        int m = lx + (rx-lx)/2;
        if(p < t[2*x+1]) return calc(p, 2*x+1, lx, m);
        return calc(p-t[2*x+1], 2*x+2, m+1, rx);
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
    void update(int p) {
        update(p, 0, 0, sz-1);
    }
    int calc(int p) {
        return calc(p, 0, 0, sz-1);
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
        int a, b;
        cin>>a>>b;
        if(a == 1) {
            sg.update(b);
        } else {
            cout<<sg.calc(b)<<'\n';
        }
    }
}
```
