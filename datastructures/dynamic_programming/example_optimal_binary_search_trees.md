# Example : Optimal Binary Search Trees

As we saw in red-black tree and splay trees, we want to minimze the time that is needed to access a binary tree. Therefor we want to find a solution that calculates the most efficient binary tree structure, which can be done through dynamic programming.

Lets say that we have our keys that we want to get inserted in this tree in ascending order $$k_1, k_2, k_3, k_4, k_5, ...$$, and also their priorities $$p_1, p_2, p_3, p_4, p_5, ...$$ , now how can we create a BST with the lowest possible access time? Well first we have to define that the cost for finding an element _i_ in a BST on depth d = d + 1 is equal to the number of comparisons that we have to do to find that element.

Now to solve this with dynamic programming, we follow these steps:

* Take 2 tables \(1 with the sorted keys, and 1 with the priorities\)
* For every index _i_ \(where _i_ is the number of nodes that we will combine\)
  * Take every combination of elements that we can combine together. \(example, is we have 1, 2, 3 as elements and i = 2, then we can take 1,2 together and 2,3 together\).
    * Now take the sum of the probabilities of the combined elements
    * * the minimum of the longest combination possible if we take every index seperately as a root element.

## Example

| | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| V | 10 | 12 | 16 | 21 |
| P | 4 | 2 | 6 | 3 |

### i = 1

For i = 1, we see every element seperately, and thus we can write the probabilities as the diagonal of their indexes.

|  | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 4 | - | - | - |
| 1 | - | 2 | - | - |
| 2 | - | - | 6 | - |
| 3 | - | - | - | 3 |

### i = 2

For i = 2 it gets more complicated, this means that we take 2 nodes together. Let's take [0,1] together. This sum becomes: 4 + 2 = 6 and now we find the minimum if we take them bother seperately as root.

0 as root gives 2
1 as root gives 6

so the minimum is 2, add this together to our 6, becomes 8.

| | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 4 | **8** | - | - |
| 1 | - | 2 | **10** | - |
| 2 | - | - | 6 | **12** |
| 3 | - | - | - | 3 |

### i = 3

Now we take 3 elements together, so we have the following combinations:

* **[0, 2]**: Sum probabilities = 4 + 2 + 6 = 12
    * root = 0 ==> [1, 2] = 10
    * root = 1 ==> [0, 0] + [2, 2] = 10
    * root = 2 ==> [0, 1] = 8 (smallest)
    * ==> Solution: [0, 2] = 12 + 8 = 20
* **[1, 3]**: Sum probabilities = 2 + 6 + 3 = 11
    * root = 1 ==> [2, 3] = 12
    * root = 2 ==> [1, 1] + [3, 3] = 2 + 3 = 5 (smallest)
    * root = 3 ==> [1, 2] = 10
    * ==> Solution: [1, 3] = 11 + 5 = 16

| | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 8 | **20** | - |
| 1 | - | 2 | 10 | **16** |
| 2 | - | - | 6 | 12 |
| 3 | - | - | - | 3 |

### i = 4

| | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 8 | 20 | **26** |
| 1 | - | 2 | 10 | 16 |
| 2 | - | - | 6 | 12 |
| 3 | - | - | - | 3 |


