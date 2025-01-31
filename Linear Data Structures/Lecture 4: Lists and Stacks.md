<h1 style="text-align:center">Linear Data Structures</h1>

---

## List ADT

>A series of entries $A_0, A_1, A_2, \dots, A_{n-1}$ of size $N$.

Lists can be implemented by creating **arrays** or **linked lists**.

```c
template <typename T>
...
public:
    virtual void add(const T& ele) = 0;
    virtual void insertAt(int index, const T& ele) = 0;
    virtual void removeAt(int index) = 0;
    virtual void get(int index) const = 0;
    virtual void size() const = 0;
    virtual ~List()
    // its a good practice to create a virtual destructor for proper object lifetime management
```
$\\[25pt]$


### Implementation #1: Creating fixed-size arrays:

#### Pros
- Traversing an array is $O(1)$ in time complexity.
- A fixed-sized array requires no additional space for any pointers or metadata, hence it is space efficient for smaller programs.
- Since arrays are typically stored contiguously in memory, processors can efficiently access and store data in memory without complex jumps.


#### Cons
- Since the array is pre-allocated, its size is unmodifiable.
- Accessing out-of-bounds elements may result in undefined behavior.
- Large contiguous allocations for bigger and more complex programs is spatially inefficient.


One solution is to use **dynamic arrays**, which resize to $2N$ whenever the array runs out of space. One disadvantage is the increase in worst-case time complexity from $O(1)$ to $O(n)$ during insertion, where the program resizes the array when full and then inserts the element.

$\\[25pt]$

### Implementation #2: Creating a linked-list:

A series of nodes, linked sequentially together using references to the next and / or previous node.

#### Node structure

```c++
template <typename T>
class Node
{
private:
    T data;
    Node* next;
public:
    Node() : data(NULL), next(nullptr) {}
    Node(T e) : data(e), next(nullptr) {}
    T getData() const { return data; }
    Node* getNext() const { return next; }
    void setData(Node* node) { next = node; }
};

template <typename T>
class List
{
private:
    Node* head;
    size_t size;

public:
    List() : size(0), head(nullptr) {}
    size_t getSize() const { return size; }
    void insert(T loc, T val);
    void insertAtHead(T val);
    void insertAtTail(T val);
    void remove(T loc);
};
```
$\\[20pt]$

#### Pros:

- Since the size of the linked list is dynamic, it can grow and shrink a per application requirements.
- A linked list does not require contiguous memory; nodes can be scattered throughout memory but are linked together at the program level using references.
- Efficient data operations, including insertions, deletions and relocation.
- A linked list is the foundation of complex data structures, such as stacks and queues.


#### Cons

- Storing 8-bit references (for x86-64 machines) add performance overheads.
- Since a linked list is sequential by nature, data cannot be accessed directly.
- Programs implementing linked list can become complex when catering to different application requirements; some applications may require custom implementations.

$\\[25pt]$

> **Note**: Major implementations will be omitted, see attached PDF.

$\\[25pt]$

#### Efficiency Problems:

1. Insertions and deletions at the end of a singly linked list takes $\boxed{O(n)}$ time, since the list needs to be traversed till the `next` of the current node becomes `nullptr`, i.e. the end of the list.
Solution: A `tail` pointer can be used to point to the last node in the list which helps reduce the time complexity of `insertAtEnd()` and `deleteFromEnd()` to $\boxed{O(1)}$

2. Due to there being only a reference for the *next* node, a singly list cannot be traversed backwards.

$\\[25pt]$

### Other Types of Linked Lists:
$\\[25pt]$

#### Doubly Linked List:

A linked list supporting both forward and reverse iterations, having a `prev` as well as a `next` reference to nodes in the list.
$\\[20pt]$


#### Circular Linked List:

A linked list where the *last* element in the list points to the *first* element in the list, enabling endless iterations through the list without going out of bounds.



---
## Stack ADT

A structure where elements are *pushed* and *popped* from the same end of the line. In other words, a stack is a "Last In, First Out" data structure.

It has a lot of uses, mainly in a function call hierarchy, expression and syntax parsing, undo/redo operations in word processors, and browser history.

```c++
template <typename T>
class Stack
{
// usually inherits underlying structure from a parent ADT
public:
    virtual void push(const T& ele) = 0;
    virtual T pop() = 0;
    virtual T top() = 0; // return the top most element without removing it
    virtual bool isEmpty() const  = 0;
    virtual size_t size() const = 0;
    virtual ~Stack() {}
};
```
$\\[25pt]$


Like above, a stack can be implemented using **arrays** or **linked lists**; each approach has its merits and advantages.

$\\[25pt]$

### Considerations:

Since elements are being pushed and popped to and from the stack, data operations can result in:

1. **Underflow**: An empty stack is popped, leading to undefined behavior. 
Throw an **exception** when `pop()` is called when the stack is empty.

2. **Overflow**: A stack exceeds allocated capacity when a new element is pushed.
For an array-based approach, **dynamic sizing** helps to prevent overflows.

$\\[25pt]$


### Implementation #1: Using arrays:

For efficiency, the last element added to an array should be pushed at index $n$, and popped from index $n-1$; essentially, "top of the stack" (TOS) should be the last element index-wise. 

`push` and `pop` hence occur in $O(1)$ time, rather than $O(n)$ for TOS at index $0$.

$\\[25pt]$


### Implementation #2: Using linked lists:

For a singly linked list, TOS should ideally be at `head` / `push` and `pop` occurs from `head`, for $O(1)$ time complexity. If TOS was instead at the end of the singly linked list, `push` and `pop` would need to traverse the entire list for data operations, hence having an $O(n)$ complexity.

$\\[15pt]$
> **Note**: If we had access to a `tail` pointer for a singly linked list, having TOS at `tail` would make `push` run in $O(1)$ **but** `pop` would still run in $O(n)$ time, since `tail` alone does not have information about the second-in-line node in the list, and the algorithm would have to traverse the entire list to update `tail` to the previously second-in-line node.
> A doubly linked list having a `prev` pointer for each node would solve that problem and could improve `push` and `pop` to $O(1)$.

