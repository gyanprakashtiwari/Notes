## Meaning
A graph is essentially a collection of vertices (sometimes called nodes) and edges. The vertices represent individual entities of sorts, and each edge connects a pair of vertices and denotes that they are related in some way.

A bit more formally, a graph G is a pair (V, E) where V is the set of vertices and E is the set of edges (pairs (_a_, _b_) such that _a_, _b_ ∈ V).

## Types of Graphs
### Undirected Graphs

These are the kind of graphs in which an edge connects two vertices without caring about the order of the vertices connected. For example, at a party, we can say there is an edge between two people if they shook each other’s hands. Person A shaking Person B’s hand is equivalent to B shaking A’s hand.

### Directed Graphs
Contrary to an undirected graph, here, the edges have a definite starting and ending vertex.
**Important Point**
It is worth noting that an undirected graph can also be seen as a directed graph in which for every edge (A, B) in the undirected graph, there are 2 edges (A, B) and (B, A) in the directed version.
### Other categories

- **weighted graph** : where there is a cost/weight attached to an edge
- **unweighted graph** : where there is not weight/cost attached to an edge or we can say a weighted graph which all edges have equal weight
### Cyclic Graph

Starting from a node/vertex if we traverse and reach the same node/vertex again than that graph is called cyclic 
### Path

- Contains a lot of nodes and each of them are reachable.
- A node cannot appear more than once in a path
- for every 2 adjacent nodes must there must be an edge

### Degree in Graph

**degree of a node** is the number of edges that goes in and out of a node

#### For Undirected Graph

- Total degree of graph = 2 * E
- where E --> number of edges
#### For directed graph

We have 2 things Indegree(node) and Outdegree(node)
in degree --> total incoming edges to the node
out degree --> total outgoing edges from the node

## Representation of Graph

**Input :** n , m
n --> number of nodes/vertices
m --> number of edges

edges are represented by pair (a,b) which means there is an edge between node a and node b.
for undirected graph we can assume if (a,b) is an edge there also exist an edge (b,a)

### How to store a graph
### There are 2 ways to store a graph
#### Matrix

Given n --> number of nodes
we create a matrix of size n * n
all cells of matrix are initially 0
if  a cell (i,j) is 1 that means there is an edge between i and j

Space complexity of storing it this way is O(n * n)

#### List

Given n --> number of nodes

we create an array of list 

```
vector<int> adj[n+1] -- 1 based indexing
OR
vector<int> adj[n] -- 0 based indexing
```

i --> {a,b}
j --> {}

the above represents that i has an edge with a and b
j does not have edge with any other node

Space Complexity 
**Undirected** graph--> O(2 * E)
**Directed** graph --> O(E)
where E --> number of edges

### Storing weighted graphs

#### Matrix

cell(i,j) = w
which means there is an adge between i and j with weight w

#### List

```
vector<pair<int,int>> adj[n+1]
```

an array of list of pair of integers 
adj(i) --> {(a,w)}

which means there is an edge between i and a with weight w

### Connected components in graphs
Assuming a traversal algorithm if starting from a node you start traversing and you have not visited all n nodes of a graph . this means the graph has multiple components which are not connected 

```
for (auto node : all_nodes){
	if(not_visited(node)){
		traversal(node);
	}
}
```

### Traversal

#### BFS
- take a queque and insert the starting node
- take a visited array mark the starting node as visited
- while queue is not empty 
	- pop the front element and print it 
	- find all its neighbours and push it to queue if not visited then mark as visited  
```
vector<int> BFS(int n, vector<int> adj[]) {
	queue<int> q;
	q.push(1);
	vector<bool> visited(n + 1, false);
	visited[1] = true;
	vector<int> bfs;

	while (!q.empty()) {
		int curr_node = q.front();
		q.pop();
		bfs.push_back(curr_node);

		for (auto neighbour : adj[curr_node]) {
			if (!visited[neighbour]) {
				visited[neighbour] = true;
				q.push(neighbour);
			}
		}

	}
	return bfs;
}
```


#### DFS

- It uses recursion
- choose a starting node , visited array , and a dfs_traversal_vector
- mark starting node as visited and add it to dfs_traversal_vector
- for each neighbour of starting node
	- if not visited call dfs with this as starting node

```
void traverseDFS(int curr_node, vector<int> adj[], vector<int> &visited, vector<int> &dfs) {
	dfs.push_back(curr_node);
	visited[curr_node] = 1;

	for (auto child : adj[curr_node]) {
		if (!visited[child]) {
			traverseDFS(child, adj, visited, dfs);
		}
	}
	return;

}
```

Space Complexity

O(N) + O(N) + O(N) = O(N)

Time Complexity
			
TC --> O(N) + O(2 * E)

where ,
- N is number of nodes
- summation of degrees = 2 * E


### Problems
- [[Number of Provinces]]
- [[Number of Connected Components]]
- [[Flood Fill Algorithm]]
- [[Rotten Oranges]]
- [[Detect Cycle in Undirected Graph BFS]]
- [[Detect Cycle in Undirected Graph DFS]]
- [[Distance of nearest cell having 1]]
- [[Replace O's with X's]]
- [[Number of Enclaves]]
- [[Number of Distinct Islands]]
- [[Bipartite Graph BFS]]
- [[Bipartite Graph DFS]]
- [[Detect cycle in directed graph DFS]]
- [[Eventual Safe States]]
- [[Topological Sorting (DFS)]]
- [[Topological Sorting (BFS) or Kanh's Algorithm]]
- [[Detect cycle in DAG Topological Sorting(BFS)]]
- [[Prerequisite task 1]]
- [[Course Schedule]]
- [[Eventual Safe States - Topo Sort]]
- [[Alien Dictionary]]
- 




