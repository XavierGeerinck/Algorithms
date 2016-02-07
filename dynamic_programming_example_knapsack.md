# Example : Knapsack
## General analysis and formulation
In the Knapsack problem, we assume we are a thief that has a knapsack that can hold a maximum weight of $$S'$$. He now goes into a house and sees *n items* of *value $$v_i$$* and with a *weight of $$s_i$$*. Which items should the thief take to get the maximum profit?

$$solution = max(sum(values~of~subset~n~with~totalsize ≤ S))$$

**1. Identifying the sub-problems**<br />
Think of it as suffixes of items, this means what are we going to decide about item **i**? If we think about it in a normal way, then we would get that we or pick to item, or leave it. So if we pick it we get an extra value, but if we leave it we just go to the next item.

This however is NOT correct! Because we also have a constraint, which says that we can not have a weight more than the capacity **S** which our knapsack can hold.

**2. Guessing**<br />
Is item i in the subset or not? --> 2 choices

Here we can see we have 2 choices:
* Include in the subset
* Do not include in the subset

**3. Relating subproblems to a solution**<br />

$$DP(i, X) = MAX(DP(i + 1, X), DP(i + 1, X - s_i) + v_i)$$

## Coding our solution