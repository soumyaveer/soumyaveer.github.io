---
layout: post
title: Breadth-First Search Algorithm
date:  2018-10-12 18:00:00
categories: main
banner_image: "symbols_vs_strings.jpg"
---

Breadth-First-Search is a graph traversal algorithm. 

You might ask, what is **Graph Traversal**? The process of visiting each node/vertex in a graph is called - graph traversal. The order in which these vertices are visited determines what algorithm we will use to traverse a graph - Breadth First Search(BFS) or Depth First Search(DFS)

In this post, we will be going into the details of **BFS**.

### What is BFS traversal?
BFS algorithm traverses broadly or width-wise. It visits it's neighbors before visiting the children and uses Queue data structure.

/graph image.


### BFS traversal explanation

To determine the unvisited, visited and explored nodes, let's give them colors. 
	* white -> unvisited
	* gray -> visited
	* black -> explored

The first thing that we need to do in order to begin traversal is select a starting vertex. For our example let's select `A`. So we want to go to vertex `A`, and mark in as visited. Next we check if `A ` has any neighbors to explore. Since `A` has no neighbors, we move on to level 2, vertex `B` and mark it as visited. We find the neighbors of vertex `B` which are `C` and `D`. So we mark `C` and `D` as visited and `A` as explored. WE move on to next level of `B` which is `E` mark it as visited and and visit the neighbors of `E` which is `F`. Similarly, in case of vertex, `C` we have `G` and `H`, so we mark `C` as explored and `G` and `H` as visited. Since there are no more neighbors to visit for `C` and `D` we mark them as explored. We move on to `E` and find that `E` has unvisited child `I`. So we mark it as visited. Since, `I` is visited, `E` is explored and since `F` does not have any more children to visit, `F` is also explored. In the end as I also has no further children to explore, we mark I as explored as well.


### Algorithm for BFS

     1. Create queue
     2. Mark starting vertex(v) as discovered (grey).
     3. Enqueue v to queue
     4. Loop through queue ,while queue is not empty:
        4.1 Dequeue first node from queue, let's call it u.
        4.2 Mark u as discovered (grey). The undiscovered nodes are marked white.
        4.3 Find it's neighbors
        4.4 Loop through each neighbor. We will call each element w:
            4.4.1 Check is the neighbor(w) is undiscovered (white)
                  4.4.1.1 Mark it(w) as discovered (grey)
                  4.4.1.2 Enqueue the neighbor (w)
        4.5 Mark u as explored(black);
        4.6 Concatenate the result to the queue

### Pseudo Code for BFS

```javascript

	bfs(v)
	  initialize the color of all nodes as white (unvisited)
	  create a queue
	  queue.enqueue(v)
	  color[v] = gray(visited)
	  while queue is not empty
		u = queue.dequeue
		color[u] = gray
		neighbors = findNeighborsOf(u)		
		loop through neighbors
		if color[neighbor] == white
		  color[neighbor] = grey
		  queue.enqueue(neighbor)
	    color[u] = black
```

### Time and Space complexity

In the algorithm, we are only iterating only once to find the neighbors of one vertex.
Therefore, assuming that we have n nodes,  and every node is enqueued at least once and check the edges of adjacency list once, our time complexity will beO(V + E).

In case of undirected graph:

	F(n) = Visiting vertices(V) + number of Edges(E) in adjacency list = O(V) + O(E)
		 = O(V  + E)
	
In case of directed graph:
	
	F(n) = Visiting vertices(V) + number of Edges(E) in adjacency list = O(V) + O(2|E|)
		 = O(V + E)
