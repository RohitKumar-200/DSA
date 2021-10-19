# Search in a matrix

## Problem statement

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

## Approach 1 (Brute force)

Time complexity : O(M\*N)  
Space complexity : O(1)

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int M=matrix.size(), N=matrix[0].size();
    for(int i=0; i<M; i++)
        for(int j=0; j<N; j++)
            if(matrix[i][j] == target)
                return true;
    return false;
}
```

## Approach 2 (Top-right to Bottom-left)

Time complexity : O(M+N)  
Space complexity : O(1)

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int M=matrix.size(), N=matrix[0].size(), i=0, j=N-1;
    while(i<M && j>=0) {
        if(target == matrix[i][j]) return true;
        if(target < matrix[i][j]) j--;
        else i++;
    }
    return false;
}
```

## Approach 3 (Double binary search)

Time complexity : O(log(M)+O(log(N)))  
Space complexity : O(1)

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int m = matrix.size(), n = matrix[0].size();
    int l = 0, r = m-1, mid;
    while(l<r) {
        mid = (l+r)/2;
        if(matrix[mid][n-1] < target) l = mid+1;
        else r = mid;
    }
    int row = l;
    l=0, r=n-1;
    while(l<r) {
        mid = (l+r)/2;
        if(matrix[row][mid] < target) l = mid+1;
        else r = mid;
    }
    return matrix[row][l] == target ? true : false;
}
```

## Approach 4 (Binary search)

Time complexity : O(log(M\*N))  
Space complexity : O(1)

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int M=matrix.size(), N=matrix[0].size();
    int l=0, r=M*N-1, mid, i, j;
    while(l<=r) {
        mid = l+(r-l)/2;
        i=mid/N, j=mid%N;
        if(matrix[i][j] == target) return true;
        if(matrix[i][j] < target) l=mid+1;
        else r=mid-1;
    }
    return false;
}
```
