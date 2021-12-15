# Aggressive cows

## Problem statement

Farmer John has built a new long barn, with `N` (2 <= N <= 100,000) stalls. The stalls are located along a straight line at positions `x1,...,xN` (0 <= xi <= 1,000,000,000).

His `C` (2 <= C <= N) cows don't like this barn layout and become aggressive towards each other once put into a stall. To prevent the cows from hurting each other, FJ wants to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. What is the **largest minimum distance**?

## Approach 1 (Linear search)

Time complexity : O(N*N)  
Space complexity : O(1)

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPossible(int a[], int n, int dist, int cows) {
	int cnt = 1, ind = 0;
	for(int i=0; i<n; i++) {
		if(a[i] - a[ind] >= dist) {
			ind = i;
			cnt++;
		}
	}
	return cnt >= cows;
}

int main() {
	int t;
	for(cin>>t; t--;) {
		int n, cows;
		cin>>n>>cows;
		int a[n];
		for(int i=0; i<n; i++) cin>>a[i];
		sort(a, a+n);
		int res = -1;
		for(int dist = 1, mxDist = a[n-1] - a[0]; dist <= mxDist; dist++) {
		    if(isPossible(a, n, dist, cows)) res = dist;
		    else break;
		}
		cout<<res<<endl;
	}
	return 0;
}
```

## Appraoch 2 (Binary search)

Time complexity : O(N\*log(N))  
Space complexity : O(1)

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPossible(int a[], int n, int dist, int cows) {
	int cnt = 1, ind = 0;
	for(int i=0; i<n; i++) {
		if(a[i] - a[ind] >= dist) {
			ind = i;
			cnt++;
		}
	}
	return cnt >= cows;
}

int main() {
	int t;
	for(cin>>t; t--;) {
		int n, cows;
		cin>>n>>cows;
		int a[n];
		for(int i=0; i<n; i++) cin>>a[i];
		sort(a, a+n);
		int low = 1, high = a[n-1] - a[0], res = -1;
		while(low <= high) {
			int mid = (low + high) >> 1;
			if(isPossible(a, n, mid, cows)) {
				res = mid;
				low = mid + 1;
			} else {
				high = mid - 1;
			}
		}
		cout<<res<<endl;
	}
	return 0;
}
```
