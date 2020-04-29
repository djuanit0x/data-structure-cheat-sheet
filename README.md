# data-structure-cheat-sheet
This cheat sheet helps me to prepare my exams in a [data structures class](https://github.com/djuanit0x/data-structure-cheat-sheet#appendix) and to be my reference later in case I need it in the future. 

# Important Fundamental
## Time Complexity


- Measurement how fast is your algorithm
- Algorithm performance in terms of number of operations with respect input size

### Types
1. Big-O: Upper Bound
    - f(n) is Big-O(g(n)) if A * g(n) >= f(n) as n -> infinity
2. Big-Omega: lower bound
    -  f(n) is Big-Omega(g(n)) if B * g(n) <= f(n) as n -> infinity
3. Big-Theta: Both upper and lower bound 
    - f(n) is Big-Theta(g(n)) if f(n) is O(g(n)) and f(n) is Big-Omega(g(n))
    - B * g(n) <= f(n) <= A * g(n)
## Space Complexity
measures the amount of working storage needed for an input of size n.

## Abstract Data Type

### In Short
defined by what functions it should be able to perform, but it does not at all describes on how it actually goes about doing those functions (i.e., it's not implementation-specific).

---
# Data Structures

## Array List
### Complexity
#### Time:
- Insertion: O(1) -- unsorted array list
- Find/Remove: O(N) --  unsorted array list
- Remove/Insertion: O(N) -- sorted array list
- Find: O(logN) -- sorted array list

## Linked List
### Complexity
#### Time:
- Insertion: O(1) -- unsorted linked list
- Insertion: O(N) -- sorted linked list
- find/remove: O(N) -- sorted + unsorted

## Hash Table

### In C++
- Implements the Set ADT
    - Add individual element to array (depends on implementation)
- Implements the Map ADT
    - Add (key, value) pair to hash table (depends on implementation)

### Should have
Balance factor (\# empty slots / \#total slots) should be below 0.7 to be considered as a good hash table, otherwise the hash table is a poor design ones.
### Using Hash Functions
- A function with:
    - Input: An object x
    - Output: An integer representation of x
    - **Property of Equality**:  If x is equal to y, h(x) must equal h(y)
    - **Property of Inequality**: If x is not equal to y, it would be nice (but not neccessary) if h(x) was not equal to h(y)
    - Use **prime number** to evenly spread more slots in the hash

### Collision Strategies
#### Open Addressing (Linear Probing)
When a collision occurs, linearly move to the next one until you find an empty slot
#### Double Hashing
When a collision occurs, calculate the hash function again using the **state** of the hash function after the last insertion + 1(applying linear probing)

**Note**: the design of the second hash function is deterministic (can choose what works best for you) as long as the results are a pretty random spread across the hash tables.

#### Closed Addressing (Seperate Chaining)
Use linked list when the collision occurs.

### Examples
[Birthday problem](https://en.wikipedia.org/wiki/Birthday_problem)

### Complexity
#### Time:
- Insert/remove/find O(1), but need to fist perform O(k) hash where 'k' is the length of the key -- average case
- find/remove/insert O(n) -- worst case (a lot of collisions)

## Tree
A graph without any **undirected cycles** (i.e., cycles that would come about if we replaced directed edges with undirected edges) nor any unconnected parts, so it's a **connected** graph

### Types
- Rooted
    - have an implied hierarchical structure
    - All nodes except the root have a parent
    - All nodes have either 0, 1, or 2 children
- UnRooted
    - do not necessarily have an implied hierarchical structure
    - there is no notion of parents or children. Instead, a given node has **neighbors**

### Four Traverse Algorithms (O(n) worst case)
#### Pre-order (DFS)
```
1. first visit the current node, 
    then we recurse on the left child (if one exists), 
    and then we recurse on the right child (if one exists)
2. VLR (Visit-Left-Right).
```
#### In-order (DFS)
```
1. first recurse on the left child (if one exists), 
    then we visit the current node, 
    and then we recurse on the right child (if one exists). 
2. LVR (Left-Visit-Right).
```
#### Post-order (DFS)
```
1. first recurse on the left child (if one exists), 
    then we recurse on the right child (if one exists), 
    and then we visit the current node.
2. LRV (Left-Right-Visit).
```
#### Level-order (BFS)
```
1. visit nodes level-by-level (where the root is the 
    "first level," its children are the "second level," etc.),
    and on a given level, we visit nodes left-to-right. 
2. 1st level (left to right). 2nd level(left to right), ...etc
```
## Binary Search Tree

### Properties
- Rooted Binary Tree (Tree w/ 0, 1, or 2 children)
- Every Node is larger than all nodes in its left subtree
- Every node is smaller than all nodes in its right subtree

### Algorithms
#### BST Find
```
1. Start at the root
2. If query == current => success!
3. Otherwise , if query > current, traverse right and go to #2
4. Otherwise, if query < current, traverse left and go to #2
5. If  you ever try to traverse left/right but no such child exists => fail!    
```

#### BST Insert
```
1. Perform "find" algorithm starting at root
2. If "find" succeeds, then duplicate element!
3. If "find" doesn't succeed, then insert the new element 
    at the place where the "find" algorithm fail!
```

#### BST Successor Algorithm
```
1. If the node has a right child, traverse right once, then all the way left
2. Otherwise, traverse up the tree. The first time the current node is 
    its parent's left child, the parent is our successor.
```

#### BST Remove Algorithm
```
Case 1: No Children
    Just delete the node
Case 2: 1 child
    Just directly connect my child to my parent
Case 3: 2 children
    Replace my value with my successor's value, and remove me
```

### Complexity
#### Time:
- Find/insert/remove O(logN), assuming self-balancing BST. 
- O(n) is the worst case (Perfectly unbalanced tree)
- O(1) is the best case scenario for "find" n element, when the query is the **root**
- \# comparison to find a node = depth of that node = Number of nodes in the path from that node to the root
- Average case time complexity = expected \# operation to find query = expected depth

#### Space: 
O(n) for BST with n elements

## Priority Queue
Considered a **Highest Priority, First Out**(HPIFO) data type -- The highest priority element currently in the Priority Queue is the first one to be removed.

### ADT in C++
- insert(element): Add element to the Priority Queue
- peek(): Look at the highest priority element in the Priority Queue
- pop(): Remove the highest priority element from the Priority Queue

## Heap
-  A tree that satisfies the Heap Property: For all nodes A and B﻿, if node A is the parent of node B, then node A has higher priority (or equal priority) than node B.
- Typically implements Priority Queue ADT that guarantees O(1) peeking and O(log n) insertion and removal in the worst case.

### Binary Heap
Heap that are binary trees with three contraints:
- **Binary Tree Property**: All nodes in the tree must have either 0, 1, or 2 children
- **Heap Property**: For all nodes A and B﻿, if node A is the parent of node B, then node A has higher priority (or equal priority) than node B.
- **Shape Property**: A heap is a complete tree. In other words, all levels of the tree, except possibly the bottom one, are fully filled, and, if the last level of the tree is not complete, the nodes of that level are filled from left to right

#### Types of Binary Heap
- **A min-heap** is a heap where every node is smaller than (or equal to) all of its children (or has no children). 
- **A max-heap** is a heap where every node is larger than (or equal to) all of its children (or has no children). 

#### Algorithm
Insert (assuming it's a max-heap )
```
1. place element in next open slot (as defined by a "complete tree")
2. while element has a parent and element.priority > element.parent.priority:
3.     swap element and element.parent
```
Pop (assuming it's a max-heap)
```
1. replace the root with the rightmost element of the bottom level of the tree (call it "curr")
2. while curr is not a leaf and curr has lower priority than any of its children:
3.    swap curr and its highest-priority child
```

#### Complexity
##### Time:
- **Insert/Pop** is O(log n) as the shape the Binary heap are guaranteed perfectly balanced binary tree
- O(1) worst-case time complexity for **peeking** at the highest-priority element.
    
## Treap 

### What it is
- tree + heap
- BST with respect to **keys**
    - For any nodes the keys are larger than all keys in the left subtree and smaller than all keys in the right subtree
- Heap property with respect to priorities
- The heap propery of any nodes must be larger than all priorities below

### Algorithm
#### Treap Insertion
``` 
1. Insert via BST insertion algoritm with respect to keys
2.    Use AVL rotations to "bubble up" to fix heap with respect to priorities
```
### Ramdomized Search Tree
- It's special type of **treap** where, instead of us supplying both a key and a priority for insertion, we only supply a key, and the priority for the new (key, priority ) pair is **randomly** generated for us

#### Algoritm
##### find
```
perform BST find based on key
```
##### insert
```
1. priority = randomly generated integer
2. perform Treap insert based on (key, priority)
```

##### remove
```
perform Treap remove based on key
```



### Complexity
#### Time:
- Insertion: O(logN) -- average case
- Insertion: O(N) -- worst case (Linked list)
## AVL Tree

### What it is
BST in which every node has Balance factor of 0, -1, or 1

### Algorithm
1. AVL tree Insertion:
    - Regular BST insertion
    - Update Balance Factors
    - Fix broken balance factors using AVL rotations
        - Need to apply double AVL rotation to out balance nodes when the shape is a left/right kink shape or not straight line, otherwise just use single AVL rotation 

### Complexity
#### Time:
- Insertion: O(logN) -- worst case

## Trie

### What it is
Tree structure in which elements are represented by **paths**
If the tries have more than 2 children, you can call the tries as **Multiway Tries**

### Algorithm

- Multiway Tries insertion:
    - Start at root node, and for each letters for the word that you want to insert. 
        - Check if the current node has a child edge label by that letter. 
            - if it does not.
                - I need to create a new child edge labeled by that letter, then traverse down to that next child edge to continue. 
            - Finally, the moment you finish inserting a word, you have to mark the last node as a word node.
- Multiway Tries find:
    - Start at root node, and for each letters for the word that you want to find. 
        - need to check does my current node have a child edge labeled by that letter 
            - If it does, traverse it until the last letter to iterate.
            - If it doesn't, it fails to find the world -- the word does not exists in the tries.
    - return true if you manage to find the word at **the last letter**, otherwise returns false
 - Multiway Tries remove:
    - Start at root node, and for each letters for the word that you want to remove. 
        - need to check does my current node have a child edge labeled by that letter 
            - If it does, traverse it until the last letter to iterate.
            - If it doesn't, it fails to remove the world -- the word does not exists in the tries.
    -  Remove the last node, with the edge containing the last letter of the word that you want to remove. The remove is failed if **the last letter** is not a word or it does not contain the word.
                
### Complexity
#### Time:
- find/remove/insert: O(n) where n is the length of the longest word -- worst case  
    - Length of longest word = #edges // Worst case scenario for MWT

## Red Black Tree


### What it is

 - It's a **BST** with following characteristic:
    1. All nodes must red or black
    2. The root must be black
    3. If a node is red, then all of its children must be black. That's why it's not possible to have red node w/ red children (red -> red). However, it is possible for black node to have red / black children. 
        - Need to switch color if parent is black and all of children are red
        - If the parent is red and its children are red do AVL rotation + coloring
    4. For every node **n**, every possible path from **n** to a null refference (does not point to anything) must have the same # black nodes
    5. null refference must be a black node
    
 - It's not an AVL Tree (red black tree != AVL tree) -- You may get invalid AVL tree when constructing the tree from red black tree

### Algorithm
1. Red black tree tree Insertion:
    - In general cases:
        - Perform regular BST insertion
            - If you see a black node w/ 2 red children, recolor all 3: 1 red parent w/ 2 black children.
                - if the parent is the root, color it black
        - Color new node **red**
        - Potentially fix tree for red black tree properties
    - 1st case: empty tree
        - Insert the new node as the root
        - Color it black
    - 2nd case: child of black node
        - Just insert. No need to change anything
    - 3rd case: Child of red node, **straight line**
        - Insert -> single (left/right) AVL rotation w/ grand parent node -> recolor
    - 4nd case: Child of red node, kink shape
        - Rotate to make straight line, then do **straight line insertion case (3rd case)** 
    - Important Notes
        - Only coloring when traversing to insert the tree -- fixing the tree color only the way down.
        - When inserting a node, nodes with invalid color do not have to be fixed or recolor if the nodes are not visited
    

### Complexity
#### Time:
- height: O(logn)


## Tenary Search Tree (TST)

### What it is
- A type of trie, structured in a fashion similar to **BST**. 
- Unlike BST, \# children is up to **three children**: a middle child, left child, and right child. 
- Serves as **a middle-ground between** the BST and the Multiway Trie (MWT) in terms of memory usages and time complexity of operations. 

### Algorithm
1. TST Find:
    - Steps: 
        - If current node = root, then c = first letter of query
        - If c > current node's letter:
            - Traverse to right child
        - Else if c < current node's letter:
            - Traverse to left child
        - Else: // Equal
            - If c is the last letter of query and current node is a **word** node:
                - Success!!!
            - Else:
                - Traverse to the middle child and go to the next letter in the query.
        - **The word is not exist** in the TST tree If you reach here, but can't still find the word.

2. TST Insert:
    - Similar to **find** algorithm
    - When performing TST find algorithm
        - If you ever need to traverse to a child that does not exist, simply create a new child and traverse to it.
        - Then, just need make the last node in the traversal a **word** node.
4. TST Remove:
    - Similar to **find** algorithm
        - The difference is after performing TST Find algoritm
        - Make the last node in the traversal **not a word node**
        - Failed to remove if the find is failed or the last node is not a word node
### Complexity
#### Time: 
- Insert/find/remove: O(n) -- worst case -- when the word is sorted
    - (length of your alphabet + 1)*length of word // worst case for TST (**need to check**)
- Insert/find/remove: O(logn) -- average case


# Appendix [A-Z]
- **balance binary tree**: a tree where most leaves are equidistant from the root and most internal nodes have 2 children
- **Balance Factor**: Height of right subtree - height of left subtree (BF = rh -lh)
- **Depth of a Node in BST**: Number of nodes in the path from that node to the root.
- **Graph**: a collection of nodes (or vertices) and edges connecting these nodes
- **Height of a node in BST**: Longest distance (#edges) from node to a leaf
- **Height of a tree in BST**: Height of the root of the tree
- **Tree's height**: The longest distance from the root of the tree to a leaf (Note: Distance in this case is # of edges in a path)
- **Unbalanced binary tree**: a tree where many internal nodes have exactly 1 child and/or leaves are not equidistant from the root

---
All notes mainly come from a [data-stucture class](https://ucsd-cse100-s20.github.io/), that I took in spring 2020 and my own experience.

Access to online textbook from the couse is [here](https://stepik.org/course/579/syllabus).

Watch class videos is [here](https://www.youtube.com/watch?v=rhpyqL5D7K0&list=PLM_KIlU0WoXmkV4QB1Dg8PtJaHTdWHwRS).
