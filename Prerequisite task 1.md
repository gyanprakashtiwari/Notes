[problem](https://www.geeksforgeeks.org/problems/prerequisite-tasks/1)

There are a total of N tasks, labeled from 0 to N-1. Some tasks may have prerequisites, for example to do task 0 you have to first complete task 1, which is expressed as a pair: [0, 1]  
Given the total number of **tasks N** and a list of **prerequisite pairs P**, find if it is possible to finish all tasks.


### Algorithm
- check if cycle exists with topo sort  

```
bool isPossible(int V, int P, vector<pair<int, int> >& prerequisites) {
	vector<int> adj[V];

	for (auto p : prerequisites) {
		adj[p.first].push_back(p.second);
	}
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
	if (ans.size() == V)return true;
	return false;
}
```



Time Complexity
TC --> O(V + E)
for directed graph

Space Complexity

SC --> O(N) + O(N)
SC --> O(N)