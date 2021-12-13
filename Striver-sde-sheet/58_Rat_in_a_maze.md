# Rat in a maze

## Problem statement

Consider a rat placed at `(0, 0)` in a square matrix of order `N * N`. It has to reach the destination at `(N - 1, N - 1)`. Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are **'U'(up), 'D'(down), 'L' (left), 'R' (right)**. Value `0` at a cell in the matrix represents that it is blocked and rat cannot move to it while value `1` at a cell in the matrix represents that rat can be travel through it.

**Note:** In a path, no cell can be visited more than one time.

## Solution (DFS in matrix)

Time complexity : O(4^N)  
Auxiliary space : O(N)

```cpp
void solve(int x, int y, string s, vector<vector<int>> &m, vector<string> &res) {
    int n = m.size();
    if(x<0 || x>=n || y<0 || y>=n || m[x][y] == 0) return;
    if(x == n-1 && y == n-1) {
        res.push_back(s);
        return;
    }
    int dx[] = {1, 0, 0, -1}, dy[] = {0, -1, 1, 0};
    char ch[] = {'D', 'L', 'R', 'U'};
    m[x][y] = 0;
    for(int k=0; k<4; k++)
        solve(x+dx[k], y+dy[k], s+ch[k], m, res);
    m[x][y] = 1;
}
vector<string> findPath(vector<vector<int>> &m, int n) {
    vector<string> res;
    solve(0, 0, "", m, res);
    return res;
}
```
