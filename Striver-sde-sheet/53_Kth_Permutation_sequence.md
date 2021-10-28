# Kth Permutation sequence

## Problem statement

The set `[1, 2, 3, ..., n]` contains a total of `n!` unique permutations.

Given `n` and `k`, return the k<sup>th</sup> permutation sequence.

## Approach 1 (Find all permutations)

Time complexity : O(N! \* N)  
Space complexity : O(N! \* N)

```cpp
void findPermutations(int i, string s, vector<int> &v, vector<string> &permutations) {
    if(i == v.size()) {
        permutations.push_back(s);
        return;
    }
    for(int j=i; j<v.size(); j++) {
        swap(v[i], v[j]);
        findPermutations(i+1, s+to_string(v[i]), v, permutations);
    }
    int temp = v[i];
    for(int j=i; j<v.size()-1; j++) v[j] = v[j+1];
    v[v.size()-1] = temp;
}
string getPermutation(int n, int k) {
    vector<int> v(n);
    vector<string> permutations;
    for(int i=0; i<n; i++) v[i] = i+1;
    findPermutations(0, "", v, permutations);
    return permutations[k-1];
}
```

## Approach 2

Time complexity : O(N^2)  
Space complexity : O(N)

```cpp
string getPermutation(int n, int k) {
    vector<int> v(n);
    int fac = 1;
    for(int i=1; i<n; i++) v[i-1] = i, fac *= i;
    v[n-1] = n;
    string res = "";
    k--;
    while(true) {
        res += to_string(v[k/fac]);
        v.erase(v.begin() + k/fac);
        if(v.size() == 0) break;
        k %= fac;
        fac /= v.size();
    }
    return res;
}
```
