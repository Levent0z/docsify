# Trees 
- General implementation: A root node. List of children per node. 
- Example: Unix file system

# Binary tree
A tree where a node can have at most two children.

## Expression Tree
Leaf nodes are operands, ancestors are operators.

Creating an expression tree is similar to evaluating a postfix expression: instead of evaluating the operation, create a subtree where operands from the stack are the children of the operator, then push the subtree on the stack.

<br>

## Binary Search Tree
Left child is smaller than the parent, right-child is larger than the parent

### Corollaries: 
1. ALL elements in the right subtree of a node are larger than it. 
2. ALL elements in the left subtree of a node are smaller than it.
3. Smallest child is at the bottom left of the tree (drill to the left descendant until no more)
4. Largest child is at the bottom right of the tree (drill to the right descendant until no more)

### Search
Starting from the top, at each node choose left or right node, recursively, until found or done.

### Insert
Similar to Find. Pass the current (parent) node as argument. If not found, put it there.

### Remove
1. If the node has 0 children, delete trivially.
2. If the node has 1 child, the parent needs to adjust its left or right child pointer as applicable, similar to linked-list deletion.
3. If the node has 2 children, replace the key of that node with the **smallest key of the right subtree** and recursively remove that node.

<details>
<summary>Example</summary>

To delete "2":
1. Find "2" - has two children.
2. Find the smallest node on the right 
   1. "3" is found - has one child "4"
   2. To remove "3", left of "5" becomes "4"
3. Replace "2" with "3"


```
	      6                              6
       /     \                        /     \
      2       8                      3       8
   /      \                       /     \ 
  1        5          -->        1       5
         /                              /
       3                               4
  	    \
         4
```

</details>

<details>
<summary>Pseudo-code</summary>

```
Remove (key, node)
	if  node == null
		error
	elseif (key < node.key)
		Remove (key, node.left)
	elseif (key > node.key)
		Remove (key, node.right)
	elseif (node.left != null && node.right != null)
		// Two children
		tmpNode = FindMin(node.right)
		node.key = tmpNode.key;
		// node.data = tmpNode.data;
		Remove (tmpNode.Key, node.right)
	else
		// 0 or 1 child
		tmpNode = node;
		if (node.left == null)
			node = node.right     // This works in c++ because node is passed in as a reference to a pointer
		else if (node.right == null)
			node = node.Left;
       delete tmpNode
```

</details>