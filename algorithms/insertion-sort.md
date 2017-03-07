# 1.1. Insertion Sort
Insertion sort is the core algorithm to know, it is also the easiest to understand and implement. The disadvantages however are that it is horribly slow. The recommendation is to use this algorithm when you are sorting really small tables (< 10). Insertion Sort is also used as the base for more advanced algorithms (merge-sort, quick-sort).

## 1.1.1. How
We have a sorted part and a unsorted part in our array. The sorted part will grow as we loop through our elements in the unsorted part.

For every element from the unsorted part. shift the sorted part elements one to the right as long as they are bigger than the element from the unsorted part.

Let's say we have the following array. We put a  `|` as a divider for the sorted array (left part) and the unsorted array (right part)

```
| 40 21 13 7 1 0
```

We now start sorting every element on the right side, so take 40 now. There are no elements in the unsorted part, so we can just move it over.

```
40 | 21 13 7 1 0
```

The next element to sort is 21, we check the unsorted array and we see that 40 is there, 40 is > 21, so we move 40 one place up.

```
x 40 | (21) 13 7 1 0
```

Now there is a room to put 21, so let's put 21 there.

```
21 40 | 13 7 1 0
```

Now we do the same for the other elements

```
0 1 13 17 21 40 |
```

and this is Insertion sort. For the implementation check paragraph `§1.4`.

## 1.1.2. Advantages and Disadvantages
**Advantages**
* Easy to implement
* O(n) performance when almost sorted
* O(1) Extra space
* Low overhead
* Stable

**Disadvantages**
* O($n^2$)

## 1.1.3. Performance
|Worst Case|Average Case|Best Case|
|-|-|-|
|O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(n)

The above table is the analysis of the algorithm, but how do we get to this?

### 1.1.3.1. Worst Case
The worst case is when the array is in the descending order. We then have to move the element, and the other elements.

$$
1 + 2 + ... + n - 1 = \frac{(n - 1)n}{2} = \frac{1}{2}(n^2 - n) ∈ Θ(n^2)
$$
### 1.1.3.2. Average Case
Here every input is equally likely,  which results in:

$$
\frac{1 + 2 + ... + i + i}{i + 1} = \frac{\frac{i(i + 1)}{2} + i}{i + 1} = \frac{i}{2} + \frac{i}{i + 1} = \frac{i}{2} + (1 - \frac{1}{i + 1}) = \frac{(n - 1)n}{4} + n - H_n ∈ Θ(n^2)
$$


### 1.1.3.3. Best Case
The best case is when we have an array in ascending, then we just keep moving elements. Resulting in a `O(n)` performance.

## 1.1.4. Implementation
### 1.1.4.1 Pseudo Code
Implementing algorithms is always something risky. If we make 1 mistake in the code then we will end up with a non functional algorithm. This is why we always have to think it through, work it out on paper and then write the code!

When we watch `§1.1` we know how the algorithm works, so we write down what we will need:

1. A loop to go through our elements
2. A temporary key to remember the element we are moving
3. Another loop that will loop through or sorted array, and move the elements one to the right when needed.

Once we identified these points we can start writing pseudo code. Pseudo code should be short and easy to remember and re-create.


	for i in array

		// Save the temporary element
		temp = array[i]

		// Create a key that points to the previous index
		// (we need to check if we have to shift)
		int j = i - 1;

		// Now we need to move the elements to the right if they are bigger
		while (j >= 0 && array[j] > temp) {
			array[j + 1] = array[j]; // Shift right
			j--; // Go one element back
		}

		// last but not least, fill in the temp on the position that we found
		array[j + 1] = temp;


### 1.1.4.2 C++ Code
Now when we got the pseudo code we can easily convert this to the code that we need.  In my case this is C++.

	void insertionSort(vector<v> &v) {
		for (int i = 0; i < v.size(); i++) {
			// Save the temporary element
			T temp = v[i];

			// Create a key that points to the previous index
			// (we need to check if we have to shift)
			int j = i - 1;

			// Now we need to move the elements to the right if they are bigger
			while (j >= 0 && v[j] > temp) {
				v[j + 1] = v[j]; // Shift right
				j--; // Go one element back
			}

			// last but not least, fill in the temp on the position that we found
			v[j + 1] = temp;
		}
	}

## 1.1.5. Benchmark
|&nbsp;| 100 | 1.000 | 10.000 | 100.000 | 1.000.000
|-|-|-|-|-|-|
|Random Elements|2.4e-05|0.002049|0.13619|12.2835|-|
|Ascending Elements|1e-06|1e-05|7.4e-05|0.000705|-|
|Descending Elements|4.5e-05|0.003895|0.247554|24.8399|-|

## 1.1.6. Conclusion
We can see that Insertion Sort is a easy to implement algorithm and the benchmarks confirm that we have indeed a $O(n^2)$ algorithm here. Therefor we can also confirm that it is better to use this algorithm only when we need to sort small lists.
