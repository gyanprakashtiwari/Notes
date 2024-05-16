[Problem](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=bottom_sticky_on_article)


if the neighbour of any node is already visited and it is not the parent node than some other path exist that have visited this and it got visited twice hence it has a cycle

Algorithm
- if any of the component of the graph has cycle than a graph has cycle
Code 

```
bool bfs(int start, vector<int> adj[], vector<bool> &vis) {
	queue<pair<int, int>> q;
	q.push({start, -1});
	vis[start] = true;

	while (!q.empty()) {
		int node = q.front().first;
		int parent = q.front().second;
		q.pop();
		for (auto neighbour : adj[node]) {
			if (!vis[neighbour]) {
				q.push({neighbour, node});
				vis[neighbour] = true;
			} else {
				// already visited
				if (parent != neighbour) {
					// it is not the parent node of node
					// it must have been visited by some other parent node on different path
					// now from different path we are trying to visit the neighbour
					// means there is a cycle
					return true;
				}
			}
		}
	}
	return false;
}
bool isCycle(int V, vector<int> adj[]) {

	vector<bool> vis(V, false);
	for (int i = 0; i < V; i++) {
		if (!vis[i]) {
			if (bfs(i, adj, vis) == true) {
				return true;
			}
		}
	}
	return false;
}
```



Space Complexity

SC --> N 

space used for storing ans + stack space

Time Complexity
TC --> N + 2E
