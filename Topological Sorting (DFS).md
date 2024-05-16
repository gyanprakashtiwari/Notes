[problem](https://www.geeksforgeeks.org/problems/topological-sort/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=bottom_sticky_on_article)


Given a Directed Acyclic Graph (DAG) with V vertices and E edges, Find any Topological Sorting of that Graph

- can only be applied to DAG
### Definition
linear ordering of vertices such that if there is an edge between u and v , then u appears before v in that ordering

#### Why only in DAG?
in undirected graph if there is an edge between u and v then there is also an edge between v and u which does not make sense to write while ordering the vertices

also similarly a cycle cannot be represented in ordering of vertices

```
void dfs(int node, vector<int> adj[], vector<int> &vis, stack<int> &st) {
	vis[node] = 1;

	for (int neighbour : adj[node]) {
		if (!vis[neighbour]) {
			dfs(neighbour, adj, vis, st);
		}
	}
	st.push(node);
}
vector<int> topoSort(int V, vector<int> adj[]) {
	vector<int> ans;
	stack<int> st;
	vector<int> vis(V, 0);
	for (int i = 0; i < V; i++) {
		if (!vis[i]) {
			dfs(i, adj, vis, st);
		}
	}

	while (!st.empty()) {
		ans.push_back(st.top());
		st.pop();
	}
	return ans;
}
```

Time Complexity
TC --> O(V + E)
for directed graph

Space Complexity

SC --> O(N) + O(N)
SC --> O(N)