# BFS of graph

## Problem statement

Given a directed graph. The task is to do Breadth First Traversal of this graph starting from 0.

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> bfsOfGraph(int V, vector<int> adj[]) {
    vector<int> res, vis(V, 0);
    queue<int> q;
    q.push(0);
    vis[0] = 1;
    while(!q.empty()) {
        int node = q.front();
        q.pop();
        res.push_back(node);
        for(int child:adj[node]) {
            if(!vis[child]) {
                q.push(child);
                vis[child] = 1;
            }
        }
    }
    return res;
}
```
