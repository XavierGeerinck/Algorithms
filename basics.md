# 2.8 Graphs
* Abstract model
* Exists of n nodes or vertices
* Has a collection of m edges
* The nodes represent objects with connections
* Can have a direction.
* The grade of a node is the amount of neighbors of that node.
* For a graph with a direction, we have an ingrade, this is the amount of incoming neighbors. The same goes for the outgrade which is the amount of outgoing neighbours.
* 2 Basic representations of graphs:
    * Neighbor matrix: takes a connection (i,j) and represents it on a square neighbormatrix. This value can be logical or can be the weight. The problem is that matrices take a lot of memory en the initialization takes $$\Theta(n^2)$$ operations.
    * Neighbor lists: Mostly used when we do not have a lot of connections (m << $$n^2$$). In reality most graphs are like this. The neighbors of every node are saved in a neighbor list and the graph is represented by a table of n neighbor-lists.

These pictures show a normal graph, it's neighbor list and the neighbor matrix

![](Screen Shot 2015-04-02 at 13.21.33.png)![](Screen Shot 2015-04-02 at 13.21.39.png)

Looping through a graph is different then looping through a tree, this because a graph has multiple pathways and we have to find a way to only go through each path once.

