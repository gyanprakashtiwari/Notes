**Suppose we have an array of size n and a value target we want to print/return all unique combinations of numbers selected from array which has sum=target and the resultant list of lists will be sorted**

**Key Observation**  : Generate all combinations with target as sum then we can observe out of all combinations if we want only unique combinations, starting element of all combinations of equal length will be unique
### Recursive Approach

**Steps in our recursive function**
- At every index i we pick only first occurence of all elements from which our curr_ans(subsequence with sum=target) will start
- **Base Case** : target =0 , we want to select some numbers with target=0, here base case is different from [[Combination Sum 1]] because at an index i we are deciding our current subsequence will start from which number 
- *TRICK :*  How to make recursive calls so that our current pick element is unique



Code(C++)
```
void helper(vector<int> &candidates, int i, int target, vector<int> &curr_ans, vector<vector<int>> &ans) {
	if (target == 0) {
		ans.push_back(curr_ans);
		return;
	}


	// curr ans should start with only unique values of candidates
	for (int j = i; j < candidates.size(); j++) {
		if (j > i and candidates[j] == candidates[j - 1])continue;
		if (candidates[j] > target)break;

		curr_ans.push_back(candidates[j]);
		helper(candidates, j + 1, target - candidates[j], curr_ans, ans );
		curr_ans.pop_back();
	}

}


vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
	sort(candidates.begin(), candidates.end());
	vector<int> curr_ans;
	vector<vector<int>> ans;
	helper(candidates, 0, target, curr_ans, ans);

	return ans;

}
```

#### Time Complexity
At every index we have 2 choices - 2^n 
but we can select ith element multiple times say t
Average length of combination generated is k
overall --> *O(2^t * k)*


#### Space Complexity
It depends on number of combinations
k is average length of combination
x is average number of combinations

overall --> *O(k * x)*




