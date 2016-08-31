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
### Bottom-up
To code our solution we can again think of the top down way and the bottom up way. Let us start with the top-down way since this will explain us properly on how the solution works. So for the base case (which is on 0 items and total capacity of 0) this will return 0 (maximum value that we can put in our knapsack).

Now for the rest of the cases we will just go through the solutions. Every time making sure that we do not exceed our total capacity W.

```javascript
// Knapsack (Max Capacity, values, weights, number of items)
function knapSack(S, v, s, n) {
    // Our base case
    if (n == 0 || S == 0) {
        return 0;
    }
    
    // If the n'th item > capacity S, do not include
    if (s[n - 1] > S) {
        return knapSack(S, v, s, n - 1);
    }
    // Return max if item included or not
    else {
        return Math.max(v[n - 1] + knapSack(S - s[n - 1], v, s, n - 1), knapSack(S, v, s, n -1));
    }
}

var v = [60, 100, 120];
var s = [10, 20, 30];
var S = 50;
var n = v.length;
console.log(knapSack(S, v, s, n));
```

### Top-Down
```javascript
function knapSack(S, v, s, n) {
    var K = [[]];
    
    for (var i = 0; i <=n; i++) {
        for (var w = 0; w <= S; w++) {
            if (!K[i]) {
                K[i] = [];
            }
            
            if (i == 0 || w == 0) {
                K[i][w] = 0;
            } else if (s[i - 1] <= w) {
                K[i][w] = Math.max(v[i - 1] + K[i - 1][w - s[i - 1]], K[i - 1][w]);
            } else {
                K[i][w] = K[i - 1][w];
            }
        }
    }
    
    return K[n][S];
}

var v = [60, 100, 120];
var s = [10, 20, 30];
var S = 50;
var n = v.length;
console.log(knapSack(S, v, s, n));
```