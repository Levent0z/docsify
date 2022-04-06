# Sorting

## Bucket Sort
>Time: $O(m+n)$

To sort a limited number of positive integers $a_1,\cdots,a_n$, where all is $< m$,

1. Have an array of size $m$ initialized to all 0s.
2. For each value encountered, increment the value of the corresponding index.
3. When done, print out the results.
   


## Insertion Sort
> Time: $O(n^2)$

Given an array $a$ of size $n$,
1. Track two indexes $i$ and $j$. 
2. Outer loop: $0 <= i < n-1$, assume $a[i]$ is minimum.
3. Inner loop: $i+1 <= j < n$. If $a[j]$ < minimum, $a[j]$ becomes the new minimum.
4. When inner loop exits, swap $a[i]$ with min. 

```JavaScript
function insertionSort(array) {
	for (let i = 0; i < array.length - 1; i += 1) {
		let minIndex = i;
		let val = array[minIndex]
		
		for (let j = i;  j < array.length; j+= 1) {
			if (array[j] < val) {
				minIndex = j
				val = array[j];
            }
        }
				
		tmp = array[i]
		array[i] = val
        array[minIndex] = tmp
    }
}
```
[Run it on replit.com](https://replit.com/@leventoz/InsertionSort)

## Shell Sort
> Time: $O(n^{7/6})$

## Heap Sort
> Time: $O(n \cdot \log n )$

1. Build a [min_heap](6%20-%20Heap.md), which takes $O(n)$ (on average)
2. Delete_Root is $O(\log n)$ --> Deleting all elements is $O(n \cdot \log n )$

## Quick Sort
> Time: $O(n \cdot \log n )$

## Merge Sort
> Time: $O(n \cdot \log n )$

Uses `divide and conquer`:
1. Recursively calls itself for the left and right half of the array until 1 element
2. On the way back, merge the array pairs while sorting


```JavaScript

```
[Run it on replit.com](https://replit.com/@leventoz/MergeSort#index.js)

