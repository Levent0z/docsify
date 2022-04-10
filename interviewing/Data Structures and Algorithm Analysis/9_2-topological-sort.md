# Topological Sort

`Topological Sort` is the ordering of vertices in a directed acyclic graph, such that if there is a path from $v_i$ to $v_j$,  then the former comes first.
- It is not possible if the graph has a cycle.
- Orderings are not necessarily unique.

`Indegree` is the number of directed edges coming into a vertex

## Idea
- Process each node that has 0 indegree in a queue. When a node is processed, "it's taken out of the graph", i.e. decrement the indegree of its adjacent vertices.

## Algorithm
1. Initialize an array "orders" for each vertex and initialize it to 0s.
2. Calculate the indegree of all vertices in the graph
3. Queue all vertices with indegree = 0;
4. As long as the queue is full
   1. Get the next vertex $v$
   2. increment the order of the vertex
   3. For each vertex $w$ adjacent to $v$,
      1. Decrement the indegree of $w$
      2. If indegree of $w$ is 0, enqueue $w$

<details>
<summary>Code</summary>

See [graph data structures](9_1-graph-data-structures.md) for referenced types below.

```TypeScript
function topoSort(g: Graph): Map<Vertex, number> {
    const orders = new Map<Vertex, number>();
    const queue = new Array<Vertex>();

    g.vertices.forEach(v => {
        if (v.inDegree === 0) {
            queue.push(v);
        }
    });

    order = 1;
    while(queue.length) {
        const v = queue.shift();
        orders[v] = order++;
        v.adjList.forEach(w => { 
            w.inDegree -= 1; 
            if (w.inDegree === 0) {
                queue.push(w);
            }
        });
    }

    if (order <= g.vertices.length) {
        throw new Error();
    }
    return orders;
}

```

</details>