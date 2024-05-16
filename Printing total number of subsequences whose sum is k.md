#### Recursive Approach
Suppose we have an array of size n .
for ever index *(```1 <= i <= n```)* we have 2 choices :
1. To add *```ith```* element in our current subsequence 
2. Not to add *```ith```* element in our current subsequence
3. Trust  the function that it will return total number of subsequences with sum == k for all elements from *ith index to n*



Code(C++)
```
int total_number_of_subsequences_with_sum_k(vector<int> &v, int i, int k, int curr_sum) {
	if (i == v.size()) {
		// reached the end of array where we have choosen and not choosen some of elements
		if (curr_sum == k) {
			return 1;
		}
		return 0;
	}

	// Standing at index i , we have two choices
	// Choice 1 pick current element
	int pick_cnt = total_number_of_subsequences_with_sum_k(v,  i + 1, k, curr_sum + v[i]);


	// Choice 2 not pick current element
	int not_pick_cnt = total_number_of_subsequences_with_sum_k(v,  i + 1, k, curr_sum);


	return pick_cnt + not_pick_cnt;

}
```

#### Time Complexity

For every index we have 2 options so the overall complexity will be *O(2^n) * n*

2 2 2 2 . . . n ==> *2^n*
n ==> printing a subsequence
Overall == >  *O(2^n) * n*
#### Space Complexity
O(n) stack space (in this case depth of recursion tree)

