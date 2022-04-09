# Splay Tree

A binary search tree where after a node is accessed, it is pushed to the root by a series of AVL tree rotations.

No balance requirement.

Doing only single-rotations doesn't improve access times for all nodes.

Instead, we need to consider two types of rotations:
1. `zig-zig`: Like rotating 3 nodes without bending in the middle so the lowest node becomes the top
2. `zig-zag`: AVL double-rotation

## Example: Find '4':

<pre>
                    16
            8             32
       6        12
   2      7
1    4
    3 5
</pre>

Apply **zig-zag on 6, 2, 4:**:

<pre>
                    16
            8             32
       4        12
   2     6
1    3  5  7
</pre>

Notice how the left of 4, became the right of its parent and how the right of 4 became the left of its right child.

Next, apply **zig-zig on 16, 8, 4**:

<pre>
                    4    
            2               8    
        1       3       6       16 
                       5 7    12  32
</pre>


> Guarantees any $m$ consecutive operations take at most $O(m \cdot \log⁡ n)$  time. Any single operation might take $O(n)$ time. It has an "amortized" running time of $O(\log⁡ n)$.



