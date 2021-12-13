# M coloring Problem

## Problem statement

Given an undirected graph and an integer `M`. The task is to determine if the graph can be colored with at most `M` colors such that no two adjacent vertices of the graph are colored with the same color. Here coloring of a graph means the assignment of colors to all vertices. Print `1` if it is possible to colour vertices and `0` otherwise.

## Approach 1 (DFS)

Time complexity : O(M^N)  
Auxiliary space : O(N)

```cpp
bool solve(int curr, bool graph[101][101], int color[], int &m, int &V) {
    if(color[curr] != -1) return true;
    vector<int> available(m, 1);
    for(int i=0; i<V; i++) {
        if(graph[curr][i] && color[i] != -1) {
            available[color[i]] = 0;
        }
    }
    for(int i=0; i<m; i++) {
        if(available[i]) {
            color[curr] = i;
            bool f = true;
            for(int j=0; j<V; j++) {
                if(graph[curr][j])
                    f = f && solve(j, graph, color, m, V);
            }
            if(f) return true;
            color[curr] = -1;
        }
    }
    return false;
}
bool graphColoring(bool graph[101][101], int m, int V) {
    int color[V];
    memset(color, -1, sizeof(color));
    bool f = true;
    for(int i=0; i<V; i++) {
        if(color[i] == -1)
            f = f && solve(i, graph, color, m, V);
    }
    return f;
}
```

## Approach 2 (Traversing node in recursive function)

Time complexity : O(M^N)  
Auxiliary space : O(N)

```cpp
bool solve(int curr, bool graph[101][101], int color[], int &m, int &V) {
    if(curr == V) return true;
    vector<int> available(m, 1);
    for(int i=0; i<V; i++) {
        if(graph[curr][i] && color[i] != -1) {
            available[color[i]] = 0;
        }
    }
    for(int i=0; i<m; i++) {
        if(available[i]) {
            color[curr] = i;
            if(solve(curr+1, graph, color, m, V))
                return true;
            color[curr] = -1;
        }
    }
    return false;
}
bool graphColoring(bool graph[101][101], int m, int V) {
    int color[V];
    memset(color, -1, sizeof(color));
    return solve(0, graph, color, m, V);
}
```
