# Red-Black Trees
## General
* Allows us to do all operations (Access, Search, Insertion, Deletion) in O(log(n)) time.
* Is based on a BST (=Binary Search Tree) with a color bit
* Preferred over a AVL tree if we need to do more insertions and deletions

### Properties
* Every node is black or red
* The leafs of the tree (nil's) are **black**
* Red nodes can not have a red parent- or child
* Every path from a node to a "descendent" (nil node) has the same amount of black nodes, we call this the **"black-height"**

We try to keep these properties by using *rotation* or *recoloring*

### Rotation
* We can rotate left or right, this text is for right rotation
* Take I as the new root
* Make the original right child (β) the left child of the new right child (P = old root)
* Left rotation is symmetrical

![](trees_red_black_rotation.png)
### Recoloring


