Consider a rat placed at **(0, 0)** in a square matrix of order **N * N**. It has to reach the destination at **(N - 1, N - 1)**. Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are **'U'(up)**, **'D'(down)**, **'L' (left)**, **'R' (right)**. Value 0 at a cell in the matrix represents that it is blocked and rat cannot move to it while value 1 at a cell in the matrix represents that rat can be travel through it.  
**Note**: In a path, no cell can be visited more than one time. If the source cell is 0, the rat cannot move to any other cell.


## Approach

1. basic dfs in all directions move if valid

Code C++

```
char ds[4] = {'R', 'L', 'D', 'U'};
	int dx[4] = {0, 0, 1, -1};
	int dy[4] = {1, -1, 0, 0};


	void go(int r, int c, int n, vector<vector<int>> &m, string curr, vector<string> &ans, vector<vector<int>> &vis) {
		if (r == n - 1 and c == n - 1) {
			ans.push_back(curr);
			return;
		}

		for (int dir = 0; dir < 4; dir++) {
			int row = r + dx[dir];
			int col = c + dy[dir];
			if (row >= 0 and col >= 0 and row < n and col < n) {
				if (m[row][col] == 1 and vis[row][col] == 0) {
					// 	curr.push_back(ds[dir]);
					vis[row][col] = 1;
					go(row, col, n, m, curr + ds[dir], ans, vis);
					// 	curr.pop_back();
					vis[row][col] = 0;
				}
			}
		}

	}

	vector<string> findPath(vector<vector<int>> &m, int n) {
		// Your code goes here
		vector<string> ans;
		string curr = "";

		vector<vector<int>> vis(n, vector<int> (n, 0));
		if (m[0][0] == 1) {
			vis[0][0] = 1;
			go(0, 0, n, m, curr, ans, vis);
		}


		if (ans.size() == 0) {
			return {"-1"};
		}
		sort(ans.begin(), ans.end());

		return ans;
	}
```