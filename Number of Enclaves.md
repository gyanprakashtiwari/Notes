[Problem](https://www.geeksforgeeks.org/problems/number-of-enclaves/1)

You are given an **n x m** binary matrix **grid**, where **0** represents a sea cell and **1** represents a land cell.

A move consists of walking from one land cell to another adjacent (4-directionally) land cell or walking off the boundary of the grid.

Find the number of land cells in **grid** for which we cannot walk off the boundary of the grid in any number of moves.
### Draft thoughts
#### Initial approach 
start traversing from boundary 1's in DFS and mark all connected 1's as visited, since you can reach out of the boundary
##### Better approach
same as initial approach
### Algorithm

- start traversing from boundary 1's in DFS and mark all connected 1's as visited, since you can reach out of the boundary
### Observation
- clicking the idea of the solution is main thing here
- similar as [[Replace O's with X's]]

```
int dx[4] = {1, -1, 0, 0};
int dy[4] = {0, 0, 1, -1};

void dfs(int n, int m, int r, int c, vector<vector<int>> &grid, vector<vector<bool>> &vis ) {
	vis[r][c] = true;
	for (int i = 0; i < 4; i++) {
		int row = r + dx[i];
		int col = c + dy[i];
		if (row >= 0 and row<n and col >= 0 and col < m) {
			if (!vis[row][col] and grid[row][col] == 1) {
				dfs(n, m, row, col, grid, vis);
			}
		}
	}
}
int numberOfEnclaves(vector<vector<int>> &grid) {
	int n = grid.size();
	int m = grid[0].size();
	vector<vector<bool>> vis(n, vector<bool> (m, false));

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (i == 0 or i == n - 1 or j == 0 or j == m - 1) {
				if (grid[i][j] == 1) {
					dfs(n, m, i, j, grid, vis);
				}

			}
		}
	}
	int ans = 0;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (!vis[i][j] and grid[i][j] == 1) {
				ans++;
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
