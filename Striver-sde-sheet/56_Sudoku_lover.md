## Problem statement

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

## Approach 1 (Simple recursion)

Time complexity : 9^(9\*9)  
Space complexity : O(1)  
Auxiliary Space : O(9\*9)

```cpp
bool isValid(int x, int y, vector<vector<char>> &board, char ch) {
    for(int i=0; i<9; i++) if(board[i][y] == ch) return false;
    for(int j=0; j<9; j++) if(board[x][j] == ch) return false;
    int row = x - x%3, col = y - y%3;
    for(int i=0; i<3; i++)
        for(int j=0; j<3; j++)
            if(board[row+i][col+j] == ch)
                return false;
    return true;
}
bool solve(int x, int y, vector<vector<char>> &board) {
    if(x==9) return true;
    if(y==9) return solve(x+1, 0, board);
    if(board[x][y] != '.') return solve(x, y+1, board);
    for(int ch='1'; ch<='9'; ch++) {
        if(isValid(x, y, board, ch)) {
            board[x][y] = ch;
            if(solve(x, y+1, board)) return true;
            board[x][y] = '.';
        }
    }
    return false;
}
void solveSudoku(vector<vector<char>>& board) {
    solve(0, 0, board);
}
```

## Approach 2 (Recursion + Hashing)

Time complexity : O(81)  
Space complexity : O(3\*9\*256)  
Auxiliary space : O(9\*9)

```cpp
class Solution {
private:
    int row[9][256], col[9][256], cube[3][3][256];
    bool isValid(int x, int y, vector<vector<char>> &board, char ch) {
        if(row[x][ch] || col[y][ch] || cube[x/3][y/3][ch]) return false;
        return true;
    }
    bool solve(int x, int y, vector<vector<char>> &board) {
        if(x==9) return true;
        if(y==9) return solve(x+1, 0, board);
        if(board[x][y] != '.') return solve(x, y+1, board);
        for(int ch='1'; ch<='9'; ch++) {
            if(isValid(x, y, board, ch)) {
                board[x][y] = ch;
                row[x][ch] = col[y][ch] = cube[x/3][y/3][ch] = 1;
                if(solve(x, y+1, board)) return true;
                row[x][ch] = col[y][ch] = cube[x/3][y/3][ch] = 0;
                board[x][y] = '.';
            }
        }
        return false;
    }
public:
    void solveSudoku(vector<vector<char>>& board) {
        memset(row, 0, sizeof(row));
        memset(col, 0, sizeof(col));
        memset(cube, 0, sizeof(cube));

        for(int i=0; i<9; i++) {
            for(int j=0; j<9; j++) {
                if(board[i][j] != '.') {
                    int d = board[i][j];
                    row[i][d] = col[j][d] = cube[i/3][j/3][d] = 1;
                }
            }
        }
        solve(0, 0, board);
    }
};
```
