# AVL Trees
An AVL tree is identical to a **binary search tree**, except that **for every node, the height of the left and right subtree can differ by at most 1**. The height of an empty tree is defined to be -1.


## Insertion
During insertion, balance may need to be restored through single or double rotation. 

Start at the node inserted and travel up the tree, updating balance information at every node on the path. If an unbalance is found, do the rotation and it's done. (No need to keep traveling)

### Example:
1. Inserting 1 through 7 can be achieved by single rotation when needed. 
<pre>
        4
    2       6
1     3   5    7
</pre>

2. Insert 15, doesn't affect balance.
3. Insert 14, requires double rotation.


### Single Rotation
Involves 3 subtrees
<pre>
    8               4               2
  4       -->    2     8    <--       4
2                                       8
</pre>



### Double Rotation 
Involves 4 subtrees
<pre>
    8               4               2
2         -->    2     8    <--         8
  4                                   4
</pre>
