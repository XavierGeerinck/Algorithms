# Red-Black Trees

## General

* Allows us to do all operations \(Access, Search, Insertion, Deletion\) in O\(log\(n\)\) time.
* Is based on a BST \(=Binary Search Tree\) with a color bit
* Preferred over a AVL tree if we need to do more insertions and deletions

### Properties

* Every node is black or red
* The leafs of the tree \(nil's\) are **black**
* Red nodes can not have a red parent- or child
* Every path from a node to a "descendent" \(nil node\) has the same amount of black nodes, we call this the **"black-height"**

We try to keep these properties by using _rotation_ or _recoloring_

### Rotation

* We can rotate left or right, this text is for right rotation
* Take I as the new root
* Make the original right child \(β\) the left child of the new right child \(P = old root\)
* Left rotation is symmetrical

![Left Right Rotation](../images/datastructures/trees_red_black_rotation.png)

### Bottom-Up Insertion

Every time we insert a node, we will set its color to red and the root node to black, this because the root always has to be black. Now follow these steps:

**Legend:** N = new node, S = sibling of N, P = parent, U = uncle of parent, G = grandparent

1. Insert as you would in a BST tree, but make the new node = red \(so if &gt; go right, if &lt; go left\)
2. If P is NOT BLACK or N is not the root
  1. U is red

  * Make U and P black
  * Make G red
  * Repeat from G

  1. U is black

    * Left Left Case \(P is left child of G and N is left child of P\)
    * Right Rotate G and Switch colors P and G
    * Left Right Case \(P is left child of G and N is right child of P\)
    * Left Rotate P --&gt; Back to the Left Left case

  2. N is root, set color to black

> Note that these cases are always symmetrical to each other! so we could have a Right Right case and a Right Left case as well.


| **Left Left Case** | **Left Right Case** |
| --- | --- |
| ![](/images/datastructures/trees_red_black_insert_left_left_case.png) | ![](/images/datastructures/trees_red_black_insert_left_right_case.png) |

> A good way to study this, is to try this yourself on paper for the series: 1,2,3,4,5,7,6

### Bottom-Up Deletion

**Legend:** N = new node, S = sibling of N, P = parent, U = uncle of parent, G = grandparent

For deletion, we will now start as we would in a BST. This means, find the node by going down the tree and look at its children:

* no children: just delete the node
* 1 child: Swap the child with its parent and delete the new child
* 2 children: Swap the child with its inorder successor \(most left node in the right subtree\)

Whenever we remove a child from the tree, we have to decrease the color of the leaf by one.

* For a red color, this becomes black \(so nothing special has to be done\)
* A black color however, becomes a _double black_ color. Which means we will have to fix this in the tree with the cases below:

| Case 1: Sibling = RED | Case 2: Sibling = BLACK & has 2 BLACK childs |
| --- | --- |
| Rotate S over P and recolor S & P, then go to another case ![](/images/datastructures/trees_red_black_deletion_case1.png) | Make S RED, P now absorves the double black \(so if P was red, then we are done; else repeat from P which is now double black\) ![](/images/datastructures/trees_red_black_deletion_case2.png) |
| Case 3: Sibling = BLACK & Right child is RED | Case 4: Sibling = BLACK & Right child is BLACK and left child is RED |
| Rotate S over P and swap their colors. Make the right child of S black. ![](/images/datastructures/trees_red_black_deletion_case3.png) | Rotate S its left child over S and swap their colors. Now go to case 3. ![](/images/datastructures/trees_red_black_deletion_case4.png) |

> Learning this can be quite tricky since the cases are alike. We can however see that all the cases have to do with looking at a sibling! 1x sibling black and 2x sibling black, the last case is a special one with only the sibling and a red left child.

### Top-Down Insertion

**Legend:** N = new node, S = sibling of N, P = parent, U = uncle of parent, G = grandparent

Top down insertion is more efficient then Bottom Up, because now we will be restructuring the tree on our way down, instead of going down first and then back up.

To do this, we will look at the parent and the children first. If these 2 children are red, then we reverse the colors of the 3 nodes (parent and children). However if we have a red parent and a red grandparent, then we reorganize the tree.

Now we can have the same 2 cases as we could have in the Top-Down algorithm:

| **Left Left Case** | **Left Right Case** |
| --- | --- |
| Rotate right over G and swap P and G its colors ![](/images/datastructures/trees_red_black_insert_left_left_case.png) | Rotate left over P first and afterwards right over G, now swap N and G its colors ![](/images/datastructures/trees_red_black_insert_left_right_case.png) |

### Top-Down Deletion

**Legend:** N = new node, S = sibling of N, P = parent, U = uncle of parent, G = grandparent

