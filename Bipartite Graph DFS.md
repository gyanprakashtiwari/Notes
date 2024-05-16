[Problem](https://www.geeksforgeeks.org/problems/bipartite-graph/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=bottom_sticky_on_article)


### Definition
A bipartite graph is a graph in which the vertices can be divided into two disjoint sets, such that no two vertices within the same set are adjacent. In other words, it is a graph in which every edge connects a vertex of one set to a vertex of the other set.

### Question
Given an adjacency list of a graph **adj** of V no. of vertices having 0 based index. Check whether the graph is bipartite or not.
### Algorithm
- any linear acyclic graph can always be bipartite
- any cyclic graph with even cycle length can also be bipartite
- any graph with odd length cycle length cannot be bipartite 
### Observation
- if a graph problem gives WA on large input usually it is due to multiple components of the graph



```
bool dfs(int start, int color, vector<int> adj[], vector<int> &vis) {
	vis[start] = color;
	for (auto neighbour : adj[start]) {
		if (vis[neighbour] == -1) {
			bool res;
			if (color == 0) {
				res = dfs(neighbour, 1, adj, vis);
			} else {
				res = dfs(neighbour, 0, adj, vis);
			}
			if (res == false)return false;
		} else {
			// visited or colored before
			if (vis[start] == vis[neighbour]) {
				return false;
			}
		}
	}
	return true;
}
bool isBipartite(int V, vector<int>adj[]) {
	vector<int> vis(V, -1);

	for (int i = 0; i < V; i++) {
		if (vis[i] == -1) {
			if (dfs(i, 0, adj, vis) == false) {
				return false;
			}
		}
	}
	return true;

}
```












Space Complexity

SC --> O(N ) 




Time Complexity
TC --> O(N ) + O(2 * E)

