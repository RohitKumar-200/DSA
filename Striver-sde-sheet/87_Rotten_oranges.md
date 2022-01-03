# Rotten oranges

## Problem statement

You are given an `m x n` grid where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

## Solution (BFS)

Time complexity : O(M\*N)  
Space complexity : O(M\*N)

```cpp
int orangesRotting(vector<vector<int>>& grid) {
    int res = 0, m = grid.size(), n = grid[0].size(), fresh = 0;
    queue<pair<int, int>> q;
    for(int i=0; i<m; i++) {
        for(int j=0; j<n; j++) {
            if(grid[i][j] == 2)
                q.push({i, j});
            else if(grid[i][j] == 1)
                fresh++;
        }
    }
    int dx[] = {-1, 0, 1, 0};
    int dy[] = {0, 1, 0, -1};
    while(!q.empty()) {
        int sz = q.size();
        while(sz--) {
            pair<int, int> p = q.front();
            q.pop();
            for(int k=0; k<4; k++) {
                int x = p.first + dx[k];
                int y = p.second + dy[k];
                if(x<0 || x>=m || y<0 || y>=n || grid[x][y] != 1)
                    continue;
                fresh--;
                grid[x][y] = 2;
                q.push({x, y});
            }
        }
        if(!q.empty())
            res++;
    }
    if(fresh == 0) return res;
    return -1;
}
```
