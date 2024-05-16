[problem](https://www.geeksforgeeks.org/problems/course-schedule/1)


There are a total of **n** tasks you have to pick, labelled from 0 to n-1. Some tasks may have **prerequisite** tasks, for example to pick task 0 you have to first finish tasks 1, which is expressed as a pair: [0, 1]  
Given the total number of **n** tasks and a list of prerequisite pairs of size **m**. Find a ordering of tasks you should pick to finish all tasks.  
**Note:** There may be multiple correct orders, you just need to return any one of them. If it is impossible to finish all tasks, return an empty array. Driver code will print **"No Ordering Possible"**, on returning an empty array. Returning any correct order will give the output as **1**, whereas any invalid order will give the output **0**.

### Algorithm
- check if cycle exists with topo sort  and return topo sort ordering of vertices

```
vector<int> findOrder(int V, int m, vector<vector<int>> prerequisites) {
	vector<int> adj[V];

	for (auto p : prerequisites) {
		adj[p[1]].push_back(p[0]);
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

	if (ans.size() == V)return ans;
	return {};
}
```




Time Complexity
TC --> O(V + E)
for directed graph

Space Complexity

SC --> O(N) + O(N)
SC --> O(N)