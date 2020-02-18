# Depth First Search

This is analog to recursive searching in a tree. We start at any node and we continue forward. It also keeps a log of the already visited nodes so we do not visit them twice. On the end we discover the remaining nodes.

DFS is used to solve problems that have one solution, such as finding the way out of a maze.

```cpp
void DFSUtil(int i) {
    discovered[i] = true;

    for (every neighbor j of node i) {
        if (!discovered[j]) {
            check_node(j);
        }
    }
}

void DFS() {
    // No nodes discovered
    for (int i = 0; i < n; i++) {
        discovered[i] = false;
    }

    // Go through each node
    for (int i = 0; i < n; i++) {
        if (!discovered[i]) {
            check_node(i); // start a new tree
        }
    }
}
```

The output of DFS can be expressed as a spanning tree. Based on this we can divide the original graph into several classes:

![](https://github.com/thebillkidy/algorithms/tree/533511c54f9f1e2a083d31e7c68f99d66637058b/412px-Tree_edges.svg.png)

* **Forward Edges**: Point from node to a descendant.
* **Back Edges**: Points from node to an ascendant.
* **Cross Edges**: Points to neither.
* **Tree Edges**: Appears sometimes, belongs to the spanning tree and are classified separately from forward edges.

## Performance:

The performance is determined by how the graph is represented:

* Θ\(n\) operations on initialisation
* We start searching from where we stopped, so Θ\(n\) for the second for.
* We discover every node once, Θ\(n\)

We get Θ\(n + m\) for neighbor and Θ\(n + m2\) = Θ\(n2\) for the neighbor matrix.

