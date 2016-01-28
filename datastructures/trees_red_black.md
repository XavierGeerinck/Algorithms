# General
* A red-black tree makes sure that all operations can happen in **O(lg n)** time
* It's based on a Binary Search Tree (BST) with a color bit.
* Properties
    * Every node is black or red
    * The root and the leaves are black
    * A red node can not have a red parent or a red child
    * Every path from a known node to a descendant leaf has the same amount of black nodes (= black-height) [<sup>[1]</sup>](https://youtu.be/iumaOUqoSCk?t=609)