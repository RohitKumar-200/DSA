# Fractional Knapsack

## Problem statement

Given weights and values of `N` items, we need to put these items in a knapsack of capacity `W` to get the maximum total value in the knapsack.

**Note:** Unlike 0/1 knapsack, you are allowed to break the item.

## Solution

Time complexity : O(N\*log(N))  
Space complexity : O(1) (Ignoring space taken by merge sort)

```cpp
static bool comp(Item i, Item j) {
    double iRatio = (double)i.value/i.weight, jRatio = (double)j.value/j.weight;
    return iRatio > jRatio;
}
double fractionalKnapsack(int W, Item arr[], int n) {
    sort(arr, arr+n, comp);
    double res=0;
    for(int i=0; W && i<n; i++) {
        if(arr[i].weight <= W) {
            W -= arr[i].weight;
            res += arr[i].value;
        } else {
            res += ((double)arr[i].value/arr[i].weight) * W;
            W = 0;
        }
    }
    return res;
}
```
