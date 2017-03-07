# 2.9. Dictionaries
Dictionaries are structures that make it easy to find values based on keys.

## 2.9.1. Direct Addressable Table
We can use a key to access and set a value in a dictionary. If multiple values have the same key then we will use a LinkedList.

Every operation here is O(1).

## 2.9.2. Unordered table.
### 2.9.2.1. Searching
We perform a linear search over the complete dictionary to find the value we are looking for. This has a performance of O(n).

### 2.9.2.2. Adding
This happens on the back of the dictionary, so the performance is O(1).

### 2.9.2.3. Removing
We first search for the key and then we can just remove this line. This results in a performance of O(1) for removing. Note that searching has a separate performance.

## 2.9.3. Table ordered by search chance
Here we will order the table by the chance of searching, we can do this when we know the different chances of a key being searched. This will improve our performance.

## 2.9.4. Ordered table
We order the table, for example in top down order. We now have several operations:

### 2.9.4.1. Sequential Search
This method is faster if we want to know if an element appears in the table, this because when a value is bigger then our current then we can stop searching. This method however is not faster if we found the value, which is why we use the other methods more.

### 2.9.4.2. Binary Search
Compare the key we are looking for with the key of the middle element. Now we look further in the left or right sub table. This gives us a performance of $$O(lg(n))$$.

```c++
int binary_search(int s, const vector<int> &v) {
    // v is not empty
    // if found, return index
    // if not found, return -1
    int l = 0, r = v.size() - 1;
    
    // Invariant: v[l] <= s <= v[r]
    while (l < r) {
        int m = l + (r - l) / 2; // l <= m < r
        
        if (s <= v[m]) 
            r = m;
        else
            l = m + 1;
    }
    
    return s == v[l] ? l : -1;
}
```

For some specific problems there are more efficient variants:

* **Searching in cyclic ordered sequence:** if we compare 2 elements xl and xr with each other, if xl < xr then i is not l < i <= r because xi is the smallest element. If xl > xr then i has to be l < i <= r. By choosing l and r correctly we are able to eliminate 50% of the elements. This causes the algorithm to have a performance of $$O(lg(n))$$.
* **Searching in ordered sequence of unknown length:** Let's say we have to find element y in a ascending ordered sequence of unknown length. Now we first search for an element that is not < than y. We also compare y with x1, if y <= x1, than y can only be equal to x1. If not then we compare y with x2, en after that with x4, x8, ... Now we are doubling the range so that we go past y fast. Now we just need $$\Theta(lg(j))$$ equations to find index j for y <= xj.

### 2.9.4.3. Interpolation Search
We are going to search a uniform sorted array by estimating the next position to check based on linear interpolation of the search key and the values at the ends of the search interval.

The average run time for this is $$O(log(log(n)))$$

#### Adding elements
When we found the place we can add the element by moving 50% of the table. Performance here is $$O(n)$$.

#### Removing elements
As with adding elements we will have to move 50% of the table. So also $$O(n)$$.

## 2.9.3. List
### 2.9.3.1. Unordered List
* **Searching:** Sequential, so O(n)
* **Adding:** At front, so O(1)
* **Removing:** After searching this is O(1)

### 2.9.3.2. List ordered by search chance
The best order here is descending chance order. If we don't know this then we try to find the optimal order dynamically by switching a found key with it's predecessor (transpose). Or by moving it to the front (move to front). The first way is better but the second way is faster.

### 2.9.3.3. Ordered list
* **Searching:** Ordering only improves the average search time, but the performance stays O(n)
* **Adding:** We have to go through the list this time, so this becomes O(n)
* **Removing:** Same as adding.