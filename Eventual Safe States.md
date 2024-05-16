[Problem](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

### Question
A directed graph of **V** vertices and **E** edges is given in the form of an adjacency list **adj**. Each node of the graph is labelled with a distinct integer in the range **0** to **V - 1**.

A node is a **terminal node** if there are no outgoing edges. A node is a **safe node** if every possible path starting from that node leads to a **terminal node**.

You have to return an array containing all the **safe nodes** of the graph. The answer should be sorted in **ascending** order.
### Algorithm
-
### Observation
- every node that is part of a cycle or leads to a cycle cannot be a safe node
- all other nodes are safe nodes



```
bool dfs(int start, vector<int> adj[], vector<bool> &vis, vector<bool> &pathVis, vector<bool> &check) {
	vis[start] = true;
	pathVis[start] = true;
	check[start] = false;

	for (auto neighbour : adj[start]) {
		if (!vis[neighbour]) {
			if (dfs(neighbour, adj, vis, pathVis, check) == true) {
				check[start] = false;
				return true;
			}
		} else {
			if (pathVis[neighbour]) {
				check[start] = false;
				return true;
			}
		}
	}
	check[start] = true;
	pathVis[start] = false;
	return false;
}

vector<int> eventualSafeNodes(int V, vector<int> adj[]) {
	// code here
	vector<int> safeNodes;
	vector<bool> vis(V, false);
	vector<bool> pathVis(V, false);
	vector<bool> check(V, false);

	for (int i = 0; i < V; i++) {
		if (!vis[i]) {
			dfs(i, adj, vis, pathVis, check);

		}
	}

	for (int i = 0; i < V; i++) {
		if (check[i])safeNodes.push_back(i);
	}
	return safeNodes;
}
```






Space Complexity

SC --> O(N ) 




Time Complexity
TC --> O(N ) + O(2 * E)

