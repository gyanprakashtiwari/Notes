[Problem](https://www.geeksforgeeks.org/problems/flood-fill-algorithm1856/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=flood-fill-algorithm)



Algorithm
- we maintain two 2 D matrix for visited and ans(final result of image)
- make a DFS call to cell i, j
	- mark it as visited 
	- change its colour to new colour if it is of initial colour
- Each DFS call marks a cells neighbour with same colour as new colour

Code 

```
int dx[4] = {0, 0, 1, -1};
int dy[4] = {1, -1, 0, 0};
void dfs(vector<vector<int>>& image, int sr, int sc, int color, int initialColor, vector<vector<bool>> &vis, vector<vector<int>>& ans) {
	int n = image.size();
	int m = image[0].size();
	vis[sr][sc] = true;
	ans[sr][sc] = color;
	for (int i = 0; i < 4; i++) {
		int r = sr + dx[i];
		int c = sc + dy[i];
		if (r >= 0 and r<n and c >= 0 and c < m) {
			if (image[r][c] == initialColor and !vis[r][c]) {
				dfs(image, r, c, color, initialColor, vis, ans);
			}
		}
	}
}

vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
	int n = image.size();
	int m = image[0].size();
	vector<vector<bool>> vis(n, vector<bool> (m, false));
	vector<vector<int>> ans(n, vector<int> (m, 0));
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			ans[i][j] = image[i][j];
		}
	}
	int initialColor = image[sr][sc];
	dfs(image, sr, sc, color, initialColor, vis, ans);
	return ans;
}
```

Space Complexity

SC --> N * M + N * M

space used for storing ans + stack space

Time Complexity
N * M --> X nodes
TC --> X + X * 4 --> X
TC -->O(N * M)