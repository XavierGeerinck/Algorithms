# Variants
## B+-tree
A B-tree has a few disadvantages:
* It has to reserve place for leafs, even if they are not used
* Searching for a successor requires a lot of write operations

That is why we got B+-trees, these save the data in the leafs instead of in the nodes, and uses the nodes as indexes. The other main difference is that they also link the leafs together so that we can scan the keys linearly instead of going through each level.

The performance of a B+-tree is almost the same as a normal B-tree.

![](/images/datastructures/b_trees_+.png)

## Prefix B+-tree

If the keys are strings, then a normal b-tree asks a lot of space. Therefor we can save the strings as the prefixes of the distinct strings to save room.

![](/images/datastructures/b_trees_prefix.png)

## B*-tree

A normal B tree delays splitting by moving items to its neighbors, if these are full, then it will split the node in 2 parts that are filled for 50%.

A B*-tree will divide the keys of the neighbor and the node over 3 different nodes. This way they are filled for 2/3th each.

This has as advantage that the search time is smaller.