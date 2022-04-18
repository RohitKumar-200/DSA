# Clone Graph

## Problem statement

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

## Solution

Time complexity : O(N)  
Space complexity : O(N)  
Auxiliary space : O(N)

```cpp
Node* dfs(Node* node, unordered_map<Node*, Node*> &hash) {
    if(hash.find(node) == hash.end()) {
        hash[node] = new Node(node->val);
        for(Node* neighbor:node->neighbors) {
            hash[node]->neighbors.push_back(dfs(neighbor, hash));
        }
    }
    return hash[node];
}
Node* cloneGraph(Node* node) {
    if(node == NULL) return node;
    unordered_map<Node*, Node*> hash;
    return dfs(node, hash);
}
```
