# Unique paths

## Problem statement

A robot is located at the top-left corner of a `m x n` grid.

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid.

How many possible unique paths are there?

## Approach 1 (Recursion)

Time complexity : O(2^(M\*N))  
Space complexity : O(1)

```cpp
int countUniquePaths(int x, int y, int &m, int &n) {
    if(x<0 || x>=m || y<0 || y>=n) return 0;
    if(x==m-1 && y==n-1) return 1;
    return countUniquePaths(x+1, y, m, n) + countUniquePaths(x, y+1, m, n);
}
int uniquePaths(int m, int n) {
    return countUniquePaths(0, 0, m, n);
}
```

## Approach 2 (Recursive DP)

Time complexity : O(M\*N)  
Space complexity : O(M\*N)

```cpp
int countUniquePaths(int x, int y, int &m, int &n, vector<vector<int>> &dp) {
    if(x<0 || x>=m || y<0 || y>=n) return 0;
    if(x==m-1 && y==n-1) return 1;
    if(dp[x][y] != -1) return dp[x][y];
    return dp[x][y] = countUniquePaths(x+1, y, m, n, dp) + countUniquePaths(x, y+1, m, n, dp);
}
int uniquePaths(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n, -1));
    return countUniquePaths(0, 0, m, n, dp);
}
```

## Approach 3 (Iterative DP)

Time complexity : O(M\*N)  
Space complexity : O(M\*N)

```cpp
int uniquePaths(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n));
    for(int i=0; i<m; i++) dp[i][n-1]=1;
    for(int j=0; j<n; j++) dp[m-1][j]=1;
    for(int i=m-2; i>=0; i--)
        for(int j=n-2; j>=0; j--)
            dp[i][j] = dp[i+1][j] + dp[i][j+1];
    return dp[0][0];
}
```

## Approach 3 (Iterative DP with optimised space)

Time complexity : O(M\*N)  
Space complexity : O(N)

```cpp
int uniquePaths(int m, int n) {
    vector<int> dp(n, 1);
    for(int i=1; i<m; i++)
        for(int j=1; j<n; j++)
            dp[j] += dp[j-1];
    return dp[n-1];
}
```

## Approach 4 (Maths - Combination)

Time complexity : O(M+N)  
Space complexity : O(1)

> <sup>m+n-2</sup>C<sub>m-1</sub> or <sup>m+n-2</sup>C<sub>n-1</sub> or (m+n-2)! / ((m-1)! \* (n-1)!)

```cpp
int uniquePaths(int m, int n) {
    int N = m+n-2, R = m-1;
    double res=1;
    for(int i=R; i>=1; i--) {
        res *= N--;
        res /= i;
    }
    return round(res); // or (int)(res+0.5)
}
```
