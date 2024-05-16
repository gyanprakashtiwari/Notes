### Recursive Approach
**Divide & Conquer**
Suppose we have an array of size n .
**Steps in our recursive function**
- Pick an *pivot* (any element in the array,in this case we will pick the 1st element as pivot)
- place the pivot element in its correct place in the sorted array
	- smallet on left 
	- greater on right
**Make recursive calls on left and right parts  of pivot**




Code(C++)
```
int find_partition_index(vector<int> &v, int low, int high) {
	int pivot = low;
	int i = pivot, j = high;

	// elements smaller than pivot will be in the left
	// elements greater than pivot will be to the right
	while (i < j) {
		while (v[i] <= v[pivot] and i <= high) {
			i++;
		}
		while (v[j] > v[pivot] and j >= low) {
			j--;
		}

		if (i < j) {
			swap(v[i], v[j]);
		}
	}

	swap(v[j], v[pivot]);
	return j;
}


void quick_sort(vector<int> &v, int low, int high) {
	if (low >= high) {
		// array with single element is always sorted
		return;
	}

	// get partiotion index
	int partition_index = find_partition_index(v, low, high);

	// left part
	quick_sort(v, low, partition_index - 1);
	// right part
	quick_sort(v, partition_index + 1, high);

}
```

#### Time Complexity
divide part : logn --> n , n/2, n/4, .. 1
merge part : n
overall complexity *O(n logn)*

#### Space Complexity
O(1) 

