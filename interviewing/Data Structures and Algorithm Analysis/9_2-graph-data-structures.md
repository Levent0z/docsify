# Graph Data Structures
For each vertex, keep track of adjacent vertices. Use `adjacency matrix` for dense graphs, `adjacency lists` for sparse graphs.

Walking the list of a vertex in the adjacency list, by definition, gives all the adjacent vertices.

```TypeScript
class AdjVertex 
{
	w: Vertex;
    distVtoW: number;
}

class Vertex
{
	adjList: AdjVertex[] = [];
    known: boolean;
    dist: number = Infinity;
    previous: Vertex;
}

class Graph
{
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