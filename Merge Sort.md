### Recursive Approach
**Divide & Merge**
Suppose we have an array of size n .
Divide the array into 2 parts and merge them after we have sorted two parts
1. Recursive calls will keep dividing the array . **TRUST**  the function will sort the divided parts
2. Base Case : an array of single element is already sorted




Code(C++)
```
void merge(vector<int> &v, int low, int mid, int high) {
	int i = low;
	int l1 = low, l2 = mid + 1;

	// temporary array to store merged array
	vector<int> temp(high + 1);

	while (l1 <= mid and l2 <= high) {
		if (v[l1] <= v[l2]) {
			temp[i++] = v[l1++];
		} else {
			temp[i++] = v[l2++];
		}
	}
	while (l1 <= mid) {
		temp[i++] = v[l1++];
	}
	while (l2 <= high) {
		temp[i++] = v[l2++];
	}

	// copying merged array back to original array
	for (int i = low; i <= high; i++) {
		v[i] = temp[i];
	}
}


void merge_sort(vector<int> &v, int low, int high) {
	if (low >= high) {
		// array with single element is always sorted
		return;
	}
	int mid = low + (high - low) / 2;


	merge_sort(v, low, mid);
	merge_sort(v, mid + 1, high);
	merge(v, low, mid, high);

}
```

#### Time Complexity
divide part : logn --> n , n/2, n/4, .. 1
merge part : n
overall complexity *O(n logn)*

#### Space Complexity
O(n) space to store temp array while merging two sorted arrays

