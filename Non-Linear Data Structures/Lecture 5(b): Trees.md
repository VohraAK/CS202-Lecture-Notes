<h1 style="text-align: center;">Non-Linear Data Structures</h1>

---

So far, we have looked at data structures which store their contents **in sequence**. While this does not hamper insertion and deletion operations at the extremities much in terms of time complexity (we can always devise a better and more efficient solution), traversing and doing operations on data stored generally becomes inefficient, with a average time complexity of $\Theta(n)$. 

Non-linear data structures, such as trees and graphs, address this inefficiency, which allow for more efficient data traversal and manipulation. 

---

## Tree ADT

A tree can be recursively defined as a collection of nodes, which is either empty, or contains a **root** node connected to zero or more sub-trees by **directed edges.**

$$T(V, E)\;\;\text{consists of a set of Vertices and Edges}$$

Two nodes have **exactly** one path (sequence of edges) between them, i.e. there are no cycles between any two nodes.

$\\[25pt]$

### Terminologies
- The node at the top of the tree is called the **root** node. 
The recursive definition of a tree allows us to define roots of sub-trees, which aid us in recursive traversals.

- The **children** of a node N are the nodes connected to N directly below it. N is the **parent** of those children nodes.

- A node with no child is called a **leaf**.

- Nodes with same parents are **siblings** of each other.

- Nodes on all paths from the root to a node N are called the **ancestors** of N (including N). The nodes from N to leaves (ends of tree) are the **descendants** of N (including N).

- The number of ancestors / length of the path from a node N to the root is the **depth** of N. 
The root is at depth 0.

- The longest path from a node N to a leaf is its **height**. All leaves are at height 0.
The **depth** of the tree is equal to the depth of the deepest leaf, which is the same as its **height**.

- Nodes at the same depth form a **level** of the tree. The root is at level 0.

- **Interior nodes** are non-leaf nodes / with one or more children.

$\\[25pt]$

### Applications of Trees

Trees are great at representing *hierarchical structure*. An example of that is the filesystem of a computer, with directories linked back to their parents and which may themselves contain nested directories.

Trees are most widely used in databases, supporting inherently fast lookup, insertion, and deletion operations. For example, B-trees and their variants are used in databases to maintain sorted data and allow searches, sequential access, insertions, and deletions in logarithmic time.

Another common application is in network routing algorithms, where spanning trees are used to find the shortest path between nodes.

Trees are also used in various algorithms, such as Huffman coding for data compression, and in the representation of expressions in compilers.

