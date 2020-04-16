# data-structure-cheat-sheet

## Tree

## AVL Tree

### What it is
BST in which every node has Balance factor of 0, -1, or 1

### Algorithm
1. AVL tree Insertion:
    - Regular BST insertion
    - Update Balance Factors
    - Fix broken balance factors using AVL rotations
        - Need to apply double AVL rotation to out balance nodes when the shape is a left/right kink shape or not straight line, otherwise just use single AVL rotation 

### Time Complexity
- Insertion: O(logN) -- worst case

## Red Black Tree


### What it is
 - Characteristic:
    1. All nodes must red or black
    2. The root must be black
    3. If a node is red, then all of its children must be black. That's why it's not possible to have red node w/ red children (red -> red). However, it is possible for black node to have red / black children
    4. For every node **n**, every possible path from **n** to a null refference (does not point to anything) must have the same # black nodes
    5. null refference must be a black node
    
 - It's not an AVL Tree (red black tree != AVL tree) -- You may get invalid AVL tree when constructing the tree from red black tree
 
### Algorithm


### Time Complexity
- height: O(logn)

## Appendix
- Tree's height: The longest distance from the root of the tree to a leaf (Note: Distance in this case is # of edges in a path)
- Balance Factor: Height of right subtree - height of left subtree (BF = rh -lh)
- A balance binary tree: a tree where most leaves are equidistant from the root and most internal nodes have 2 children
- Unbalanced binary tree: a tree where many internal nodes have exactly 1 child and/or leaves are not equidistant from the root
