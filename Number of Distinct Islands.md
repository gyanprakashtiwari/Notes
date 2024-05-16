[Problem](https://www.geeksforgeeks.org/problems/number-of-distinct-islands/1)


You are given an **n x m** binary matrix **grid**, where **0** represents a sea cell and **1** represents a land cell.

A move consists of walking from one land cell to another adjacent (4-directionally) land cell or walking off the boundary of the grid.

Find the number of land cells in **grid** for which we cannot walk off the boundary of the grid in any number of moves.

### Algorithm

- start traversing from boundary 1's in DFS and mark all connected 1's as visited, since you can reach out of the boundary
### Observation
- clicking the idea of the solution is main thing here
- main idea was how to store unique islands or what makes 2 islands of some shape at similar whats  pattern

```
int dx[4] = {1, -1, 0, 0};
int dy[4] = {0, 0, 1, -1};
void dfs(int n, int m, int r, int c, vector<vector<int>>& grid,
         vector<vector<bool>>& vis, vector<pair<int, int>> &curr_island, int r0, int c0) {
	vis[r][c] = true;
	curr_island.push_back({r - r0, c - c0});
	for (int dir = 0; dir < 4; dir++) {
		int row = r + dx[dir];
		int col = c + dy[dir];
		if (row >= 0 and row<n and col >= 0 and col < m) {
			if (!vis[row][col] and grid[row][col] == 1) {
				dfs(n, m, row, col, grid, vis, curr_island, r0, c0);
			}
		}
	}

}
int countDistinctIslands(vector<vector<int>>& grid) {
	int n = grid.size();
	int m = grid[0].size();
	set<vector<pair<int, int>>> ans;
	vector<vector<bool>> vis(n, vector<bool> (m, false));
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (grid[i][j] == 1 and !vis[i][j]) {
				vector<pair<int, int>> curr_island;
				dfs(n, m, i, j, grid, vis, curr_island, i, j);
				ans.insert(curr_island);
			}
		}
	}
	return ans.size();
}


```










Space Complexity

SC --> O(N * M) 




Time Complexity
TC --> O(N * M * log(set length)) + O(N * M * 4)

TC --> O(N * M * log(N * M)) + O(N * M * 4)
TC --> O(N * M) 
