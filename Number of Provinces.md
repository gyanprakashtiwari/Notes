[Problem](https://leetcode.com/problems/number-of-provinces/)

Algorithm
- we traverse through each node and if not visited call dfs on it
- dfs will further traverse through connected nodes
- while traversing through each node number of provinces will be number of times dfs is called

Code 

```
void dfs(int i, vector<vector<int>>& isConnected, vector<bool> &vis) {
	vis[i] = true;
	int n = vis.size();
	for (int node = 0; node < n; node++) {
		if (isConnected[i][node] == 1) {
			if (!vis[node]) {
				dfs(node, isConnected, vis);
			}
		}
	}
}
int findCircleNum(vector<vector<int>>& isConnected) {
	int n = isConnected.size();
	vector<bool> vis(n, false);
	int ans = 0;
	for (int i = 0; i < n; i++) {
		if (!vis[i]) {
			ans++;
			dfs(i, isConnected, vis);
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