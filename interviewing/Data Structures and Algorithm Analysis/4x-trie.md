# Trie
AKA `Digital Tree`, `Radix Tree`, `Prefix Tree`

**Definition**: A tree where a path from the root node to an "end" node indicates the existence of a value. 

- The root is the empty string. 
- For each possible symbol in a fixed set of symbols (i.e. letter in the English alphabet), a node has an array of pointers/references that index into the pointer for that node. (e.g. children[], index 0 -> a, index 25 -> z)
- Nodes have a boolean flag that indicates whether they're an 'end' node.

```TypeScript
class TrieNode {
    readonly children: TrieNode[];
    isEnd: boolean;
    constructor(size: number) {
        this.children = new Array<TrieNode>(size);
    }
}
```

<hr>

## Insertion

Every character of input key is inserted as an individual Trie node. The key character acts as an index into the array children. If the input key is new or an extension of existing key, we need to construct non-existing nodes of the key, and mark end of word for last node.  **No need for recursion**.

<details>
<summary>Code</summary>

```TypeScript
const A = 'A'.charCodeAt(0);
const range = 'z'.charCodeAt(0) - A + 1;

function insert(root: TrieNode, text: string): void {
    let start: TrieNode = root;
    Array.from(text).forEach(charStr => {
        const index = charStr.charCodeAt(0) - A; // map character to index
        if (!start[index])  {
            start.children[index] = new TrieNode(range);
        }        
        start = start.children[index];
    });     
    start.isEnd = true
}
```

</details>
<hr>

## Search

Search is practically the same as inserting, except instead of creating the node when a link is not found, return false. If the text is found, ensure the last char is at an "end" node.

<details>
<summary>Code</summary>

```TypeScript
function search(root: TrieNode, text: string): boolean {
    let start: TrieNode = root;
    Array.from(text).forEach(charStr => {
        const index = charStr.charCodeAt(0) - A; // map character to node index
        if (!start[index])  {
            return false;
        }        
        start = start.children[index];
    });        
    return start?.isEnd;
}
```
</details>
<hr>

## Delete

1. Use helper method to process nth character of a given text for the current node.
2. If the node doesn't have a corresponding child, done.
3. If it does, and it's the last character:
    1. If the childNode is not "end" done, done.
    2. If the childNode has its own children, then make it a non-end node, done.
       1. Otherwise, reset current node's child Index. done.
4. Otherwise, call the method with the next character index.

<details>
<summary>Code</summary>

```TypeScript
function deleteText(text: string): boolean {
    return deleteRecur(root, text, 0);
}

function deleteRecur(node: TrieNode, text: string, charIndex: number): boolean {
    const index = text[charIndex].charCodeAt(0) - A; // map character to node index
    const childNode = node[index];

    if (!childNode) {
        return false;
    }
    if (charIndex === text.length - 1) {
        if (!childNode.isEnd) {
            return false;
        }

        // Found. Has children?
        if (childNode.children.some(l => !l)) {
            childNode.isEnd = false;
        } else {
            node[index] = undefined;
        }
        return true;
    }
    return deleteRecur(childNode, text, charIndex + 1);
}

```
</details>
