# Segment with the Maximum Sum

## Problem statement

In this problem, you need to write a segment tree to find the segment with the maximum sum.

The first line contains two numbers n and m, the size of the array and the number of operations. The next line contains n numbers ai, the initial state of the array. The following lines contain the description of the operations. The description of each operation is as follows: i v, assign the value v to the element with index i.

## Solution

```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

struct item {
    int val, pre, suf, sum;
};

class SegTree {
private:
    int sz;
    vector<item> t;
    void init(vector<int> &v, int x, int lx, int rx) {
        if(lx == rx) {
            int val = v[lx];
            if(val < 0)
                t[x] = {0, 0, 0, val};
            else
                t[x] = {val, val, val, val};
            return;
        }
        int m = (lx + rx)/2;
        init(v, 2*x+1, lx, m);
        init(v, 2*x+2, m+1, rx);
        item left = t[2*x+1], right = t[2*x+2];
        t[x].val = max(left.val, right.val);
        t[x].val = max(t[x].val, left.suf + right.pre);
        t[x].sum = left.sum + right.sum;
        t[x].pre = max(left.pre, left.sum+right.pre);
        t[x].suf = max(right.suf, right.sum+left.suf);
    }
    void update(int p, int q, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            if(q < 0)
                t[x] = {0, 0, 0, q};
            else
                t[x] = {q, q, q, q};
            return;
        }
        int m = (lx + rx )/2;
        update(p, q, 2*x+1, lx, m);
        update(p, q, 2*x+2, m+1, rx);
        item left = t[2*x+1], right = t[2*x+2];
        t[x].val = max(left.val, right.val);
        t[x].val = max(t[x].val, left.suf + right.pre);
        t[x].sum = left.sum + right.sum;
        t[x].pre = max(left.pre, left.sum+right.pre);
        t[x].suf = max(right.suf, right.sum+left.suf);
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        item i = {0, 0, 0, 0};
        t.assign(2*sz, i);
        sz = n;
    }
    void init(vector<int> &v) {
        init(v, 0, 0, sz-1);
    }
    void update(int p, int q) {
        update(p, q, 0, 0, sz-1);
    }
    int calc() {
        return t[0].val;
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
    cout<<sg.calc()<<'\n';
    while(m--) {
        int p, q;
        cin>>p>>q;
        sg.update(p, q);
        cout<<sg.calc()<<'\n';
    }
}
```
