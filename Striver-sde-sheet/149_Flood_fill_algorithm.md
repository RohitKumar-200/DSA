# Flood fill

An image is represented by an `m x n` integer grid image where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `newColor`. You should perform a flood fill on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with newColor.

Return the modified image after performing the flood fill.

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
    if(image[sr][sc] == newColor) return image;
    queue<pair<int, int>> q;
    q.push({sr, sc});
    int m = image.size(), n = image[0].size();
    int oldColor = image[sr][sc];
    while(!q.empty()) {
        int x = q.front().first, y = q.front().second;
        q.pop();
        image[x][y] = newColor;
        if(x > 0 && image[x-1][y] == oldColor)
            q.push({x-1, y});
        if(x < m-1 && image[x+1][y] == oldColor)
            q.push({x+1, y});
        if(y > 0 && image[x][y-1] == oldColor)
            q.push({x, y-1});
        if(y < n-1 && image[x][y+1] == oldColor)
            q.push({x, y+1});
    }
    return image;
}
```
