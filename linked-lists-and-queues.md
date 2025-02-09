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

While arrays are typically preferred for their simplicity and performance in scenarios requiring frequent random access and where the size of the collection is known and fixed, linked lists shine in situations where dynamic resizing, frequent insertions and deletions, and efficient memory usage are critical. Understanding these trade-offs helps you choose the right data structure for your specific application needs.


# Linked List Optimisation

* Linked List Performance Review
    • Definition: A linked list stores values in a sequence of nodes, each containing a value and a pointer to the next node
    • Space Complexity: O(n), since n nodes are required to store n values
    • Time Complexity:
        - `addToHead()`: O(1) - constant time, regardless of list size
        - `Traversal Operations (e.g. print, search)`: O(n) - must visit all nodes

* Adding to the Tail
    • Algorithm to Add to Tail:
        1. Create a new node with the given value
        2. If the list is empty (head is null), set the head and tail to this new node
        3. Otherwise, iterate to the last node
        4. Point the last node's `next` to the new node
    • Time Complexity: O(n), as it requires traversal to find the last node

* Optimising `addToTail`
    • Tail Pointer Addition:
        - Adds a tail pointer to point directly to the last node
        - Steps:
            1. Create a new node
            2. If the list is empty, point head and tail to the new node
            3. Otherwise, point the current tail's `next` to the new node
            4. Update the tail to the new node
        - Time Complexity: O(1) - constant time for add to tail operations

    • Adjusting `addToHead`:
        - Ensure both head and tail point to the new node if the list was empty

        ```js
        addToHead(value) {
            this.head = new LinkedListNode(value, this.head);
            if (!this.tail) this.tail = this.head;
        }
        ```


* Removing Nodes

    • Removing from Head:
        - Simply update the head to the next node
        - If the list becomes empty, update the tail to null

        ```js
        removeFromHead() {
            if (this.head) this.head = this.head.next;
            if (this.head === null) this.tail = null;
        }
        ```

    • Removing from Tail:
        - Without a previous pointer, you must traverse the list to find the second-to-last node
        - Steps:
            1. Traverse the list to find the second-to-last node
            2. Update its `next` to null
            3. Update the tail to this node
        - Time Complexity: O(n) - requires traversal to find the second-to-last node


* Doubly Linked List:

    • Definition: Each node has pointers to both the next and previous nodes

    • Benefits:
        - Remove from Tail becomes O(1):
            • Directly access the previous node of the tail
            • Update tail and the new tail's next to null

        ```js
        removeFromTail() {
            if (!this.tail) return;
            if (this.tail === this.head) {
                this.head = null;
                this.tail = null;
            } else {
                this.tail = this.tail.previous;
                this.tail.next = null;
            }
        }
        ```

    • Cost:
        - Space: Increased by O(n) due to additional pointers
        - Code Complexity: All list methods must account for both `next` and `previous` pointers


* Key Takeaways

    • Tradeoffs:
        - Performance vs. Readability: Optimisations like adding pointers improve performance but increase code complexity
        - Space vs. Time: Adding pointers consumes more memory but speeds up operations

    • Optimisation Decisions: Use Big-O analysis and timing benchmarks to decide if the tradeoffs are worth it

    • Understand Constraints: Always consider problem constraints and use cases before optimising

These principles help to evaluate and optimise data structures like linked lists effectively


# Queues

A queue is an abstract data type (ADT) that follows the First In, First Out (FIFO) principle. It is similar to waiting in a line: the first person in the line is the first person to be served.

* Key Concepts

    1. FIFO (First In, First Out):
        • The first element added to the queue will be the first one to be removed
        • Example: Customer service apps, printer queues

    2. Key Operations:
        • `enqueue(value)`: Adds an element to the end of the queue
        • `dequeue()`: Removes and returns the element from the front of the queue


* Implementing a Queue with an Array

    1. Array-Based Queue:
        • Uses an array to store elements
        • `enqueue(value)`: Adds the element to the end using `push()`
        • `dequeue()`: Removes the element from the front using `shift()`

        Example:
        ```js
        class Queue {
            constructor() {
                this.data = [];
            }
            enqueue(value) {
                this.data.push(value);
            }
            dequeue() {
                return this.data.shift();
            }
        }
        ```

    2. Performance Issue:
        • The `shift()` method in arrays requires shifting all other elements, making `dequeue()` an O(n) operation


* Implementing a Queue with a Linked List

    1. Linked List-Based Queue:
        • Utilises a linked list to store elements
        • `enqueue(value)`: Adds the element to the tail of the list
        • `dequeue()`: Removed the element from the head of the list

        Example:
        ```js
        const LinkedList = require('./linked-list.js');

        class Queue {
            constructor() {
                this.linkedList = new LinkedList();
            }
            enqueue(value) {
                this.linkedList.addToTail(value);
            }
            dequeue() {
                const value = this.linkedList.head.value;
                this.linkedList.removeFromHead();
                return value;
            }
        }
        ```

    2. Performance Advantage:
        • Both `addToTail` and `removeFromHead` operations are O(1), making the linked list implementation more efficient for large datasets


* Performance Testing

    1. Testing Enqueue and Dequeue Times:

        • Array Implementation:
        ```js
        // example with n = 100000
        q = new Queue();
        n = 100000;

        enqueueStartTime = Date.now();
        for (let i = 0; i < n; i++) {
            q.enqueue(i);
        }
        enqueueEndTime = Date.now();

        dequeueStartTime = Date.now();
        for (let i = 0; i < n; i++) {
            q.dequeue();
        }
        dequeueEndTime = Date.now();

        console.log(`Enqueue time: ${enqueueEndTime - enqueueStartTime}ms`);
        console.log(`Dequeue time: ${dequeueEndTime - dequeueStartTime}ms`);
        ```

        • Expected Results:
            - Linked List: Enqueue ~20ms, Dequeue ~5ms
            - Array: Enqueue -7ms, Dequeue - 877ms

    2. Comparative Testing:
        • For smaller values of n (e.g. n = 1000), the performance difference is negligible due to the high speed of arrays for small operations

* Tradeoffs

    1. Array vs. Linked List:

        • Array:
            - Simpler, easier to read and maintain
            - Efficient for small datasets

        • Linked list:
            - More complex but necessary for large datasets to avoid performance bottlenecks

    2. Decision Making:

        • Use arrays for simplicity and ease of maintenance for smaller datasets
        • Use linked lists for large datasets where performance is critical

* Summary
    • Queue: FIFO data structure with key operations `enqueue()` and `dequeue()`
    • Array Implementation: Simple but inefficient for large datasets due to O(n) `dequeue()` operations
    • Linked List Implementation: Efficient O(1) operations for both `enqueue()` and `dequeue()`, suitable for large datasets
    • Performance Testing: Validates the efficiency of linked list over array for large values of n
    • Tradeoffs: Balance between simplicity (array) and performance (linked list) based on the use case requirements
