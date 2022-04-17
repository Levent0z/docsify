# Insert a node at a specific position in a linked list

[From](https://www.hackerrank.com/challenges/insert-a-node-at-a-specific-position-in-a-linked-list/problem?isFullScreen=false)

```TypeScript
class SinglyLinkedListNode {
    data: number;
    next: SinglyLinkedListNode | null;

    constructor(nodeData: number) {
        this.data = nodeData;
        this.next = null;
    }
};

class SinglyLinkedList {
    head: SinglyLinkedListNode | null;
    tail: SinglyLinkedListNode | null;

    constructor() {
        this.head = null;
        this.tail = null;
    }

    insertNode(nodeData: number): void {
        const node = new SinglyLinkedListNode(nodeData);

        if (this.head == null) {
            this.head = node;
        } else {
            this.tail!.next = node;
        }

        this.tail = node;
    }
};


function printSinglyLinkedList(node: SinglyLinkedListNode | null, sep: string, ws: WriteStream): void {
    while (node != null) {
        ws.write(String(node.data));

        node = node.next;

        if (node != null) {
            ws.write(sep);
        }
    }
}
```

## Solution

```TypeScript
function insertNodeAtPosition(llist: SinglyLinkedListNode, data: number, position: number): SinglyLinkedListNode {
    // Write your code here
    const newNode = new SinglyLinkedListNode(data);
    if (llist == null) {
        return newNode;
    }
    if (position === 0) {
        newNode.next = llist;
        return newNode;
    }
    
    const headNode = llist;
    let curNode = llist;
    while(position > 1 && curNode.next) {
        curNode = curNode.next;
        position -= 1;        
    }
    newNode.next = curNode.next;
    curNode.next = newNode;
    return headNode;
}
```
