# Simulated Annealing
Simulated annealing comes from the metalwork, where they heat a metal object to make sure that there are no errors or cracks in it. After the heating process, they will then cool down the metal object in phases to prevent cracks later on.

To apply this algorithm, we start with a high temperature. This high temperature allows the algorithm to escape any local optimums (it thus accepts values worse then our current). As the temperature gets reduced, we decrease the chance of worse values being accepted. 

## Algorithm
1. Create Initial Solution *S* and set our begin temperature *T*
2. While(termination not met)
    1. Pick a new solution at random by making a small change to our current solution
    2. Do we go to this new solution? (check if acceptanceProbability(old, new, temperature) > Math.random())
    3. Decrease the temperature and continue loop