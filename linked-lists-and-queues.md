# Linked Lists

* Definition:
    • A linked list is an ordered sequence of nodes
    • Each node contains a data value and a pointer to the next node

* Node Structure:
    ```js
    class LinkedListNode {
        constructor(value, next = null) {
            this.value = value;
            this.next = next;
        }
    }
    ```


* Linked List Structure:
    ```js
    class LinkedList {
        constructor() {
            this.head = null;
        }

        // add a node to the head
        addToHead(value) {
            this.head = new LinkedListNode(value, this.head);
        }

        // print all node value
        print() {
            let current = this.head;
            while (current) {
                process.stdout.write(`${current.value} ->`);
                current = current.next;
            }
            console.log("NULL");
        }
    }
    ```

* Creating and Adding Nodes:
    • Example to create nodes storing values 12, 99, 37:
    ```js
    const node3 = new LinkedListNode(37);
    const node2 = new LinkedListNode(99, node3);
    const node1 = new LinkedListNode(12, node2);

    const ll = new LinkedList();
    ll.head = node1;
    ```

* Add to Head Algorithm:
    1. Create a new node with the given value
    2. Set the new node's next pointer to the current head
    3. Update the head to the new node

    ```js
    addToHead(value) {
        this.head = new LinkedListNode(value, this.head);
    }
    ```

* Time Complexity:
    • addToHead: O(1)
        - Creating a new node: O(1)
        - Setting the next pointer O(1)
        - Updating head pointer: O(1)

* Traversing a Linked List:
    • To print or search, traverse each node until reaching null
    • Traversal Time Complexity: O(n)

    ```js
    print() {
        let current = this.head;
        while (current) {
            process.stdout.write(`${current.value} -> `);
            current = current.next;
        }
        console.log("NULL");
    }
    ```

* Memory Structure:
    • Nodes are stored non-contiguously in memory
    • Linked list nodes can be scattered, unlike array elements which are contiguous

* Comparison with Arrays:
    • Memory Usage: higher due to pointers
    • Access Time: O(n) for linked list (traverse nodes); O(1) for array (direct access)


* Key Questions

    1. Space Complexity of Linked List:
        • O(n) for n nodes due to storage of data and pointers

    2. Adding a Value to the End:
        • Traverse to the end node. then add the new node
        • Time Complexity: O(n)

    3. Recursive Print Function:
        ```js
        printRecursive(node = this.head) {
            if (!node) {
                console.log("NULL");
                return;
            }
            process.stdout.write(`${node.value} -> `);
            this.PrintRecursive(node.next);
        }
        ```
        • Time Complexity: O(n)
        • Space Complexity: O(n) due to call stack

* Summary:
    • Linked lists store ordered sequences using nodes with data and pointers
    • Efficient for insertions/removals at the head (O(1))
    • Traversal and access are O(n)
    • Higher memory usage compared to arrays due to additional pointers
