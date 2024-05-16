#### Recursive Approach
Suppose we have an array of size n .
for ever index *(```1 <= i <= n```)* we have 2 choices :
1. To add *```ith```* element in our current subsequence 
2. Not to add *```ith```* element in our current subsequence
3. Stop making next recursive calls if already printed a subsequence with sum k

Code(C++)
```
bool print_any_subsequences_whose_sum_is_k(vector<int> &v, vector<int> &ans, int i, int k, int curr_sum) {
	if (i == v.size()) {
		// reached the end of array where we have choosen and not choosen some of elements
		if (curr_sum == k) {
			// printing curr subsequences if current subsequences sum is equal to k
			for (auto x : ans) {
				cout << x << " ";
			}
			cout << "\n";
			return true;
		}
		return false;
	}

	// Standing at index i , we have two choices
	// Choice 1 pick current element
	ans.push_back(v[i]);
	bool pick = print_any_subsequences_whose_sum_is_k(v, ans, i + 1, k, curr_sum + v[i]);
	ans.pop_back();
	if (pick == true) {
		return true;
	}

	// Choice 2 not pick current element
	bool not_pick = print_any_subsequences_whose_sum_is_k(v, ans, i + 1, k, curr_sum);

	if (not_pick == true) {
		return true;
	}
	return false;

}
```

#### Time Complexity

For every index we have 2 options so the overall complexity will be *O(2^n) * n*

2 2 2 2 . . . n ==> *2^n*
n ==> printing a subsequence
Overall == >  *O(2^n) * n*
#### Space Complexity
O(n) stack space (in this case depth of recursion tree)

