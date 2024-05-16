[Problem](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

### Question
Given a Directed Graph with **V** vertices (Numbered from **0** to **V-1**) and **E** edges, check whether it contains any cycle or not.

### Algorithm
-
### Observation
- on the same path every node has to be visited to be a cyclic



```
bool dfs(int start, vector<int> adj[], vector<bool> &vis, vector<bool> &pathVis) {
	vis[start] = true;
	pathVis[start] = true;

	for (auto neighbour : adj[start]) {
		if (!vis[neighbour]) {
			if (dfs(neighbour, adj, vis, pathVis) == true) {
				return true;
			}
		} else {
			if (pathVis[neighbour]) {
				return true;
			}
		}
	}
	pathVis[start] = false;
	return false;
}
bool isCyclic(int V, vector<int> adj[]) {

	vector<bool> vis(V, false);
	vector<bool> pathVis(V, false);

	for (int i = 0; i < V; i++) {
		if (!vis[i]) {
			if (dfs(i, adj, vis, pathVis) == true) {
				return true;
			}
		}
	}
	return false;
}
```





Space Complexity

SC --> O(N ) 




Time Complexity
TC --> O(N ) + O(2 * E)

