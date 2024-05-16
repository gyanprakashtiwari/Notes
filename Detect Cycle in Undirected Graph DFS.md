[Problem](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=bottom_sticky_on_article)


if the neighbour of any node is already visited and it is not the parent node than some other path exist that have visited this and it got visited twice hence it has a cycle

Algorithm
- if any of the component of the graph has cycle than a graph has cycle
Code 

```
bool dfs(int start, int from, vector<int> adj[], vector<bool> &vis) {
	vis[start] = true;
	for (auto neighbour : adj[start]) {
		if (!vis[neighbour]) {
			if (dfs(neighbour, start, adj, vis) == true) {
				return true;
			}
		} else {

			if (neighbour != from) {
				return true;
			}
		}
	}
	return false;
}
bool isCycle(int V, vector<int> adj[]) {

	vector<bool> vis(V, false);
	for (int i = 0; i < V; i++) {
		if (!vis[i]) {
			if (dfs(i, -1, adj, vis) == true) {
				return true;
			}
		}
	}
	return false;
}
```




Space Complexity

SC --> stack space(N) + visited array(N)
SC --> O(N)



Time Complexity
TC --> for each node all it edges(N + 2E) + N loops for calling all unvisited no once(N)
TC --> O(N + 2E)
