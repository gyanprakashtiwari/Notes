**Given a set of numbers return list of sorted numbers . these numbers are sum of all subsets of the given set**
### Recursive Approach

**Steps in our recursive function**
- At every index i we have 2 choices to pick or not pick current element
- TRUST : the function will fill all subset sums in range *1<=i<=N* in array ans
- finally we sort the ans array and return


Code(C++)
```
void helper(vector<int> &arr, int N, int i, int sum, vector<int> &ans) {

	// base case
	if (i == N) {
		ans.push_back(sum);
		return;
	}
	// choices
	// pick
	helper(arr, N, i + 1, sum + arr[i], ans);
	// not pick
	helper(arr, N, i + 1, sum, ans);

}


vector<int> subsetSums(vector<int> arr, int N) {
	vector<int> ans;

	helper(arr, N, 0, 0, ans);

	sort(ans.begin(), ans.end());
	return ans;
}
```

#### Time Complexity
At every index we have 2 choices - 2^n 
for sorting subset_sum array *2^nlog(2^n)*
overall --> *O(2^n + 2^nlog(2^n))*

#### Space Complexity
overall --> *O(n)*





