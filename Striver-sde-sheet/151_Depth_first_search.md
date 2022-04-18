# DFS of Graph

## Problem statement

Given a connected undirected graph. Perform a Depth First Traversal of the graph.

## Solution

Time complexity : O(N)  
Auxiliary space : O(N)

```cpp
void dfs(int curr, vector<int> adj[], vector<int> &vis, vector<int> &res) {
    if(vis[curr]) return;
    vis[curr] = 1;
    res.push_back(curr);
    for(int child:adj[curr])
        dfs(child, adj, vis, res);
}
vector<int> dfsOfGraph(int V, vector<int> adj[]) {
    vector<int> vis(V, 0);
    vector<int> res;
    dfs(0, adj, vis, res);
    return res;
}
```
