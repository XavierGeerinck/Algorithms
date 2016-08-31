# Randomized Search Trees

Randomized search trees use a random generator to neutralise the effect that the order of operations has. The trees stay random, even after every operation.

A common example is the _treap_

## Treap

A treap is a combination of a heap and a tree, every node in this tree gets a priority and a key. These keys are sorted by the heap condition rule which says that the priority of the child should be &lt;= priority of the parent.

The performance of a Treap is O\(log\(n\)\) but its worse than the previous trees \(red-black, splay, ...\) but easier to implement.

Example:

### Operations

* **Search:** Is identical to the BST searching
* **Insert:** Make a new node with a random priority p and add it as you would in a BST. Now fix the heap property.
    * If the parent p > node p --> rotate to make the node parent
    * Repeat this until the heap condition is applied
* **Remove:** 
    * Remove as in a BST
        * 0 children: remove
        * 1 child: swap with child and remove
        * 2 children: swap with inorder successor (right subtree most left child) and repeat
    * Sometimes a swap can nvalidate the heap property, that's why we have to perform extra rotations sometimes

### Example

![](/images/datastructures/treap.png)

