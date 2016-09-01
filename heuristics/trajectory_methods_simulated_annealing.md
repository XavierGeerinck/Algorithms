# Simulated Annealing
Simulated annealing comes from the metalwork, where they heat a metal object to make sure that there are no errors or cracks in it. After the heating process, they will then cool down the metal object in phases to prevent cracks later on.

To apply this algorithm, we start with a high temperature. This high temperature allows the algorithm to escape any local optimums (it thus accepts values worse then our current). As the temperature gets reduced, we decrease the chance of worse values being accepted. 

In code we can explain this by picking a start temperature which is our probability for a value to be accepted. Then when we find a new value, if it is better we can instantly accept it, but if it is worse, we accept it with a specific probability. To explain this better, let's say we have a worse value, now we throw a dice and when it is a 1 or a 2, we accept the worse value. After each iteration this temperature now decreases and we will only accept a 1. After a while, the probability will be so low that only better values are accepted.

## Algorithm
1. Create Initial Solution *S* and set our begin temperature *T*
2. While(termination not met)
    1. Pick a new solution at random by making a small change to our current solution
    2. Do we go to this new solution? (check if acceptanceProbability(old, new, temperature) > Math.random())
    3. Decrease the temperature and continue loop