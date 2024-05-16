[Problem](https://www.geeksforgeeks.org/problems/distance-of-nearest-cell-having-1-1587115620/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=distance-of-nearest-cell-having-1)

Given a binary grid of *n * m*. Find the distance of the nearest 1 in the grid for each cell.  
The distance is calculated as **|i1  - i2| + |j1 - j2|**, where i1, j1 are the row number and column number of the current cell, and i2, j2 are the row number and column number of the nearest cell having value 1. There should be atleast one 1 in the grid.

Algorithm
- 

```
int dx[4] = {0, 0, 1, -1};
int dy[4] = {1, -1, 0, 0};
void bfs(vector<vector<int>>&grid, vector<vector<int>>&dist, vector<vector<bool>>&vis) {
	queue<pair<pair<int, int>, int>> q;
	int n = grid.size();
	int m = grid[0].size();
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (grid[i][j] == 1) {
				vis[i][j] = true;
				dist[i][j] = 0;
				q.push({{i, j}, 0});
			}
		}
	}

	while (!q.empty()) {
		int r = q.front().first.first;
		int c = q.front().first.second;
		int level = q.front().second;
		q.pop();
		dist[row][col] = level;
		for (int dir = 0; dir < 4; dir++) {
			int row = r + dx[dir];
			int col = c + dy[dir];
			if (row >= 0 and row<n and col >= 0 and col < m) {
				if (!vis[row][col] and grid[row][col] == 0) {
					vis[row][col] = true;
					q.push({{row, col}, level + 1});
				}
			}
		}

	}

}
vector<vector<int>>nearest(vector<vector<int>>grid) {
	int n = grid.size();
	int m = grid[0].size();

	vector<vector<int>> dist(n, vector<int> (m));
	vector<vector<bool>> vis(n, vector<bool> (m, false));
	bfs(grid, dist, vis);
	return dist;
}
```





Space Complexity

SC --> O(N * M) 




Time Complexity
TC --> O(N * M) + O(N * M * 4)

TC --> O(N * M) 
