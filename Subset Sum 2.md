**Given a set of numbers print all unique subsets of the given set**

**Key Observation :** Generate all subsets of given set and now the unique ones will always start with unique element for a given length
### Recursive Approach
**Non Optimal Approach**
- same as [[Subset Sum 1]]
- but we store our ans in a set of vectors instead vector of vector this will ensure all unique subsets
- **ISSUE** : TC --> *O(2^n)m * log(m)*
	- where m = *2^n log(2^n)*
	
**Steps in our recursive function**
- sort the initial input array so that all equal elements come close to each other
- TRICK : similar to [[Combination Sum 2]]
- at every index when we are choosing current element we make sure that we choose only first occurrence of every unique number


Code(C++)
```
void helper(vector<int>& nums, int i, vector<int>& curr_ans, vector<vector<int>>& ans) {

	ans.push_back(curr_ans);

	for (int j = i; j < nums.size(); j++) {
		if (j > i and nums[j] == nums[j - 1])continue;

		curr_ans.push_back(nums[j]);
		helper(nums, j + 1, curr_ans, ans);
		curr_ans.pop_back();
	}


}


vector<vector<int>> subsetsWithDup(vector<int>& nums) {
	vector<vector<int>> ans;
	vector<int> curr_ans;

	sort(nums.begin(), nums.end());

	helper(nums, 0, curr_ans, ans);

	return ans;
}
```

#### Time Complexity
At every index we have 2 choices - 2^n 
adding curr_ans to ans - k
overall --> *O(2^n  *  k)*

#### Space Complexity
overall --> *O(2^n * k)*
k -- > average length of subset





