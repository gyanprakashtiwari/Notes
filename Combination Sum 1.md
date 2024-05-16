**Suppose we have an array of size n and a value target we want to print/return all combinations of numbers selected from array which has sum=target .**
### Recursive Approach

**Steps in our recursive function**
- At every index i we have 2 choices to pick or not pick *ith element* 
- for next recursive calls we can stay at *ith index* until the current can be included
- **Base Case** : reached the end of array (in which we have picked some elements 1 or multiple times and not picked some elements)



Code(C++)
```
void helper(vector<int> &candidates, int i, int target, vector<int> &curr_ans, vector<vector<int>> &ans) {
	if (i == candidates.size()) {
		if (target == 0) {
			ans.push_back(curr_ans);
		}
		return;
	}

	// two choices
	// pick
	if (target >= candidates[i]) {
		curr_ans.push_back(candidates[i]);
		helper(candidates, i, target - candidates[i], curr_ans, ans );
		curr_ans.pop_back();
	}
	// not pick
	helper(candidates, i + 1, target, curr_ans, ans );

}


vector<vector<int>> combinationSum(vector<int>& candidates, int target) {

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




