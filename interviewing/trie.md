# Trie / Digital Tree / Radix Tree / Prefix Tree

Definition: A tree where a path from the root node to an "end" node indicates the existence of a value. 
- The root is the empty string. 
- For each possible symbol in a fixed set of symbols (i.e. letter in the English alphabet), a node has an array of pointers/references that index into the pointer for that node. (e.g. children[], index 0 -> a, index 25 -> z)
- Nodes have a boolean flag that indicates whether they're an 'end' node.

## Insertion

Every character of input key is inserted as an individual Trie node. The key character acts as an index into the array children. If the input key is new or an extension of existing key, we need to construct non-existing nodes of the key, and mark end of word for last node.  No need for recursion.

```
start = root
for each character in the search text
	index = map character to index // subtract 'a', for example for lower-case words
	if (start[index] == null) 
		start[index] = new Trie node // isEnd = false
	
	start = start[index]
	
start.isEnd = true
```

## Search
```
start = root
for each character in the search text
	index = map character to index // subtract 'a', for example for lower-case words
	if (start[index] == null)  
		return false
	start = start[index]
return start != null && start.isEnd
```

## Delete
```
func DeleteText(text)
	DeleteRecur(root, text, 0)

func DeleteRecur(node, text, symbolIndex) 
	childIndex = map text[symbolIndex] to childIndex, i.e. 'a' --> 0
	childNode = node[childIndex]
	
	if (childNode == null)
		return // Doesn't exist
		
	if (symbolIndex == text.Length - 1)
		if (!childNode.isEnd)
			return // Doesn't exist
			
		if (HasChildren(node[currentIndex]))  // Check all children to be null
			childNode.isEnd = false 
		else
			node[childIndex] = null
			
		return
			
			
	DeleteRecur(childNode, text, symbolIndex + 1)
```