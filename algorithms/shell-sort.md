# 1.2. Shell Sort
Shellsort is a more refined version of insertion sort. This algorithm will change our array from completely random unsorted data to partially sorted data so that insertion sort may work faster.

## 1.2.1. How
This algorithm works by using increments, the increments can be found [here](http://en.wikipedia.org/wiki/Shellsort). For this Article I will make us of the increment $N/2^k$.

What we do with the increments is we keep applying it till we get 1 as an increment, once we have 1 we know we are using the last insertion sort.

Let's take this array as an example:

	6 7 8 2 3 1 2 9 4 0 1 7 8 9 5 0

we now know that our N = 16, and the first increment therefor becomes: 8. We now split our array in 2

	6 7 8 2 3 1 2 9
	4 0 1 7 8 9 5 0

Once we did that, we sort the columns:

	4 0 1 2 3 1 2 0
	6 7 8 7 8 9 5 9

And we go to the next increment (here that is 8 / 2 = 4) and sort.

	4 0 1 2   =>   3 0 1 0
	3 1 2 0   =>   4 1 2 2
	6 7 8 7   =>   6 7 5 7
	8 9 5 9   =>   8 9 8 9


Next increment = 2

	3 0        1 0
	1 0        2 0
	4 1        3 1
	2 2        4 2
	6 7   =>   5 7
	5 7        6 7
	8 9        8 9
	8 9        8 9

Next increment is our last increment = 1

	1        0
	0        0
	2        1
	0        1
	3        2
	1        2
	4        3
	2        4
	5   =>   5
	7        6
	6        7
	7        7
	8        8
	9        8
	8        9
	9        9

Which sorted the complete array.

For the implementation check paragraph `§3.4`.

## 1.2.2. Advantages and Disadvantages

**Advantages**
* Requires $O(1)$ extra space
* Performance of $O(n^{7/6})$ for the best currently known sequence
* $O(n * lg(n))$ when almost sorted.

**Disadvantages**
* Not stable

## 1.2.3. Performance
|Worst Case|Average Case|Best Case|
|-|-|-|
|$O(n^{7/6})$|-|$O(n * log^2(n))$|

### 1.2.3.1. Worst Case
The performance of ShellSort depends on the used gap sequence, because the best gap sequence is not yet known. We are unable to say which the best case is. Currently one of the best gap sequences is the one of Tokuda (1992): $k_i = \frac{9^5 - 4^k}{5 * 4^{k - 1}}$ with a performance of $O(n^{7/6})$.

## 1.2.4. Implementation
### 1.2.4.1 Pseudo Code
When we watch `§1.1` we know how the algorithm works, so we write down what we will need:

1. Get initial increment
2. Use insertion sort with rebased indexes

This means our pseudocode is the same as the one for Insertion Sort, only with the difference of the gap index.

### 1.2.4.2 C++ Code

    int k = v.size() / 2; // Initial increment

    while (k >= 1) {
        // Split the vector in columns, loop through each column
        for (int col = k; col < v.size(); col++) {
            int j = col - k; // Gap sequence back, we get the other elements of the columns
            int temp = v[col]; // Get the element we are sorting

            // Perform Insertion sort
            while (j >= 0 && temp < v[j]) {
                v[j + k] = v[j]; // Make sure to take the index of the elements in the columns based on the gap!
                j -= k; // Go to the next element
            }

            v[j + k] = temp; // And on the end of course place the element once we found the spot
        }

        k /= 2; // Next increment
    }

## 1.2.5. Benchmark
|&nbsp;| 100 | 1.000 | 10.000 | 100.000 | 1.000.000
|-|-|-|-|-|-|
|Random Elements|1.2e-05|0.000191|0.002876|0.041843|0.565456
|Ascending Elements|4e-06|6e-05|0.000892|0.011036|0.12966
|Descending Elements|7e-06|9.1e-05|0.001226|0.015739|0.178499

## 1.2.6. Conclusion
When we have to use a fast algorithm that is easy to implement, and the performance that we require is not ultimate. Then Shell Sort is the facto standard to use.
