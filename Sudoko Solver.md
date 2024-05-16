**Give a  9 * 9 sudoko board filled with numbers 1 to 9 . which consists of 9, 3 * 3)small boards . which has some empty cells , Find one valid sudoko solved board**
**The conditions for the board to be solved are :**
- The digits 1 - 9 occurs only once in every row
- The digits 1 - 9 occurs only once in every col
- The digits 1 - 9 occurs only once in every 3 * 3 small board

### Recursive Approach

**Steps in our recursive function**
- Trying to fill up empty cells with numbers 1 - 9 if possible
- Base Case : there are no empty cells to be filled return true
- 
Code(C++)
```
bool isValid(vector<vector<char>>& board, int num, int r, int c) {
	char ch = '0' + num;
	for (int i = 0; i < 9; i++) {
		if (board[r][i] == ch)return false;
		if (board[i][c] == ch) return false;
		if (board[3 * (r / 3) + i / 3][3 * (c / 3) + i % 3] == ch)return false;
	}
	return true;

}

bool helper(vector<vector<char>>& board) {


	for (int row = 0; row < 9; row++) {
		for (int col = 0; col < 9; col++) {
			if (board[row][col] == '.') {
				for (int num = 1; num <= 9; num++) {
					if (isValid(board, num, row, col)) {
						board[row][col] = '0' + num;
						if (helper(board))return true;
						else board[row][col] = '.';
					}

				}
				return false;
			}
		}
	}
	return true;

}

void solveSudoku(vector<vector<char>>& board) {

	bool found = helper(board);
	// bool found = true;

	if (found) {
		for (int i = 1; i <= 9; i++) {
			for (int j = 1; j <= 9; j++) {
				cout << board[i - 1][j - 1] << " ";
			}
			cout << "\n";
		}
	}

}


```


#### Time Complexity
overall --> *O(N * N )* --> O(1) since n=9 which is constant

#### Space Complexity








