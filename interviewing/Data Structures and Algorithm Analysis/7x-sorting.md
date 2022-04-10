# More on Sorting 
This section is not from the book.

## Selection Sort
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