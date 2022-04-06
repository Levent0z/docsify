# B-Trees


A B-tree of order $k$ is a tree where:
- Every node has at most $k$ children
- The root is either a leaf or has at least 2 children
- All non-leaf nodes (except the root) has at least $\lceil\frac{k}{2}\rceil$ children
- A non-leaf node with $k$ children has $k-1$ keys.
- All leaves are at the same depth

Notes:
- "All data is stored at the leaves."
- There is an ordering in that leaf nodes contain items in the range indicated by their parent node, similar to a binary search tree.
- Has depth $O(\log_{k/2}n)$, where $n$ is the number of records. 

<br>

> B-Tree grows upwards from the leaves.

<br>

Goot to know:
- B-tree of order 3 is known as a "2-3 tree". 
- B-tree of order 4 is known as a "2-3-4 tree".
These names come how many values a leaf can hold.
- B-trees are advantageous in database systems when not all the data can be in the memory, and reducing disk accesses (which are significantly slower) is important.


## Insertion

All insertions start at a leaf node. To insert a new element, search the tree to find the leaf node where the new element should be added. Insert the new element into that node with the following steps:

1. If the node contains fewer than the maximum allowed number of elements, then there is room for the new element. Insert the new element in the node, keeping the node's elements ordered.
2. Otherwise the node is full, evenly split it into two nodes so:
   1. A single median is chosen from among the leaf's elements and the new element.
   2. Values less than the median are put in the new left node and values greater than the median are put in the new right node, with the median acting as a separation value.
   3. The separation value is inserted in the node's parent, which may cause it to be split, and so on. If the node has no parent (i.e., the node was the root), create a new root above this node (increasing the height of the tree).
   4. If the splitting goes all the way up to the root, it creates a new root with a single separator value and two children


[More on Wikipedia](https://en.wikipedia.org/wiki/B-tree)

### Example
Adding elements 1-7 into a B-tree of order 3:
![Example](https://upload.wikimedia.org/wikipedia/commons/3/33/B_tree_insertion_example.png)