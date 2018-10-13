---
layout: post
title: Breadth-First Search Algorithm
date:  2018-10-12 18:00:00
categories: main
banner_image: "BFS.png"
---

Breadth-First-Search is a graph traversal algorithm. 

You might ask, what is **Graph Traversal**? The process of visiting each node/vertex in a graph is called - graph traversal. The order in which these vertices are visited determines what algorithm we use to traverse a graph - **Breadth First Search(BFS)** or **Depth First Search(DFS)**

In this post, we will go into the details of **BFS**.

### What is BFS traversal?
BFS algorithm traverses broadly or width-wise. It visits it's neighbors before visiting the children and uses **Queue** data structure.

### BFS traversal explanation

To determine the unvisited, visited and explored nodes, let's give them colors. 
* black -> unvisited
* red -> explored
	
Initially our graph is going to look like this.
      ![Graph]({{ "/assets/images/graph.jpg" }})

**Step 1:** We select our starting vertex as _A_ and our goal as _I_. We want to search the nodes width-wise, till we reach point _I_.

![Step1]({{ "/assets/images/graph-step1.jpg" }})

**Step 2:** Nodes B, C, D are reachable from node _A_. So we mark A as _explored_, _B_, _C_ and _D_ as _visited_. Marking _B_, _C_, _D_ visited also means that these nodes have to be queued.
![Step1]({{ "/assets/images/graph-step2.jpg" }})

**Step 3:** Now we select node _B_
![Step1]({{ "/assets/images/graph-step3.jpg" }})

**Step 4:** Nodes _E_ and _F_ are reachable from node _B_. We mark them as _visited_ and add them to the queue. We mark _B_ as _explored_
![Step1]({{ "/assets/images/graph-step4.jpg" }})

**Step 5:** Because there are no more nodes to visit through node _B_. We move on to the next queued node, which is node _C_. 
![Step1]({{ "/assets/images/graph-step5.jpg" }})

**Step 6:** From node _C_, we can reach node _G_. We mark _G_ as visited and is queued. _C_ is marked as _explored_.
![Step1]({{ "/assets/images/graph-step6.jpg" }})

**Step 7:** Since, there are no more nodes to visit in node _C_. We move on to node _D_
![Step1]({{ "/assets/images/graph-step7.jpg" }})

**Step 8:** We can see that from node _D_, node _H_ is reachable. So we mark node _H_ as visited and queue it. Node _D_ is marked as _explored_.
![Step1]({{ "/assets/images/graph-step8.jpg" }})

**Step 9:** All the nodes _B_, _C_ and _D_ at level 1 have been _explored_. We move on to the next queued node, which is _E_. 
![Step1]({{ "/assets/images/graph-step9.jpg" }})

**Step 10:** Node _I_ is reachable from node _E_. So we mark _I_ as visited and _E_ as explored. _I_ is queued.
![Step1]({{ "/assets/images/graph-step10.jpg" }})

**Step 11:** We check node _F_ now and observe that it has no children.So, we mark node _F_ as _explored_.
![Step1]({{ "/assets/images/graph-step11.jpg" }})

**Step 12:**  It is the same case with node _G_. It has no children. so, we mark node _G_ as explored and move on to the next queued node.
![Step1]({{ "/assets/images/graph-step12.jpg" }})

**Step 13:** Our next queued node is _H_. Here, we find an unvisited child _J_. So, we mark _J_ as _visited_ and add it to the queue. We mark _H_ as _explored_ 
![Step1]({{ "/assets/images/graph-step13.jpg" }})

**Step 14:** Finally, we reach node _I_. Node _I_ was our goal node and we have reached it, so we abandon any further search and call our BFS successful!
![Step1]({{ "/assets/images/graph-step14.jpg" }})


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

### Time and Space complexity

In BFS, we are iterating only once to find the neighbors of one vertex.
Therefore, assuming that we have _n_ nodes, every node is enqueued at least once and check the edges of adjacency list once, our time complexity will be O(V + E).

In case of undirected graph:

	F(n) = Visiting vertices(V) + number of Edges(E) in adjacency list = O(V) + O(E)
		 = O(V + E)
	
In case of directed graph:
	
	F(n) = Visiting vertices(V) + number of Edges(E) in adjacency list = O(V) + O(2|E|)
		 = O(V + E)

Check out the code for BFS [here](https://github.com/soumyaveer/javascript-algorithms/blob/master/src/containers/Graph.js).
