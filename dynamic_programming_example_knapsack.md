# Example : Knapsack
## General analysis and formulation
In the Knapsack problem, we assume we are a thief that has a knapsack that can hold a maximum weight of S'. He now goes into a house and sees *n items* of *value v_i* and with a *weight of s_i*. Which items should the thief take to get the maximum profit?

```
solution = max(sum(values of subset n with totalsize ≤ S))
```

###1. Subproblems?
Suffix i: of items

###2. Guessing
Is item i in the subset or not? --> 2 choices

Here we can see we have 2 choices:
* Include in the subset
* Do not include in the subset

> We however also add a constraint stating the **remaining capacity x** that we can use and which we can not exceed the total weight s_i.

This will result in the following formula, which basically says that when we do not take the item, we will just check the next item with our remaining capacity. If we however do take the item, then we will go to the next item, but state that the current remaining capacity has decreased by the weight of the current item s_i and that the value of our sack has increased by the value of our current item v_i.

```
DP(i,S) = max(DP(i + 1, X), DP(i + 1, X - s_i) + v_i)
```

This will give us a running time of `Θ(n * S)`, which we will consider as a *pseudopolynomial time* because S is going to be small and is not going to be exponential, but still worse than polynomial.
### Coding our solution