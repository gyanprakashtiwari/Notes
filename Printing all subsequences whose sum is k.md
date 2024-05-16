#### Recursive Approach
Suppose we have an array of size n .
for ever index *(```1 <= i <= n```)* we have 2 choices :
1. To add *```ith```* element in our current subsequence 
2. Not to add *```ith```* element in our current subsequence

Code(C++)
```
void print_all_subsequences_whose_sum_is_k(vector<int> &v, vector<int> &ans, int i, int k, int curr_sum) {
	if (i == v.size()) {
		// reached the end of array where we have choosen and not choosen some of elements
		if (curr_sum == k) {
			// printing curr subsequences if current subsequences sum is equal to k
			for (auto x : ans) {
				cout << x << " ";
			}
			cout << "\n";
		}
		return;
	}

	// Standing at index i , we have two choices
	// Choice 1 pick current element
	ans.push_back(v[i]);
	print_all_subsequences_whose_sum_is_k(v, ans, i + 1, k, curr_sum + v[i]);
	ans.pop_back();

	// Choice 2 not pick current element
	print_all_subsequences_whose_sum_is_k(v, ans, i + 1, k, curr_sum);

}
```

#### Time Complexity

For every index we have 2 options so the overall complexity will be *O(2^n) * n*

2 2 2 2 . . . n ==> *2^n*
n ==> printing a subsequence
Overall == >  *O(2^n) * n*
#### Space Complexity
O(n) stack space (in this case depth of recursion tree)

