# Pascal's triangle

## Problem 1 (Leetcode)

Given an integer numRows, return the first numRows of Pascal's triangle.

## Solution

Time complexity : O(N\*N)  
Space complexity : O(N\*N)

```cpp
vector<vector<int>> generate(int numRows) {
    vector<vector<int>> res(numRows);
    for(int i=0; i<numRows; i++) {
        res[i].resize(i+1);
        res[i][0] = res[i][i] = 1;
        for(int j=1; j<i; j++)
            res[i][j] = res[i-1][j-1] + res[i-1][j];
    }
    return res;
}
```

## Problem 2

Given row no. and column no. in a pascal triangle, find element in that position.

### Formula

r = row, c = col  
Element = <sup>r-1</sup>C<sub>c-1</sub>

## Solution

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int getPascalElement(int row, int col) {
    int res=1;
    for(int j=1; j<col; j++)
        res *= --row;
    while(--col) res /= col;
    return res;
}
```

## Problem 3

Given row number, return that whole row

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> getPascalRow(int row) {
    int n = row;
    vector<int> res(n);
    res[0] = res[n-1] = 1;
    int numerator = 1, denominator=1;
    for(int col=2; col<n; col++) {
        numerator *= (--row);
        denominator *= (col-1);
        res[col-1] = (numerator/denominator);
    }
    return res;
}
```
