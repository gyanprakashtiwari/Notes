[problem](https://www.geeksforgeeks.org/problems/eventual-safe-states/1)


A directed graph of **V** vertices and **E** edges is given in the form of an adjacency list **adj**. Each node of the graph is labelled with a distinct integer in the range **0** to **V - 1**.

A node is a **terminal node** if there are no outgoing edges. A node is a **safe node** if every possible path starting from that node leads to a **terminal node**.

You have to return an array containing all the **safe nodes** of the graph. The answer should be sorted in **ascending** order.

### Algorithm
- check if cycle exists with topo sort  and return topo sort ordering of vertices

```
vector<int> eventualSafeNodes(int V, vector<int> adj[]) {
	vector<int> revAdj[V];
	for (int i = 0; i < V; i++) {
		for (int it : adj[i]) {
			revAdj[it].push_back(i);
		}
	}

	int indegree[V] = {0};

	for (int i = 0; i < V; i++) {
		for (int it : revAdj[i]) {
			indegree[it]++;
		}
	}

	queue<int> q;
	for (int i = 0; i < V; i++) {
		if (indegree[i] == 0) {
			q.push(i);
		}
	}

	vector<int> topo;

	while (!q.empty()) {
		int node = q.front();
		q.pop();
		topo.push_back(node);

		for (int it : revAdj[node]) {
			indegree[it]--;
			if (indegree[it] == 0) {
				q.push(it);
			}
		}
	}

	sort(topo.begin(), topo.end());

	return topo;
}
```





Time Complexity
TC --> O(V + E)
for directed graph

Space Complexity

Extra space for storing rev graph