**Given an array or string print all its permutations**

**Key Observation :** Maintain visited array
### Recursive Approach

**Steps in our recursive function**
- At every index i we decide whether we want to include ith element in our current permutation
- **Base Case :** when size of current permutation is equal to size of input array we print our current permutation OR if all elements are visited and we don't have any element left to include in our array 

Code(C++)
```
void helper(vector<int>& nums, int i, vector<int>& curr_ans, vector<vector<int>>& ans, vector<bool> &visited) {
	if (curr_ans.size() == nums.size()) {
		ans.push_back(curr_ans);
		return;
	}

	for (int j = 0; j < nums.size(); j++) {
		if (visited[j] == false) {

			visited[j] = true;
			curr_ans.push_back(nums[j]);

			helper(nums, j + 1, curr_ans, ans, visited);

			visited[j] = false;
			curr_ans.pop_back();
		}
	}

}

vector<vector<int>> permute(vector<int>& nums) {
	vector<vector<int>> ans;
	vector<int> curr_ans;
	vector<bool> visited(nums.size(), false);

	helper(nums, 0, curr_ans, ans, visited);
	return ans;
}

```

#### Time Complexity
overall --> *O(!N * N)*

#### Space Complexity
N for stack space 
N for visited array
O(N) + O(N) = O(N)
overall --> *O(N)*






