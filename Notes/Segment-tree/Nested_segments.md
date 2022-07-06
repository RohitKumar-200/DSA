# Nested Segments

## Problem statement

Given an array of 2n numbers, each number from 1 to n in it occurs exactly twice. We say that the segment y is nested inside the segment x if both occurrences of the number y are between the occurrences of the number x. Find for each segment i how many segments that are nested inside it.

## Solution

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

class SegTree {
private:
    int sz;
    vector<int> t;
    void update(int p, int x, int lx, int rx) {
        if(p < lx || p > rx) return;
        if(lx == rx) {
            t[x] = 1;
            return;
        }
        int m = lx + (rx-lx)/2;
        update(p, 2*x+1, lx, m);
        update(p, 2*x+2, m+1, rx);
        t[x] = t[2*x+1] + t[2*x+2];
    }
    int calc(int l, int r, int x, int lx, int rx) {
        if(r < lx || l > rx) return 0;
        if(l <= lx && rx <= r) return t[x];
        int m = lx + (rx-lx)/2, res = 0;
        res += calc(l, r, 2*x+1, lx, m);
        res += calc(l, r, 2*x+2, m+1, rx);
        return res;
    }
public:
    SegTree(int n) {
        sz = 1;
        while(sz < n) sz <<= 1;
        t.assign(2*sz, 0);
        sz = n;
    }
    void update(int p) {
        update(p, 0, 0, sz-1);
    }
    int calc(int l, int r) {
        return calc(l, r, 0, 0, sz-1);
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n;
    cin>>n;
    vector<int> v(2*n);
    map<int, int> mp;
    vector<int> res(n);
    SegTree sg(2*n);
    for(int i=0; i<2*n; i++) {
        cin>>v[i];
        if(mp.find(v[i]) != mp.end()) {
            int j = mp[v[i]];
            res[v[i]-1] = sg.calc(j, i);
            sg.update(j);
        } else {
            mp[v[i]] = i;
        }
    }
    for(auto it:res) cout<<it<<' ';
}
```
