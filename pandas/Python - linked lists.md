#LinkedLists #DSA #Leetcode 

https://www.freecodecamp.org/news/how-linked-lists-work/

# create a node 

```java
class Node {
    int data;
    Node next;
 
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

```java
// create nodes
Node node1 = new Node(11);
Node node2 = new Node(18);
Node node3 = new Node(24);
```

# link nodes 
Initially the `head` node is set to `null` because there are no nodes in the linked list yet.
```java
class LinkedList {

    Node head;

        LinkedList() {
        this.head = null;
    }

}
```

Now to connect the nodes together in a Linked List, you can start by setting the `head` node to the first node in the list, in this case `node1`.

```java
head = node1;
```
Then make the next of `node1` point to `node2`, and the next of `node2` point to `node3`. That is:
```java
node1.next = node2;
node2.next = node3;
```

# How to Append a Node to Linked List

Appending a node means adding a node to the end of a linked list. There are two cases to consider when appending a node:

- Appending to an empty linked list.
- Appending to a non-empty linked list.

## append to empty

```java
if (head == null) {
    head = newNode;
}
```

## append to non empty

If there are one or more nodes in a linked list, it is a non-empty linked list.
To append a node to a non-empty linked list, make the last node link to the new node.

Unlike arrays, we cannot access any elements in a linked list directly. We must traverse from the `head` node to the `last` node.

To do that, create a temporary pointer (you can call the pointer `current`) that points to the head node.
Next, make `current` point to its `next` node, till the `next` of the current node points to `null`.
When the `next` node of `current` is `null`, you can then make the `next` of the `current` node point to the new node. That is:

```java
while (current.next != null) {
    current = current.next;
}
current.next = newNode;
```

# insert a node

```
```java
current.next = newNode;
```

## How to Insert a Node in a Linked List

Inserting a node means adding a node to a given index. There are two cases to consider when inserting a node:

- Inserting a node at the first index.
- Inserting a node at a given index.
```
## Linked list: fast and slow pointer

  

```python

def fn(head):

    slow = head
    fast = head
    ans = 0


    while fast and fast.next:
        # do logic
        slow = slow.next
        fast = fast.next.next

    return ans

```

  # insert at first index
- make `next` of the new node point to the `head` node
- set the `head` to the new node
```java
if (index == 0) {
    newNode.next = head;
    head = newNode;
}
```

# ### How to Insert a Node at Any Position

Let’s suppose you want to add a node at index 2 in the linked list above.

To insert a node at index 2, you must **traverse the node** that comes before index 2.

Next, create a new node and make the `next` of the new node point to the `next` of the `current` node.

Make the `next` of `current` point to the new node.

```java
for (int i = 0; i < index - 1 && current != null; i++) {
    current = current.next;
}
if (current != null) {
    newNode.next = current.next;
    current.next = newNode;
}
```

### How to Delete the Head Node

Deleting the `head` node of a linked list is simple. You can store the data of the `head` node in a temporary variable if it needs to be accessed later. Then set the `head` pointer to point to the `next` node after the `head` node.
```java
if (index == 0) {
    deletedValue = head.data;
    head = head.next;
}
```

### How to Delete a Node at a Given Position

Suppose you want to delete the node at index 2 in the diagram below:
You can delete the node at index 2 by making the node at index 1 point to the node at index 3.

To delete a node you must access the node you want to delete and the node before it. Take two temporary pointers (you can call the pointers `previous` and `current`). Let `previous` point to `null` and `current` point to the `head` node.
Now, move `current` one step forward and move `previous` to `current` till you reach index 2.
Make the `next` of `previous` point to the `next` of the `current` node.
Then store the data of `current` in a variable for future use.

After removing the link to the node at index 2, it is no longer accessible through any reference in the linked list.

It's important to note that when removing a node from a linked list, you don't need to explicitly delete the node itself at the given index. This is because the removed node will be automatically handled by the garbage collector when it is no longer reachable through any references.

However, in languages like C or C++, which do not have automatic garbage collection, you need to manually delete the node when it is no longer needed to avoid memory leaks and wasted memory resources.
```java
for (int i = 0; i < index && current != null; i++) {
    previous = current;
    current = current.next;
}

if (current != null) {
    deletedValue = current.data;
    previous.next = current.next;
}
```

## Complete Linked List Code

The code below shows a complete linked list. You can create, append, insert, delete, and display the nodes in the linked list:

```java
class Node {

	int data;
	Node next;

	Node(int data) {
		this.data = data;
		this.next = null;
	}
}

class LinkedList {

	Node head;

	LinkedList() {
		this.head = null;
	}

	public void createLinkedList() {

		Node node1 = new Node(11);
		this.head = node1;

		Node node2 = new Node(18);
		node1.next = node2;

		Node node3 = new Node(24);
		node2.next = node3;
	}

	public void append(Node newNode) {

		Node current = this.head;

		if (current == null) {
			this.head = newNode;
		} else {
			while (current.next != null) {
				current = current.next;
			}
			current.next = newNode;
		}

	}

	public void insert(Node newNode, int index) {

		Node current = this.head;
		if (index == 0) {
			newNode.next = current;
			this.head = newNode;
		} else {

			for (int i = 0; i < index - 1 && current != null; i++) {
				current = current.next;
			}
			if (current != null) {
				newNode.next = current.next;
				current.next = newNode;
			}

		}

	}

	public int delete(int index) {

		Node current = this.head;
		Node previous = null;
		int deletedValue = -1;

		if (index == 0) {
			deletedValue = this.head.data;
			this.head = this.head.next;
			return deletedValue;
		}

		else {
			for (int i = 0; i < index && current != null; i++) {
				previous = current;
				current = current.next;

			}
			if (current != null) {

				deletedValue = current.data;
				previous.next = current.next;
			}
			return deletedValue;
		}
	}
	
	public void displayLinkedList() {

		Node current = this.head;
		while (current != null) {
			System.out.println(current.data);
			current = current.next;

		}
	}

}

class Main {
	public static void main(String[] args) {
		LinkedList l1 = new LinkedList();
		Node newNode1 = new Node(22);
		Node newNode2 = new Node(43);
		Node newNode3 = new Node(5);
		l1.createLinkedList();

		l1.append(newNode1);
		l1.insert(newNode2, 0);
		l1.insert(newNode3, 2);
		l1.delete(2);
		l1.displayLinkedList();
	}
}
```

```

## Reversing a linked list

  

```python

def fn(head):

    curr = head
    prev = None

    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node

    return prev

```

  