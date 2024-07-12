
**Given an string s . partition s such that every substring of the partition is palindrome . Return all possible palindrome partition of s**

### Recursive Approach

### My Idea (Wrong):
n = size of string
for every length 1 to n
check if all partitions of length l is palindrome

### Correct Approach:

**Steps in our recursive function**
- At every index i try to decide if i can partition here or not . i can only partition here if current partitioned string is palindrome
	- save current string in curr_ans and call recursion on substring to right 
- **Base Case :** when i reaches end of substring now my curr_ans has all substrings of s that are palindrome
- 
Code(C++)
```
bool check(string s) {
	bool ans = true;
	int L = 0, R = s.size() - 1;
	while (L <= R) {
		ans &= (s[L] == s[R]);
		L++;
		R--;
	}
	return ans;
}
void go(int idx, string s, vector<vector<string>>& ans,
        vector<string>& curr) {
	if (idx == s.size()) {
		ans.push_back(curr);
		return;
	}
	for (int i = idx; i < s.size(); i++) {
		string left = s.substr(idx, i - idx + 1);
		if (check(left)) {
			curr.push_back(left);
			go(i + 1, s, ans, curr);
			curr.pop_back();
		}
	}
}
vector<vector<string>> partition(string s) {

	vector<vector<string>> ans;
	vector<string> curr;
	go(0, s, ans, curr);
	return ans;
}

```


#### Time Complexity
overall --> *O(2^N)*

#### Space Complexity
N for stack space 
N for visited array
O(N) + O(N) = O(N)
overall --> *O(N)*






