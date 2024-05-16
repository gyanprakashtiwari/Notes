**Given an chess board of side n and place n queen such that the queens don't attack each other  **


### Recursive Approach

**Steps in our recursive function**
- Optimised Version of [[N Queen - 1 Recursion]]
- At every column from left we decide for all rows in that cols if it is safe to place the queen and place it accordingly and make recursive call for next col
- is_save function is optimised by using hashing by removing while loops 
- **Base Case :** when we have filled all cols than our current board is answer

Code(C++)
```
void helper(int col, vector<string> &board, vector<vector<string>> &ans, int n, vector<int> &west, vector<int> &north_west, vector<int> &south_west) {
	if (col == n) {
		ans.push_back(board);
		return;
	}

	for (int row = 0; row < n; row++) {

		if (west[row] == 0 and north_west[n - 1 + col - row] == 0 and south_west[row + col] == 0) {
			// place queen at board[row][col]
			board[row][col] = 'Q';
			west[row] = 1;
			north_west[n - 1 + col - row] = 1;
			south_west[row + col] = 1;
			helper(col + 1, board, ans, n, west, north_west, south_west);
			// remove placed when returing from recursion
			board[row][col] = '.';
			west[row] = 0;
			north_west[n - 1 + col - row] = 0;
			south_west[row + col] = 0;
		}

	}

}

vector<vector<string>> solveNQueens(int n) {
	vector<vector<string>> ans;

	vector<string> board(n);
	string s(n, '.');

	for (int i = 0; i < n; i++) {
		board[i] = s;
	}

	vector<int> west(n, 0);
	vector<int> south_west(2 * n - 1, 0);
	vector<int> north_west(2 * n - 1, 0);


	helper(0, board,  ans, n, west, north_west, south_west);
	return ans;
}

```

#### Time Complexity
overall --> *O(N * N )*

#### Space Complexity
*N * N for stack space*
N * N for current board
overall --> *O(N * N)*







