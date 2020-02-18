# Radix Exchange Sort

Radix Exchange sort is a sorting algorithm that works by looking at the key. This algorithm has a performance of $$O(b*N)$$.

## 1.8.1. How

We will first get the first bit of every integer in the array, after that we will sort the array by the left most bit. Once we did that we will split the array in 2 positions and repeat this recursively.

So summarised this is:

```text
1          0
1          0
0    =>    1
1          1
0          1
```

Partition the array:

```text
0
0

1
1
1
```

And repeat, ignoring the left most bit.

For the implementation check paragraph `§8.4`.

## 1.8.2. Advantages and Disadvantages

**Advantages**

* Very fast

**Disadvantages**

* Limited use cases

## 1.8.3. Performance

| Worst Case | Average Case | Best Case |
| :--- | :--- | :--- |
| - | - | - |

## 1.8.4. Implementation

### 1.8.4.1 C++ Code

[http://www.cs.princeton.edu/courses/archive/spr02/cs226/lectures/radix.4up.pdf](http://www.cs.princeton.edu/courses/archive/spr02/cs226/lectures/radix.4up.pdf)

> DELETE: Code

## 1.8.5. Benchmark

|  | 100 | 1.000 | 10.000 | 100.000 | 1.000.000 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Random Elements | - | - | - | - | - |
| Ascending Elements | - | - | - | - | - |
| Descending Elements | - | - | - | - | - |

## 1.8.6. Conclusion

