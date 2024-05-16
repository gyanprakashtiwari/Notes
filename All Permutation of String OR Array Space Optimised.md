**Given an array or string print all its permutations**

**Key Observation :** Maintain visited array
### Recursive Approach

**Steps in our recursive function**
- At every index i we decide whether we want to include ith element in our current permutation
- **Base Case :** when size of current permutation is equal to size of input array we print our current permutation OR if all elements are visited and we don't have any element left to include in our array 
- Similar to [[All Permutation of String OR Array]] where we don't use visited array to use less space complexity

Code(C++)
```
void helper(vector<int>& nums, int i,  vector<vector<int>>& ans) {
	if (i == nums.size()) {
		ans.push_back(nums);
		return;
	}

	for (int j = i; j < nums.size(); j++) {

		swap(nums[i], nums[j]);
		helper(nums, i + 1, ans);
		swap(nums[i], nums[j]);

	}

}

vector<vector<int>> permute(vector<int>& nums) {
	vector<vector<int>> ans;
	vector<int> curr_ans;

	helper(nums, 0,  ans);
	return ans;
}
```

#### Time Complexity
overall --> *O(!N * N)*

#### Space Complexity
overall --> *O(N)*
extra visited array





