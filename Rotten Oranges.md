[Problem](https://www.geeksforgeeks.org/problems/rotten-oranges2536/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=rotten_oranges)


it basically boils down to find max level of BFS calls to get all oranges rotten if possible else return -1

Algorithm
- 
Code 

```
int dx[4] = {0, 0, 1, -1};
int dy[4] = {1, -1, 0, 0};
int bfs(vector<vector<int>>& grid, vector<vector<int>>& res, vector<vector<bool>>& vis, int t, int tmax) {
	int n = grid.size();
	int m = grid[0].size();
	queue<pair<int, pair<int, int>>> q;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (grid[i][j] == 2) {
				vis[i][j] = 1;
				q.push({0, {i, j}});
			}
		}
	}
	while (!q.empty()) {
		pair<int, pair<int, int>> curr = q.front();
		q.pop();
		int r = curr.second.first;
		int c = curr.second.second;
		int level = curr.first;
		if (res[r][c] == 1) {
			tmax = max(tmax, level);
			res[r][c] = 2;
		}

		vis[r][c] = 1;

		for (int dir = 0; dir < 4; dir++) {
			int x = r + dx[dir];
			int y = c + dy[dir];
			if (x >= 0 and x<n and y >= 0 and y < m and grid[x][y] == 1 and !vis[x][y]) {
				q.push({level + 1, {x, y}});
			}
		}
	}

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (res[i][j] == 1) {
				return -1;
			}
		}
	}

	return tmax;

}
int orangesRotting(vector<vector<int>>& grid) {
	int n = grid.size();
	int m = grid[0].size();
	vector<vector<int>> res = grid;
	vector<vector<bool>> vis(n, vector<bool> (m, false));
	return bfs(grid, res, vis, 0, 0);
}
```

Space Complexity

SC --> N * M 

space used for storing ans + stack space

Time Complexity
N * M --> X nodes
TC --> X + X * 4 --> X
TC -->O(N * M)