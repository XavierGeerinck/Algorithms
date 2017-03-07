# 1.7. Dual Pivot Quicksort
Quciksort is a really great sorting algorithm, but has as a disadvantage that it is easy to get the worst case scenario that causes a $$O(n^2)$$ performance. Because of this the Dual Pivot QuickSort has come to life that tries to overcome a lot of problems with these problematic datasets.

Remember that this is a complex algorithm if you are not used to working with algorithms, so I would recommend starting with the normal QuickSort first.

## 1.7.1. How

![Dual Pivot Quicksort](https://lh3.googleusercontent.com/-jlVq_B-UgSM/VQamEqYOaDI/AAAAAAAAKkI/yC5HWAfUULQ/s0/Screen+Shot+2015-03-16+at+10.43.32.png "Dual-Pivot Quicksort")

To start, we have 2 Pivots called *P1* and *P2*, we then divide the array in 4 parts (see figure). Important to remember is the indexes *L*, *K* and *G* which we will move during the algorithm.

**Range for our parts:**

|Part|Range|
|-|-|
|Part 1|Left + 1 → L - 1
|Part 2|L → K - 1
|Part 3|G + 1 → Right - 1
|Part 4|K → G (Not processed elements)

**Our algorithm:**

1. If PartitionSize < 17 => Use Insertion Sort
2. Pick 2 Pivots, *P1* and *P2*, mostly P1 = v[0] and P2 = v[v.size() - 1]
3. If P1 > P2, swap them
4. Foreach element in Part 4:
	1. If Element < P1 → Swap Element with v[L] and do L++ and K++
	2. If Element > P2 → Swap Element with v[G - 1] and do G--
	3. If P1 ≤ Element ≤ P2 → K++
5.  As long as K ≤ G → Repeat step 4
6. Swap P1 with last element from Part 1, Swap P2 with first element from Part 3
7. Repeat steps 1 → 6 For every part 1, 2 and 3

These are a lot of steps, but we can literally follow them and turn them into code.

For the implementation check paragraph `§1.4`.

## 1.7.2. Advantages and Disadvantages

**Advantages**

* Faster than normal QuickSort
* Less chance to hit the worst case scenario
* Requires less swaps ($$1.9 * ln(n) * n$$ average)

**Disadvantages**

* Requires more swaps ($$0.6 * ln(n) * n$$)

## 1.7.3. Performance
|Worst Case|Average Case|Best Case|
|-|-|-|
|-|-|-|

### 1.7.3.1. Worst Case

### 1.7.3.2. Average Case

### 1.7.3.3. Best Case

## 1.7.4. Implementation
### 1.7.4.1 C++ Code

> DELETE: Code

## 1.7.5. Benchmark
|&nbsp;| 100 | 1.000 | 10.000 | 100.000 | 1.000.000
|-|-|-|-|-|-|
|Random Elements|-|-|-|-|-
|Ascending Elements|-|-|-|-|-
|Descending Elements|-|-|-|-|-

## 1.7.6. Conclusion
