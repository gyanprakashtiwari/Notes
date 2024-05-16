#### Print all subsequences of an array

#### Recursive Approach
Suppose we have an array of size n .
for ever index *(```1 <= i <= n```)* we have 2 choices :
1. To add *```ith```* element in our current subsequence
2. Not to add *```ith```* element in our current subsequence

Code (C++)

```
// Initially currentIndex is start index and ans is empty array
// ans vector is the subsequence we are trying to form
void print_all_subsequences(int currentIndex, vector<int> &v, vector<int> &ans) {

	if (currentIndex >= v.size()) {
		// currentIndex have reached out of bound for the array
		// Now we have one of the subsequences that needs to be printed
		for (auto element : ans) {
			cout << element << " ";
		}
		cout << "\n";
		return;
	}

	// not include current element
	print_all_subsequences(currentIndex + 1, v, ans);

	// include the current element
	ans.push_back(v[currentIndex]);
	print_all_subsequences(currentIndex + 1, v, ans);
	ans.pop_back();


}
```

#### Time Complexity

For every index we have 2 options so the overall complexity will be *O(2^n) * n*

2 2 2 2 . . . n ==> *2^n*
n ==> printing a subsequence
Overall == >  *O(2^n) * n*
#### Space Complexity
O(n) stack space (in this case depth of recursion tree)

