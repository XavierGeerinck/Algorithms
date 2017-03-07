## 2.8.2. Breadth-first search (BFS)
### General
Start by exploring the nodes at a given depth before proceeding to the next level. This means that we will explore the children of nodes before we proceed to the children of the children. 

This is useful when we want to find the minimal path length solution, if one exists. The disadvantage is that we need to traverse the complete tree which results in a lot of nodes.

### Algorithm
BFS Uses a queue structure to hold all unexplored nodes. The order in which nodes are placed on the queue determine the type or search.

1. Place root node s on the queue
2. If queue is empty. return false and stop
3. If first element on the queue is a goal node g. Return success and stop otherwise.
4. Remove and expand the first element from the queue and place all the children at the end of the queue in any order.
5. Return to step 2

![](200px-Breadth-first-tree.svg.png)

### PseudoCode

**Input:** Graph G, Vertice of G called v.

**Output:** All vertices reachable from v labeled as discovered.

    procedure BFS(G,v) is
          let Q be a queue
          Q.enqueue(v)
          label v as discovered
          while Q is not empty
             v ← Q.dequeue()
             for all edges from v to w in G.adjacentEdges(v) do
                 if w is not labeled as discovered
                     Q.enqueue(w)
                     label w as discovered
                     
### Implementation
```c++
void Graph::BFS(int sourceNode, int numberOfVertices) {
    // Mark all vertices as not explored
    bool *explored = new bool[numberOfVertices];

    for (int = 0; i <= numberOfVertices; i++)
        explored[i] = false;
        
    // Create the queue for BFS
    list<int> queue;
    
    // Push root vertex to the queue
    queue.push_back(sourceNode);
    explored[sourceNode] = true; // Of course we have explored this one already
    
    // Use an iterator to get all adjacent vertices of a vertex
    list<int>::iterator i;
    
    while (!queue.empty()) {
        // Dequeue a vertex and print it
        sourceNode = queue.front();
        std::cout << sourceNode << " ";
        
        // Get all adjacent vertices of the dequeued vertex sourceNode
        // If a adjacent has not been explored, then mark it visited 
        // and enqueue it
        // list<int< *adj;
        for (i = adj[sourceNode].begin(); i!= adj[s].end(); ++i) {
            if (!explored[*i]) {
                explored[*i] = true;
                queue.push_back(*i);
            }
        }
    }
```
                     
### Classes
We can divide the connections into classes as we did with DFS:

* TreeNode: Connection with undiscovered node
* BackEdge: Connection with ascendant.
* CrossEdge: Connection with no ascendants and descendants.

> We can not have forward edges, this because we start from a root node and go downwards.

### Applications
BFS has many applications, some of them are:

* Testing a graph for it's bipartiteness.
* Finding loops in undirected graphs.
* Finding the shortest path between 2 nodes u and v.

### Performance

* Initialisation: $$\Theta(n)$$
* We put elements on queue and dequeue them, these operations are O(1), so we get $$\Theta(n)$$
* We go through each neighbor, this is $$\Theta(n)$$ for the neighbor lists and $$\Theta(n^2)$$ for the neighbor matrix.

So depending on the way we represent the graph we get $$\Theta(n + m)$$ for the list and $$\Theta(n^2)$$ for the matrix.