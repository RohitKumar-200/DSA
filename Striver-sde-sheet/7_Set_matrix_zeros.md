# Set matrix zeros

## Problem statement

Given an m x n integer matrix, if an element is 0, set its entire row and column to 0's, and return the matrix.

## Approach 1 (Using 2d matrix)

Time complexity : O(M\*N\*(M+N))  
Space complexity : O(M\*N)

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int i, j, p, q, m=matrix.size(), n=matrix[0].size();
    vector<vector<int>> z(m, vector<int>(n, 1));
    for(i=0; i<m; i++) {
        for(j=0; j<n; j++) {
            if(matrix[i][j]==0) {
                for(p=0; p<m; p++) z[p][j]=0;
                for(q=0; q<n; q++) z[i][q]=0;
            }
        }
    }
    for(i=0; i<m; i++) {
        for(j=0; j<n; j++) {
            matrix[i][j] *= z[i][j];
        }
    }
}
```

## Approach 2 (Using two 1d matrix)

Time complexity : O(M\*N)  
Space complexity : O(M+N)

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int i, j, m=matrix.size(), n=matrix[0].size();
    vector<int> row(m, -1);
    vector<int> col(n, -1);
    for(i=0; i<m; i++) {
        for(j=0; j<n; j++) {
            if(matrix[i][j]==0)
                row[i] = col[j] = 0;
        }
    }
    for(i=0; i<m; i++) {
        for(j=0; j<n; j++) {
            if(row[i]==0 || col[j]==0)
                matrix[i][j]=0;
        }
    }
}
```

## Approach 3 (Constant space)

Time complexity : O(M\*N)  
Space complexity : O(1)

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int i, j, m=matrix.size(), n=matrix[0].size();
    bool fr=0, fc=0;
    for(i=0; i<m; i++) if(matrix[i][0]==0) fc=1;
    for(j=0; j<n; j++) if(matrix[0][j]==0) fr=1;
    for(i=1; i<m; ++i) {
        for(j=1; j<n; ++j) {
            if(matrix[i][j] == 0)
                matrix[i][0]=matrix[0][j]=0;
        }
    }
    for(i=1; i<m; i++) {
        if(matrix[i][0]==0)
            for(j=1; j<n; j++)
                matrix[i][j]=0;
    }
    for(j=1; j<n; j++) {
        if(matrix[0][j]==0)
            for(i=1; i<m; i++)
                matrix[i][j]=0;
    }
    if(fc) for(i=0; i<m; i++) matrix[i][0]=0;
    if(fr) for(j=0; j<n; j++) matrix[0][j]=0;
}
```

## Approach 4 (Most optimized, complexity same as above)

Time complexity : O(M\*N)  
Space complexity : O(1)

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int i, j, m=matrix.size(), n=matrix[0].size();
    bool col0=0;
    for(i=0; i<m; i++) {
        if(matrix[i][0]==0) col0 = 1;
        for(j=1; j<n; j++)
            if(matrix[i][j]==0)
                matrix[i][0] = matrix[0][j] = 0;
    }
    for(i=m-1; ~i; i--) {
        for(j=n-1; j>0; j--)
            if(matrix[i][0]==0 || matrix[0][j]==0)
                matrix[i][j]=0;
        if(col0) matrix[i][0]=0;
    }
}
```
