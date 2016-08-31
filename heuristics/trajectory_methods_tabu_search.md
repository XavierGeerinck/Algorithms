# Tabu Search
Tabu Search is a heuristic that will try to find the optimal solution. It does this by using a Tabu List, where it keeps track of the most recently visited solutions and forbids moves toward them. By picking neighbor solutions, we will thus only get solutions that we did not visited before and thus improving our final result.

## Algorithm
1. Pick an initial solution and reset our "tabu list"
2. while(termination not met)
    1. Find the neighbor solutions that are not taboo, and check how good these are
    2. Pick the best neighbor and put the previous solution in the taboo list
    3. If the new solution is better, remember it