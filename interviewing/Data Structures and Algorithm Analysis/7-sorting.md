# Sorting

## Bucket Sort
>Time: $O(m+n)$

To sort a limited number of positive integers $a_1,\cdots,a_n$, where all is $< m$,

1. Have an array of size $m$ initialized to all 0s.
2. For each value encountered, increment the value of the corresponding index.
3. When done, print out the results.
   


## Insertion Sort
> Worst-case Time and Average-case Time: $O(n^2)$
> 
> Best-case Time: $O(n)$ - For presorted arrays

Observe: A single item is sorted by definition. Consider elements to the right of the first element unsorted. 

Idea: Maintain a growing sorted array starting with the first element from the left (which grows towards the right). Take the next element from the unsorted range, and shift it leftward into the correct position.

<details>
<summary>Code</summary>

Given an array $a$ of size $n$,
1. Track two indexes $i$ and $j$. 
2. Outer loop (incrementing): $1 <= i < n$
3. Set $val = a[i]$
4. Inner loop (decrementing): $i-1 >= j >= 0.
5. While $a[j] > val$, swap the last two elements
6. When inner loop exits, insert the value at the correct spot.

```JavaScript
function insertionSort(array) {
	for (let i = 1; i < array.length; i += 1) {
        const val = array[i];

        let j;
		for (j = i-1; val < array[j]; j -= 1) {
            array[j + 1] = array[j];
        }
        array[j + 1] = val;
    }
}
```

</details>

[Run it on replit.com](https://replit.com/@leventoz/InsertionSort)

Also see [Selection Sort](7x-sorting.md), which is similar.

<hr>

## Shell Sort (aka diminishing increment sort)
> Worst Time: $O(n^2)
> 
> Average Time: $O(n^{7/6})$ - For certain increment sequences

Idea:
- Pick an increment sequence which starts with 1. (e.g. 1, 2, 4, 8, ... or 1, 3, 5, ...)
- For each increment (in decreasing order), run a version of insertion sort of the subset of elements at indicated by that increment.

## Heap Sort
> Time: $O(n \cdot \log n )$
> 
> Uses an extra array so space requirement is doubled

1. Build a [min_heap](6%20-%20Heap.md), which takes $O(n)$ (on average)
2. Delete_Root is $O(\log n)$ --> Deleting all elements is $O(n \cdot \log n )$


## Merge Sort
> Time: $O(n \cdot \log n )$
>
> Space: $O(n)$


Uses `divide and conquer`:
1. Recursively calls itself for the left and right half of the array until 1 element
2. On the way back, merge the array pairs while sorting

Implementation:
1. Use a temporary array the same size as the input
2. In each recursion
   1. Divide the range in half, and pass the correct left/right indexes to self to process the left and the right halves. 
   2. Merge the two sides

<details>
<summary>Code</summary>

```JavaScript
function mergeSort(source) {
    const tmpArray = new Array(source.length);
	msort(source, tmpArray, 0, source.length - 1);
}	

function msort (source, tmpArray, left, right) {
	if (left < right) {
		const center = Math.floor((left + right) / 2);
		msort(source, tmpArray, left, center)
		msort(source, tmpArray, center + 1, right)
		merge(source, tmpArray, left, center + 1, right)
    }
}

function merge(source, tmpArray, left, right, rightEnd) {
    const count = rightEnd - left + 1;
	const leftEnd = right - 1;
	let tmp = left;    

    function copyFromLeft() {
        tmpArray[tmp] = source[left];
        left += 1;
        tmp += 1;
    }
    function copyFromRight() {
        tmpArray[tmp] = source[right];
        right += 1;
        tmp += 1;
    }

    // While both half has more entries to compare
	while (left <= leftEnd && right <= rightEnd) {
		if (source[left] <= source[right]) {
            copyFromLeft();
        } else {
            copyFromRight();
        }
    }

    // If the right half ended first, copy the remaining from the left
	while (left <= leftEnd) {
        copyFromLeft();        
    }

    // If the left half ended first, copy the remaining from the right
	while (right <= rightEnd) {
        copyFromRight();
    }

    // Copy it back at the correct indexes. Use rightEnd since it hasn't mutated.
    for (let i = 0; i < count; i += 1, rightEnd -= 1) {
        source[rightEnd] = tmpArray[rightEnd];
    }s
}
```

</details>

[Run it on replit.com](https://replit.com/@leventoz/MergeSort#index.js)

## Quick Sort
> Average time: $O(n \cdot \log n )$
>
> Worst time:  $O(n^2)$

Uses `divide and conquer`. Given an array $A$ of size $n$:
1. If $A$ has <= 1 elements, return.
2. Pick a pivot index $p$, where $A[p] = v$
   1. Choice of pivot affects performance. A good pivot is the median of $A[0], A[\lfloor n/2 \rfloor], A[n-1]$.
3. Partition $A - v$ such that
   1. $A_{left}$ has only values $<= v$ 
   2. $A_{right}$ has only values $>= v$
4. Return $qs(A_{left}) + v + qs(A_{right})$, where $qs$ is the recursive call to this algorithm.

<br>
<details>
<summary>Diagram of QuickSort with first element as the pivot</summary>
![QuickSort with first element as the pivot](https://s3.amazonaws.com/hr-challenge-images/quick-sort/QuickSort.png)
</details>
<br>
<details>
<summary>Implementation</summary>

1. If two elements, sort manually if needed and return. If one element, return.
2. Pick a pivot (median of three: Pick the first, last and middle elements, sort and pick the one in the middle of the three)
3. Move the pivot out of the way by swapping it out to the right - 1.
4. let $i$ = left, $j$ = right - 1 
5. $i$ moves to the right, skips over values smaller than pivot.
6. $j$ moves to the left, skips over values larger than pivot.
7. If $i$ is to the left of $j$, the items are swapped and loop continues from step #5.
8. Swap the pivot with what's pointed by $i$.
9. Call Qsort once for the left-side array of the pivot and once the right-side array of the pivot. 

Note: This is a rough explanation, click link below to see code.
</details>
<br>

[Run it on replit.com](https://replit.com/@leventoz/QuickSort#index.js)

> Quick Sort is faster [than Merge Sort] because the partitioning step can be performed in place and very efficiently.
>
> For efficiency employ a cut-off for small array sizes and leverage Insertion Sort in the algorithm.

