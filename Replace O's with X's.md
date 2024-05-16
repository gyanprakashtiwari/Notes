[Problem](https://www.geeksforgeeks.org/problems/replace-os-with-xs0052/1)


Given a matrix **mat** of size **N x M** where every element is either 'O' or 'X'. Replace all 'O' or a group of 'O' with 'X' that are surrounded by 'X'.

A 'O' (or a set of 'O') is considered to be surrounded by 'X' if there are 'X' at locations just below, just above, just left and just right of it.
### Draft thoughts
#### Initial approach 
go dfs on each O while traversing
if ->any of the O is at boundary return false meaning this set of O's cannot be changed to X's
else -> mark the dfs from that traversal as X at every cell with O

Steps : 
- 2 dfs calls at every cell with O
- first to find out if all its connected O's can be changed to X
- second to actually change all connected O's to X if first dfs returns true
##### Better approach
maintain 2 matrices  visited(n * m)  
start DFS from all boundary O's and call DFS all connected mark them visited(i,j)=true

Now finally makr all cells as X where it was O and visited(i,j)=false


### Algorithm

- if any one of O of a set of O's at the boundary then that set of O's can never be surrounded by X in all four direction(east, west, north, south)
### Observation
- clicking the idea of the solution is main thing here

```
int dx[4] = {0, 0, 1, -1};
int dy[4] = {1, -1, 0, 0};
void dfs(int n, int m, int r, int c, vector<vector<char>> &mat, vector<vector<bool>> &vis) {
	vis[r][c] = true;

	for (int i = 0; i < 4; i++) {
		int row = r + dx[i];
		int col = c + dy[i];
		if (row >= 0 and row<n and col >= 0 and col < m) {
			if (!vis[row][col] and mat[row][col] == 'O') {
				dfs(n, m, row, col, mat, vis);
			}
		}
	}

}
vector<vector<char>> fill(int n, int m, vector<vector<char>> mat) {
	vector<vector<bool>> vis(n, vector<bool> (m, false));

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (i == 0 or i == n - 1 or j == 0 or j == m - 1) {
				if (!vis[i][j] and mat[i][j] == 'O') {
					dfs(n, m, i, j, mat, vis);
				}

			}
		}
	}

	vector<vector<char>> ans = mat;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (vis[i][j] == false and ans[i][j] == 'O') {
				ans[i][j] = 'X';
			}
		}
	}
	return ans;
}

```








Space Complexity

SC --> O(N * M) 




Time Complexity
TC --> O(N * M) + O(N)

TC --> O(N * M) 
