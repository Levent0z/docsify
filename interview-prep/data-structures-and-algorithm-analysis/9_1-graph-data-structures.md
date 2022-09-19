# Graph Data Structures
For each vertex, keep track of adjacent vertices. Use `adjacency matrix` for dense graphs, `adjacency lists` for sparse graphs.

Walking the list of a vertex in the adjacency list, by definition, gives all the adjacent vertices.

```typescript
class AdjVertex {
	w: Vertex;
    distVtoW: number;
}

class Vertex {
	adjList: AdjVertex[] = [];

    // Working fields used by algorithms
    known: boolean;   // Another name is "visited"
    distance: number; // Can set this to Infinity if need be
    previous: Vertex;
}

class Graph {
	vertices: Vertex[];
    constructor(numVertices: number)
	{
		this.vertices = new Array(numVertices);
        for (let i = 0; i < this.vertices.length; i += 1){
            this.vertices[i] = new Vertex();
        }
	}
}
```