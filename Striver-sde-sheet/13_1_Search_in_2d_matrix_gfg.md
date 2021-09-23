# Search in a matrix

## Problem statement

Given a matrix `mat[][]` of size `N x M`, where every row and column is sorted in increasing order, and a number X is given. The task is to find whether element X is present in the matrix or not.

## Approach 1 (Brute force)

Time complexity : O(N*M)  
Space complexity : O(1)

```cpp
int matSearch (vector <vector <int>> &mat, int N, int M, int X) {
    for(int i=0; i<N; i++)
        for(int j=0; j<M; j++)
            if(mat[i][j] == X)
                return 1;
    return 0;
}
```

## Approach 2 (Top-right to Bottom-left)

Time complexity : O(N+M)  
Space complexity : O(1)

```cpp
int matSearch (vector <vector <int>> &mat, int N, int M, int X) {
    int i=0, j=M-1;
    while(i<N && j>=0) {
        if(X == mat[i][j]) return 1;
        if(X < mat[i][j]) j--;
        else i++;
    }
    return 0;
}
```
