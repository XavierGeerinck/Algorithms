# Example : Fibonacci
## General Analysis & Formula
To illustrate the steps above, we will apply them to one of the easiest problems out there. The Fibonacci problem. In the Fibonacci problem, our goal is to find the **n'th** Fibonacci number, where the solution is given by the sum of the 2 previous numbers. 

Let's write this out as a formula

$$Fib(n) = Fib(n - 2) + Fib(n - 1)$$

## Bad Code
If we would write this formula in a bad code practice, then we would get something like this (javascript code).


```javascript
function fib(n) {
    if (n <= 1) return n;
    return fib(n - 2) + fib(n - 1);
}

console.log(fib(25));
```

Now why is this bad? Well let's start with an analysis of the problem. The run time for this is going to be in a recursive way so for `Fib(n)` our solution will be the sum of the time needed for `Fib(n - 2)` and `Fib(b - 1)`. Here we also add the time needed to add them together which is `O(1)`.

$$T(n) = T(n - 1) + T(n - 2) + O(1)$$<br />
$$T(n) ≥ 2T(n - 2)$$<br />
$$T(n) = Θ(2^{n/2})$$

Which is bad! Let's improve this by using our Dynamic Programming approach.

## With Dynamic Programming
So every time we need to calculate a problem, check if we already computed the problem, if not then calculate it. This technique is the bottom-up approach which will use "memoization".

```javascript
var memo = {};

function fib(n) {
    if (memo[n]) return memo[n];
    if (n <= 1) return n;
    var f = fib(n - 2) + fib(n - 1);
    memo[n] = f;
    return f;
}

console.log(fib(25));
```

Now, what is our gain here? Well this time we use almost no recursion. Since every time when we look for a value, we check if it is in our memo table. If it is, then we will use it, giving back a `Θ(1)` performance.

This means for `n` numbers, that we will have a `Θ(1)` performance, so resulting in a total run time of: `Θ(n)` which is way better than our previous implementation.

1. Define Subproblems<br />
