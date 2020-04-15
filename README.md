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
        - Need to apply double AVL rotation to out balance nodes when the shape is not straight line, otherwise just use single AVL rotation 

### Time Complexity
- Insertion: O(logN) -- worst case



## Appendix
- Balance Factor: Height of right subtree - height of left subtree (BF = rh -lh)
