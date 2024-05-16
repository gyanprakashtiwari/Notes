[Problem](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

### Question
Given a Directed Graph with **V** vertices (Numbered from **0** to **V-1**) and **E** edges, check whether it contains any cycle or not.
### Notes
- [[Topological Sorting (DFS)]]
- 


### Observation
- try to make a topo sort array if the array doesn't have exactly N elements then there is a cycle in the graph




```
bool isCyclic(int V, vector<int> adj[]) {
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

	int cnt = 0;
	while (!q.empty()) {
		int node = q.front();
		q.pop();
		cnt++;

		for (auto neighbour : adj[node]) {
			indegree[neighbour]--;
			if (indegree[neighbour] == 0) {
				q.push(neighbour);
			}
		}
	}
	return cnt != V;
}
```


Space Complexity

SC --> O(N ) 


Time Complexity
TC --> O(N ) + O(2 * E)

