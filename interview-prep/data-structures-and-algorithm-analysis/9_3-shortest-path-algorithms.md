# Shortest Path Algorithms

Refer to the [graph data structures](interview-prep/data-structures-and-algorithm-analysis/9_1-graph-data-structures.md) for types used in code sections below.

If the path is already known, recursion can be used to print the path from start to end, using each vertex's `previous` field.

```typescript
function printPath(start: Vertex, end: Vertex): void {
    if (start === end) {
        console.log(start);
        return;
    }
    // Use recursion to print the path in the correct order
    printPath(start, end.previous);
    console.log(end);
}
```

But how do we set the previous values?
**Problem**: Starting at a given vertex, find shortest path from it to all the other vertices.


## For undirected, unweighted graph
Use `Breadth-First Search (BFS)`.

<details>
<summary>Code</summary>

```typescript
function unweightedShortestPath(g: Graph, start: Vertex): void {
    const queue = new Array<Vertex>();
    start.distance = 0;
    queue.push(start);
    while(queue.length) {
        const v: Vertex = queue.shift();
        v.adjList.forEach(w => {
            if (w.distance === undefined) {
                w.distance = v.distance + 1;
                w.previous = v;
                queue.push(w);
            }
        });
    }
}
```

</details>

## For a directed, weighted, connected graph

Use `Dijkstra's Algorithm`. It's a `greedy` algorithm that takes the shortest path from available options at that iteration. 

In each iteration, pick the closest new vertex seen to be the next current vertex.

<details>
<summary>Code</summary>

```typescript
// Note: This implementation hasn't been tested, use at your own risk.
function dijkstra(g: Graph, v: Vertex): void {
    v.distance = 0;
    do {
        v.known = true;
        let closestW: Vertex;
        let closestValue = Infinity;
        v.adjList.forEach(w => {
            if (!w.known && (w.distance === undefined || w.distance > v.distance + w.distVtoW)) {
                w.distance = v.distance + w.distVtoW;
                w.previous = v;
                if (w.distVtoW < closestValue) {
                    closestValue = w.distVtoW;
                    closestW = w;
                }
            }
        })
        v = closestW;
    } while(v);
}
```

</details>
<br>

**Note**: Dijkstra is a special case of [A* Search Algorithm](https://www.geeksforgeeks.org/a-search-algorithm/), where h = 0 for all nodes. (h is the heuristic used in $f = g + h$.)

