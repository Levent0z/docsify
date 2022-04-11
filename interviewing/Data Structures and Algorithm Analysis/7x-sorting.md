# More on Sorting 

## Radix Sort
Note: This section is from Chapter 3.2.

This is a generalization of [Bucket Sort](7-sorting.md) and should be used when the range of values to be sorted is too many (i.e. too many buckets). Instead, there can be multiple passes on a small number of buckets.

For example:
1. Have 10 buckets with linked lists (because multiple values can fall in a bucket).
2. Iterate $p$ times, where $p$ is the number of digits of the largest number.
3. In each pass, place the values in the correct bucket based on the current **least-significant** digit (starting from the least, moving towards the more significant digit).

> Time: $O(p(n + b))$ where $b$ is the number of buckets.

## Selection Sort
Note: This section is not from the book.

> Time: $O(n^2)$

Idea: Find the minimum in the "current range" in the array, (which gets smaller in each iteration). Move the current minimum to the right of the previous.

<details>
<summary>Code</summary>

Given an array $a$ of size $n$,
1. Track two indexes $i$ and $j$. 
2. Outer loop: $0 <= i < n-1$, assume $a[i]$ is minimum.
3. Inner loop: $i+1 <= j < n$. If $a[j]$ < minimum, $a[j]$ becomes the new minimum.
4. When inner loop exits, swap $a[i]$ with min. 

```JavaScript
function selectionSort(array) {
	for (let i = 0; i < array.length - 1; i += 1) {
		let minIndex = i;
		let val = array[minIndex];
		
		for (let j = i;  j < array.length; j+= 1) {
			if (array[j] < val) {
				minIndex = j;
				val = array[j];
            }
        }
				
		tmp = array[i];
		array[i] = val;
        array[minIndex] = tmp;
    }
}
```

</details>

[Run it on replit.com](https://replit.com/@leventoz/SelectionSort#index.js)


[Selection Sort vs. Insertion Sort](https://cheetahonfire.blogspot.com/2009/05/selection-sort-vs-insertion-sort.html)