# Graph Terminology

- A `graph` is a set of vertices and edges.
- An `edge` is a set of pair of vertices in the graph.
- An edge can be weighted (aka has a cost). A `weighted graph` is a graph with weighted edges.
- A `vertex` is `adjacent` to another when there is an edge between them.
- A `path` is a series of edges where two edges share the same vertex as their end and start, respectively. Alternatively, a path is a series of vertices where each consecutive vertex forms an edge.
- A `simple path` is a path where all vertices are distinct (except maybe the first and the last).
- A `loop` is an edge with the same vertex as beginning and end.
- An `undirected graph` is when edge $v_1-v_2$ implies edge $v_2-v_1$.
- A `directed graph` is when edge $v_1 \rArr v_2$ doesn't imply edge $v_2 \rArr v_1$. (i.e. the ordering of vertices is important)
- A `cycle` (in a directed graph) is a path where the start and end vertices are the same, and the path consists of at least one edge.
- A directed graph is `acyclic` if it has no cycles.
- A `DAG` is a `directed acyclic graph`.

- An `undirected graph` is `connected` if there is a path from all vertices to all other vertices.
- A `complete undirected graph` is when there is an edge between all vertices.
- A `complete directed graph` is when there are **bidirectional** edges between all vertices. (aka `strongly connected`).
- A `weakly connected` directed graph is when the graph is not strongly connected, but there is an edge (of any direction) between all its vertices.

- A connected undirected graph is `biconnected` if there are no vertices whose removal disconnects the rest of the graph. If there are such vertices, those are called `articulation points`.

- A `Euler Path` is a path that visits every edge exactly once.
- A `Euler Cycle/Circuit` is a Euler Path that starts and ends with the same node.

> A connected multigraph (and simple graph) with at least two vertices has a Euler circuit if and only if each of its vertices has an even degree.

- `Hamiltonian Path` is a path that passes through each vertex exactly once.
- `Hamiltonian Cycle` is a simple cycle that includes all the vertices.  (NP-Complete)

> Difference between Euler & Hamiltonian: In the former, a vertex can be passed through multiple times.



