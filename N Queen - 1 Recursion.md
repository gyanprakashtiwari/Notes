**Given an chess board of side n and place n queen such that the queens don't attack each other  **


### Recursive Approach

**Steps in our recursive function**
- At every column from left we decide for all rows in that cols if it is safe to place the queen and place it accordingly and make recursive call for next col
- **Base Case :** when we have filled all cols than our current board is answer

Code(C++)
```

bool is_safe(int row, int col, vector<string> &board, int n) {

	int R = row;
	int C = col;

	// check 3 direction if placing at current position attacks any previously placed queen
	row--; col--;
	// 1.north west diagonal
	while (row >= 0 and col >= 0) {
		if (board[row][col] == 'Q')return false;
		row--; col--;

	}
	row = R, col = C - 1;
	// 2.west horizontal
	while (col >= 0) {
		if (board[row][col] == 'Q')return false;
		col--;

	}
	row = R + 1, col = C - 1;
	// 3.south-west diagonal
	while (row<n and col >= 0) {
		if (board[row][col] == 'Q')return false;
		row++; col--;
	}

	// otherwise it is safe
	return true;




}

void helper(int col, vector<string> &board, vector<vector<string>> &ans, int n) {
	if (col == n) {
		ans.push_back(board);
		return;
	}

	for (int row = 0; row < n; row++) {

		if (is_safe(row, col, board, n)) {
			// place queen at board[row][col]
			board[row][col] = 'Q';
			helper(col + 1, board, ans, n);
			// remove placed when returing from recursion
			board[row][col] = '.';
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


	helper(0, board,  ans, n);
	return ans;
}

```

#### Time Complexity
overall --> *O(N * N * N)*

#### Space Complexity
*N * N for stack space*
N * N for current board
overall --> *O(N * N)*







