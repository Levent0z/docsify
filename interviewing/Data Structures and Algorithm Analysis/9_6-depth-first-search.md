# Depth-first Search

```TypeScript
function dfs(g: Graph, start: Vertex): void {
    start.known = true;
    start.adjList.forEach(w => {
        if (!w.known) {
            dfs(g, w);
        }
    });
}
```

> Time: $O(V+E)$ where $V$ is the number of vertices and $E$ is the number of edges.

> An undirected graph is connected if and only if a DFS starting from any node visits every node.