# N Queens

## Problem statement

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the **n-queens puzzle**. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

## Approach 1 (Checking all directions recursively)

Time complexity : O(N^3)  
Space complexity : O(N^2)

```cpp
bool isValid(int x, int y, vector<string> &nQueens) {
    int i = x, j = y, n = nQueens.size();
    while(i >= 0 && j < n) {
        if(nQueens[i][j] == 'Q')
            return false;
        i--, j++;
    }
    i = x, j = y;
    while(i >= 0 && j >= 0) {
        if(nQueens[i][j] == 'Q')
            return false;
        i--, j--;
    }
    i = x, j = y;
    while(i >= 0) {
        if(nQueens[i][j] == 'Q')
            return false;
        i--;
    }
    return true;
}
void solve(int row, int n, vector<string> &nQueens, vector<vector<string>> &res) {
    if(row == n) {
        res.push_back(nQueens);
        return;
    }
    for(int col = 0; col < n; col++) {
        if(isValid(row, col, nQueens)) {
            nQueens[row][col] = 'Q';
            solve(row+1, n, nQueens, res);
            nQueens[row][col] = '.';
        }
    }
}
vector<vector<string>> solveNQueens(int n) {
    vector<vector<string>> res;
    vector<string> nQueens(n, string(n, '.'));
    solve(0, n, nQueens, res);
    return res;
}
```

## Approach 2 (Hashing)

Time complexity : O(N^2)  
Space complexity : O(N^2) + 3\*O(N)

```cpp
void solve(int row, int &n, vector<string> &nQueens, vector<vector<string>> &res, vector<int> &flag_col, vector<int> &flag_45, vector<int> &flag_135) {
    if(row == n) {
        res.push_back(nQueens);
        return;
    }
    for(int col=0; col<n; col++) {
        if(!flag_col[col] && !flag_45[row+col] && !flag_135[n-1+col-row]) {
            flag_col[col] = flag_45[row + col] = flag_135[n - 1 + col - row] = 1;
            nQueens[row][col] = 'Q';
            solve(row+1, n, nQueens, res, flag_col, flag_45, flag_135);
            nQueens[row][col] = '.';
            flag_col[col] = flag_45[row + col] = flag_135[n - 1 + col - row] = 0;
        }
    }
}
vector<vector<string>> solveNQueens(int n) {
    vector<vector<string>> res;
    vector<string> nQueens(n, string(n, '.'));
    vector<int> flag_col(n, 0), flag_45(2 * n - 1, 0), flag_135(2 * n - 1, 0);
    solve(0, n, nQueens, res, flag_col, flag_45, flag_135);
    return res;
}
```
