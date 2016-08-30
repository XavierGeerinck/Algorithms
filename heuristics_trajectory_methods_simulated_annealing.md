# Simulated Annealing
Simulated annealing comes from the metalwork, where they heat a metal object to make sure that there are no errors or cracks in it. After the heating process, they will then cool down the metal object in phases to prevent cracks later on.

To apply this algorithm, we start with a high temperature. This high temperature allows the algorithm to escape any local optimums (it thus accepts values worse then our current). As the temperature gets reduced, we decrease the chance of worse values being accepted. 

## Algorithm
1. Create Initial Solution
2. While(termination not met)
    1. Pick  