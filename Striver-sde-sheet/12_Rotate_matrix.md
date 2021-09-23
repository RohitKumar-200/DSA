# Rotate matrix

## Problem statement

You are given an `n x n` 2D matrix representing an image, rotate the image by `90 degrees` (clockwise).


## Approach 1 (Using extra space)

Time complexity : O(N^2)  
Space complexity : O(N^2)

```cpp
void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size(), i, j;
    vector<vector<int>> temp(n, vector<int>(n));
    for(i=0; i<n; i++)
        for(j=0; j<n; j++)
            temp[j][n-i-1] = matrix[i][j];
    for(i=0; i<n; i++)
        for(j=0; j<n; j++)
            matrix[i][j] = temp[i][j];
}
```

## Approach 2 (Ring by ring)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size(), i, j;
    for(i=0; i<n/2; i++) {
        for(j=0; j<(n+1)/2; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[n-j-1][i];
            matrix[n-j-1][i] = matrix[n-i-1][n-j-1];
            matrix[n-i-1][n-j-1] = matrix[j][n-i-1];
            matrix[j][n-i-1] = temp;
        }
    }
}
```

## Approach 3 (Transpose + Reverse left to right)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size(), i, j;
    for(i=0; i<n; i++)
        for(j=i+1; j<n; j++)
            swap(matrix[i][j], matrix[j][i]);
    for(auto &vi : matrix) reverse(vi.begin(), vi.end());
}
```

## General approach

* Transpose + Reverse left to right => Resultant is Clockwise
    ```
    1 2 3     1 4 7     7 4 1
    4 5 6  => 2 5 8  => 8 5 2
    7 8 9     3 6 9     9 6 3
    ```
* Transpose + Reverse top to bottom => Resultant is Anticlockwise
    ```
    1 2 3     1 4 7     3 6 9
    4 5 6  => 2 5 8  => 2 5 8
    7 8 9     3 6 9     1 4 7
    ```
* Reverse top to bottom + Transpose => Resultant is Clockwise
    ```
    1 2 3     7 8 9     7 4 1
    4 5 6  => 4 5 6  => 8 5 2
    7 8 9     1 2 3     9 6 3
    ```
* Reverse left to right + Transpose => Resultant is Anticlockwise
    ```
    1 2 3     3 2 1     3 6 9
    4 5 6  => 6 5 4  => 2 5 8
    7 8 9     9 8 7     1 4 7
    ```
