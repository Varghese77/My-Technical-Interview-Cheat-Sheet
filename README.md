# Programming Interview Cheat-Sheet


## Table of Contents
1. Linked Lists
2. Graphs and Trees
3. 

## Linked Lists
#### Types of Linked Lists
A linked lists is a list of elements represented as a serial connection of nodes. There are three types of linked lists.

1. A ```Singly Linked List``` is implemented with nodes having a single reference to the next element in the list (or ```null``` if there is none). A singly node might be implemented as...

    ```
    public class Node<E> {
      E val;
      Node next;
    }
    ```

    and could look like:

        head -> node1 -> node2 -> ... -> nodeN -> null

2. A ```Doubly Linked List``` is implemented with nodes having references to **both** the previous and next nodes. A doubly node might be implemented as...

    ```
    public class Node<E> {
      E val;
      Node next;
      Node prev;
    }
    ```

    and could look like:

        head -> node1 <-> node2 <-> ... <-> nodeN (_tail_) -> null
        Note: 'nodeA <-> node B'means that nodeA.next = nodeB AND nodeB.prev = nodeA


3. A ```Circular Linked List``` can either be singly or doubly with the main difference being that the last element in the list's next node loops back to the head as opposed to ```null```.

    A circular singly linked list might look like:

        head -> node1 -> node2 -> ... -> nodeN -> node1 -> node2 -> ... (no end)

It is important to note that the head an tail pointers must exist at **ALL** times to prevent a memory leak and point to the correct elements after any modification. Head and tail prev/next values are different from middle nodes so make sure they are updated correctly.

#### Add / Remove Operations

Since all linked lists have a head pointer, inserting an element, if order doesnt matter, is simply a matter of inserting at the head pointer for an ```O(1)``` insertion time.

**if head == null, then...**
> head = new Node(val);

**if head != null, then...**
>newHead == new Node(val);
>newHead.nxt = head;
>head = newHead



Likewise, removing from the head means simply making ```head = head.next``` to pop off the first element and runs in ```O(1)``` insertion time.

Inserting/removing an element from the middle of the list requires traversing the list until the correct place has been found. Note that this insertion/deletin requires a pointer to the node **before** where we want to insert or delete.

**Insert x at Index i**
```
public void insert(E x, int i) {
  Node<E> curr = head;
  
  // Note the i - 1 bound
  for (int k = 0; k < i - 1; i++) {
    curr = curr++;
  }
  Node<E> newNode = new Node<E>(x);
  newNode.next = curr.next;
  curr.next = newNode;
}
```

**Remove x (Assume x Isn't in the Head)**
```
public E insert(E x, int i) {
  Node<E> curr = head;
  
  // note checking curr.next != null first
  while (curr.next != null && !curr.next.val.equals(x)) {
    curr = curr.next;
  }
  if (curr.next != null) {
    E res = curr.next.val;
    curr.next = curr.next.next;
    return res;
  }
  return null;
}
```













