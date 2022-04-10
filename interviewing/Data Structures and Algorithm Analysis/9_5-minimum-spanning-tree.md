# Minimum Spanning Tree

`Minimum Spanning Tree` of an *undirected* graph is a tree formed from edges that connects all vertices at lowest total cost.

## Prim's Algorithm
It's essentially identical to [Dijkstra's](9_3-shortest-path-algorithms.md), except the definition of "distance" is changed: it is the weight of the shortest edge connecting v to a known vertex.

<details>
<summary>Code</summary>

```TypeScript
// Note: This hasn't been tested, use at your own risk.
function minimumSpanningTree(g: Graph, v: Vertex): void {
    v.distance = 0;
    do {
        v.known = true;
        let closestW: Vertex;
        let closestValue = Infinity;
        v.adjList.forEach(w => {
            if (!w.known && (w.distance === undefined || w.distance > w.distVtoW)) {  // Changed from dijkstra
                w.distance = w.distVtoW;                                              // Changed from dijkstra
                w.previous = v;
                if (w.distVtoW < closestValue) {
                    closestValue = w.distVtoW;
                    closestW = w;
                }
            }
        })
        v = closestW;
    } while(v !== null);
}
```

</details>
			

## Kruskal's Algorithm
- Maintains a forest of trees (Initially as many trees as there are vertices)
- Picks an edge of the smallest weight if it doesn't cause a cycle
- joins trees as it goes
- when enough edges are selected, it's done
- Uses the Union/Find algorithm/data structure from chapter 8.