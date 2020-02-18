# B-Trees

B-Trees are a continuation on the 2-3 trees, with every node pointing towards a datablock. These trees have some special properties:

* They have a magnitude m
* The amount of keys is dependant on this magnitude
  * the root can have between 1 and m - 1 keys.
  * a node can have between \(m/2\) - 1 and m - 1 keys.
* Every leaf is on the same level
* The max amount of child nodes at a node is the \#maximum\_number\_of\_keys + 1
* Every key of a B-Tree is ordered ascending

Node properties:

* Every node has a number k that shows the current number of keys in the node
* It has a table with maximal m pointers towards children of the node
* It has a table for maximal m - 1 keys sorted ascending
* It has a boolean showing if it's a leaf or not

The performance of a B-tree is O\(log n\) for searching, removal and insertion. Because these operations are a bit more length than normal trees, they are explained in the subsections below.

## Searching

Searching is the easiest case in a B-tree, to search we just work our way down by following the pointers towards the child nodes.

> Note that a pointer towards a child node is inbetween 2 values. For example if we want to go to a child with the key 5, we would need to find the pointer between 4 and 6.

## Insertion

To insert a new element, we have to find the place where we want to insert it. Once we found this place, we need to check the number of elements:

If the number of elements currently in the node + 1 &lt; maximum elements allowed, then we can insert a new node without problems.

However when we want to add an element to a node that is full, then we have to split it. To split this node, we take the _median_ of the elements, and put this as our new parent node. Then we put all the values smaller in a new left node and all the other values in the new right node.

> Note that since we put the median in the parent element that this can also create a split, so make sure to recursively check this.

![](../../.gitbook/assets/b_trees_insertion.png)

## Removal

Removing a node is a little bit harder than inserting one since we have to take merging into account. To remove a node, we first where it should be removed. Now we replace the node with its inorder successor and remove the node.

This removal can cause a underflow, because the minimum amount of elements should be equal to m/2. To fix this we need to borrow an element from one of the siblings, or remove the leaf if borrowing is not possible. See the examples below for more information on how this works.

![](../../.gitbook/assets/b_trees_removal1.png) ![](../../.gitbook/assets/b_trees_removal2.png)

## Examples

* B-tree of magnitude 4
  * The number of keys is between 2 and 3
* B-tree of magnitude 6
  * The number of keys is between 3 and 5
* B-tree of magnitude 5
  * The number of keys is between 2 and 4

> Now try this yourself and insert the keys: 1, 2, 3, 4, 5, 6 for a B-tree with magnitude m = 3

