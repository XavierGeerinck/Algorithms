# 1.3. Selection Sort
Selection Sort is a really easy to implement sorting algorithm, due to being inefficient on large datasets this algorithm is mostly used when memory is limited.

## 1.3.1. How
Selection sort work by having a list of numbers, it then goes through the list and finds the minimum number. When we finished looping the list we swap the founder minimum number with the current index.

As an example we take the following list:

	2 9 8 3 5 6 1 0 4 7

We start at index 0, and start finding the minimal element in this sub list, which results in 0. We now swap index 0 with the index of the found minimum and get that we will swap 2 and 0 resulting into:

	0 9 8 3 5 6 1 2 4 7

Now we are at index 1 (value 9), we find the minimum value again which is at index 6 (value 1), so we swap those 2

	0 1 8 3 5 6 9 2 4 7

And we continue doing this until we have a sorted list:

	0 1 2 3 4 5 6 7 8 9

For the implementation check paragraph `§3.4`.

## 1.3.2. Advantages and Disadvantages

**Advantages**

* Uses almost no swaps! $\Theta(n)$
* No extra space required, $O(n)$

**Disadvantages**

* Not Stable
* $O(n^2)$ performance
* Not adaptive

## 1.3.3. Performance
The performance analysis is really easy for selection sort, it will always perform $n^2$ because we loop the list no matter what.

|Worst Case|Average Case|Best Case|
|-|-|-|
|O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(n<sup>2</sup>)|

## 1.3.4. Implementation
### 1.3.4.1 Pseudo Code
    for i=0, i<arraysize
    	minIdx = i
    	for j=i, j<arraysize
    		if v[j] < v[minIdx]
    			minIdx = j
    	// swap
        swap(v[i], v[minIdx])

### 1.3.4.2 C++ Code

    int minIdx;
    for (int i = 0; i < v.size(); i++) {
        minIdx = i;

        for (int j = i; j < v.size(); j++) {
            if (v[j] < v[minIdx]) {
                minIdx = j;
            }
        }

        int temp = v[i];
        v[i] = v[minIdx];
        v[minIdx] = temp;
    }

## 1.3.5. Benchmark
|&nbsp;| 100 | 1.000 | 10.000 | 100.000 | 1.000.000
|-|-|-|-|-|-|
|Random Elements|3.6e-05|0.003002|0.204347|19.3981|-
|Ascending Elements|3.1e-05|0.002846|0.190501|19.1111|-
|Descending Elements|3.5e-05|0.002114|0.205667|20.0368|-

## 1.3.6. Conclusion
We can clearly see that selection sort is a horrible sorting algorithm, however when swaps are really expensive and the memory is limited we could consider using this algorithm.
