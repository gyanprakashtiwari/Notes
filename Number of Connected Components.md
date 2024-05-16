[Problem](https://www.geeksforgeeks.org/problems/find-the-number-of-islands/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=find_the_number_of_islands)


Algorithm
- we maintain a visited 2 D matrix 
- start iterating through the grid if we find an cell with 1 and not visited and call our traversal (dfs or bfs)
- our traversal will mark all neighbour 1's as visited 
- total number of islands is equal to number of traversal calls

Code 

```
int dx[8] = { -1, -1, -1, 0, 1, 1, 1, 0};
int dy[8] = { -1, 0, 1, 1, 1, 0, -1, -1};

void dfs(int i, int j, int n, int m, vector<vector<char>>& grid, vector<vector<bool>> &vis) {
	vis[i][j] = true;

	for (int dir = 0; dir < 8; dir++) {
		int xx = i + dx[dir];
		int yy = j + dy[dir];
		if (xx >= 0 and xx<n and yy >= 0 and yy < m) {
			if (!vis[xx][yy] and grid[xx][yy] == '1') {
				dfs(xx, yy, n, m, grid, vis);
			}
		}
	}
}
int numIslands(vector<vector<char>>& grid) {
	int n = grid.size();
	int m = grid[0].size();

	vector<bool> va(m, false);
	vector<vector<bool>> vis(n, va);
	int ans = 0;

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (!vis[i][j] and grid[i][j] == '1') {
				ans++;
				dfs(i, j, n, m, grid, vis);
			}
		}
	}
	return ans;

}
```

Space Complexity

SC --> n nodes + max stack space
SC --> O(n) + O(n)

Time Complexity

TC --> n nodes + dfs
TC --> O(N) + O(2 * E)