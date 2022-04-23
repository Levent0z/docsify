# Heaps
A heap is a complete binary tree, except for the lowest level, which is filled from left to right.

- `Min-Heap`: Every node is smaller than its children. (Root is minimum)
- `Max-Heap`: Every node is larger than its children. (Root is maximum)

- Used to implement `Priority Queue`s.
- Can be implemented with **1-based** arrays.
  - For convenience in implementation, a very small or (very large) value can be used for a[0].
  - Next available index = Number of nodes in the tree
  - Left-child's index = $2i$, where $i$ is the index of the parent.
  - Right-child'ts index = $2i + 1$
  - Parent's index = $\lfloor c/2 \rfloor$, where c is the index of the child.

```
Level 0                         1
Level 1              2                     3
Level 2        4          5           6         7
Level 3     8     9    10   11     12   13   14   15
```

- For level $k$: $\qquad2^k <= value < 2^{k+1}$
- Therefore: 
  ```javascript 
  const k = Math.floor(Math.log2(value));
  ```


## Find

$O(1)$

## Insert

Insert at the next spot in the bottom, percolate up until heap order is satisfied (i.e. compare current with parent, switch if needed)

- Worst case: $O(\log n)$
- Average case: $O(1)$ for a random heap and for repeated insertions

## Delete Root

### Method One
Remove root, make last element new root. Pick the smaller child for min_heap (or larger child for max_heap) and percolate down until heap order is satisfied. 

Take care not to assume that a node has two children.

### Method Two
Remove root, percolate down to maintain order property by picking the smaller (or larger) of the children of the current. Finally, move the last element to the open slot at the bottom.



