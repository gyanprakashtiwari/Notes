[problem](https://www.geeksforgeeks.org/problems/topological-sort/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=bottom_sticky_on_article)


Given a Directed Acyclic Graph (DAG) with V vertices and E edges, Find any Topological Sorting of that Graph

- can only be applied to DAG
### Definition
linear ordering of vertices such that if there is an edge between u and v , then u appears before v in that ordering

#### Why only in DAG?
in undirected graph if there is an edge between u and v then there is also an edge between v and u which does not make sense to write while ordering the vertices

also similarly a cycle cannot be represented in ordering of vertices

### Notes
- indegree --> number of incoming edges of a node
### Algorithm
- insert all nodes in queue with indegree is zero
- take them out of the queue and reduce the indegree of it's adjacent nodes 

```
vector<int> topoSort(int V, vector<int> adj[]) {
	vector<int> indegree(V, 0);

	for (int i = 0; i < V; i++) {
		for (int j : adj[i]) {
			indegree[j]++;
		}
	}
	queue<int> q;
	for (int i = 0; i < V; i++) {
		if (indegree[i] == 0) {
			q.push(i);
		}
	}

	vector<int> ans;
	while (!q.empty()) {
		int node = q.front();
		q.pop();
		ans.push_back(node);

		for (auto neighbour : adj[node]) {
			indegree[neighbour]--;
			if (indegree[neighbour] == 0) {
				q.push(neighbour);
			}
		}
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