---
layout: page
title: "Edge Compression"
description: University of Nottingham, School of Computer Science
img: assets/img/12.jpg
importance: 2
category: work
---
## Minimum Edge Compression of General Graphs   (Allowing edges going into supernodes and nodes being overlapped)

## Introduction
Graphs with numerous nodes and edges are prevalent in various fields. However, the high complexity of large graphs poses challenges for data storage and processing in research. Lossless compression techniques have become increasingly important to address these issues. Existing research has proposed several theories for edge compression, but most studies primarily focus on edge reduction without adequately addressing shared nodes connecting multiple edges.

A novel lossless edge compression rule that permits node overlapping was introduced. We then present algorithms tailored for different graph types to find the compressed graph with the minimum number of edges. Under this rule, the problem of finding the minimum edge compressed graph can be transformed into finding the minimum vertex covering/maximum independent set of the original graph. Although this problem is NP-complete in a general graph, intelligent optimization algorithms, such as the genetic algorithm, can be employed to find approximate solutions.

However, approximate solutions may not be satisfactory when exact results are desired, or the time cost is tolerable. In such cases, we apply a dynamic programming algorithm to accurately determine the minimum edge compression. Our compression technique, which allows for node overlapping, not only reduces edges but also efficiently utilizes information stored in shared nodes. This approach saves storage space and enhances data processing efficiency.

## Explanation

In this section, some definitions, terms, notations and the compression rule would be expounded.

### Definition 1
Edge **e** is an elements pair on the set of vertex **V**. It could be an ordered pair or an unordered pair, representing a directed edge or an undirected edge respectively. *(shown in **Fig.1**)*
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
### Definition 2
**V** is a finite vertex set and **E** is an edge set defined on **V**, The mathematical structure **G = (V,E)** is a general graph.

Although general graphs contain directed graphs and weighted graphs, in this analysis, we only focus on the simplest model, undirected graphs. And then, the compression rules was introduced:

**Rule 1**: as **Fig.2** shows, if a series of vertices ($$v_{1},v_{2},...,v_{i}$$) were connected to the same neighbor vertex $$v_{nei}$$, these vertices ($$v_{1},v_{2},...,v_{i}$$) would be encapsulated into a block, called **supernode**. And these edges were compressed to a **superedge**.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/13.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
### Definition 3
A **node** refers to a vertex or a supernode.

In this analysis, the term **node** would be used more frequently than term **vertex**.

**Rule 2**: for complete subgraph parts in a general graph, all nodes in the subgraph are encapsulated into a supernode, and all edges are compressed into a self leading edge in the supernode. As **Fig.3** shows.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/14.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
**Rule 3**: supernode is also a node and the **Rule 1** is also valid for supernodes. This means that if a supernode $$S_{1}$$ containing some nodes ($$a, b,...$$) connected to a series of different nodes ($$v_{1},v_{2},..., v_{i}$$), these nodes would be encapsulated into another supernode $$S_{2}$$. Shown in **Fig.4**.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/15.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
**Rule 4**: edge was allowed to go into supernodes. This meaned an encapsulated node $$c$$ within supernode $$S$$ was allowed to connect separately to another node $$d$$ (whether $$d$$ is inside or outside $$S$$) in the compressed graph, if necessary. As **Fig.5** shows.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/16.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
**Rule 5**: If the same node $$a$$ was used by more than one supernodes ($$S_{1}, S_{2},...,S_{i}$$), these supernodes were overlapped and the node $$a$$ was allowed to be reused. Shown in **Fig.6**.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/17.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## The principle of algorithm 
For an undirected and unweighted graph without complete subgraph, the **Rule 2** is not valid. For the remaining four rules, only **Rule 1** and **Rule 3** can cause the change of edge quantity, both compressing edges connected to the common node into a superedge.

By the definition of the covering set, edges ($$e_{S,1},e_{S,2},...,e_{S,i}$$) connected to vetices ($$v_{S,1},v_{S,2},...,v_{S,i}$$) within a vertex covering S, cover all the edges in the original graph $$G(V,E)$$: $$E_{v \rightarrow e}(S) = E_{v \rightarrow e}(G)$$ Where $$E_{v \rightarrow e}$$ is a function from vertice to edges them connecting.

By the **Rule 1**, edges ($$e_{S,1},e_{S,2},...,e_{S,i}$$) connected to vetices ($$v_{S,1},v_{S,2},...,v_{S,i}$$) within a vertex covering $$S$$, would be compressed to a superedge repectively, and neighbours of these vetices ($$v_{S,1},v_{S,2},...,v_{S,i}$$) would be compressed into supernodes. Shown in **Fig.7**.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/18.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
In this way, each edge in the original graph would be compressed without omission. And the edges'quantity of the compressed graph, is equal to vertex covering's elements quantity of the original graph. Therefore, the problem of finding the minimum edge compression was transformed into the problem of finding the minimum vertex covering.

**Theorem 1**
For an undirected, unweighted and connected graph without complete subgraph, the minimum edges'quantity of the compressed graph, is the minimum vertex covering's elements quantity of the original graph: $$\#(E_{\min}) = \#(S_{\min})$$ Where $$\#(E_{\min})$$ is the minimum edges' quantity of the compressed graph and $$\#(S_{\min})$$ is the the minimum vertex covering's elements quantity of the original graph.

**Proof.** $$\#(E_{\min}) = \#(S_{\min})$$:

**Case 1**: suppose that the edges quantity of the compressed graph $$\#\left(E_{\min }\right)=n+k$$, is greater than the elements quantity of the original graph's minimum vertex covering $$\#\left(S_{\min }\right)=n$$, where $$n$$, $$k$$ are positive integers.

In this case, in the compressed graph, $n + k$ edges were connected with $$n$$ vertices belong to $$S_{min}$$ (Because vertices of $$S_{min}$$ cover all edges, there is not any edge whose two ends are not connected to any $$v_{S,i}$$). According to the combination principle, at least $$k$$ edges are connected to repeated vertices. This contradicts Rule 3. Hence, the excess $$k$$ edges will be further compressed by **Rule 3** until the total number of edges is no longer greater than $$n$$. **Case 1** does not hold.

**Case 2**: suppose that the edges quantity of the compressed graph $$\#\left(E_{\min }\right)=n-k$$, is less than the elements quantity of the original graph's minimum vertex covering $$\#\left(S_{\min }\right)=n$$, where $$n$$, $$k$$ are positive integers and $$n > k$$.

In this case, to keep $$n$$ vertices undirected graph connected needs at least $$n-1$$ edges, and there is no cycle in such a graph. (It is easily proved by mathematical induction). By the definition of tree, such an acyclic undirected connected graph is also a tree. For a tree structrued by $$v_{i}$$, the degree of leaves are $$1$$. This is contradicts that $$S_{min}$$ is a minimum vertex covering. Because if the degree of a vertex $$a$$ is 1, the unique edge connected with $$a$$ could be covered by the neighbour of $$a$$, the appropriate element of $$S_{min}$$ is not $$a$$, but its neighbour. **Case 2** does not hold.

As the above, $$\#(E_{\min})$$ can not be greater or less than $$\#(S_{\min})$$. Hence $$\#(E_{\min})$$ can only be equal to $$\#(S_{\min})$$.

**Proven**.

## The compression of Tree graphs
### Compression algorithm
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/19.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
**lemma 1**
If $$T$$ is a tree and $$v$$ is a leaf, and $$u$$ is the only point where $$v$$ is connected, then there exists Minimum point coverage containing $$u$$.

**Proof.** Considering minimum vertex covering, $$S$$, Let $$e=u-v$$ be the only associated edge. Obviously at least one of $$u$$ and $$v$$ is in $$S$$, otherwise $$e$$ cannot be covered. If $$u \in S$$, then **lemma 1** is true. If $$v \in S$$, then we delete $$v$$ from $$S$$ and insert $$u$$ to get another point coverage of the same size.

Since $$u \in S$$, then $$S-u$$ must be a minimum point cover of $$T-u$$, $$v$$ (tree $$T$$ removes points $$u$$, $$v$$ and all edges incident to $$u$$,$$v$$. Then we can calculate the minimum vertex covering of $$T-u$$,$$v$$. Thus, our **Algorithm 1** holds.

### The analysis of time complexity
A $$n$$ vertex tree $$T$$ would be input as a $$n \times n$$ adjacency matrix.

**Step 1**: the matrix was traversed to find all the rows with only one non-zero element. The identifiers of these rows were the identifiers of leaves in the tree. The time complexity of this step was $$O(n^{2})$$.

**Step 2**: the column identifiers of non-zero element in these leafrows were find. These identifiers were the previous generation of leaves. They were a part of the minimum vertex covering $$S_{min}$$. A set $$S_{min}$$ was created to store these found identifiers. Then these leaves columns and rows were deleted. Then, in the remaining matrix, these vertices connected to the $$S_{min}$$ were found, but them would not be stored in $$S_{min}$$. Them were seemed as the new leaves to be processed in a new turn of loop as same as the above, and deleting rows and columns of vertices added into $$S_{min}$$ last time (deleting elements in matrix, not in $$S_{min}$$). In this step, because of the loop, the time complexity was $$O(kn^{2})$$, where $$k$$ is a constant.

**Step 3**: when the process reached the root, a special situation, the remaining matrix was $$\left(\begin{array}{ll}0 & 1 \\ 1 & 0\end{array}\right)$$, may arise. If it happens, either of the last two points was added to $$S_{min}$$ and the other was deleted. If it does not happen, the whole process was continuely completed as **Step 2**. This step has a time complexity of $$O(1)$$.

Therefore, the time complexity of the algorithm was the level of $$O(n^{2})$$. It could be completed in a polynomial time. An example was shown in **Fig.8**:
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/20.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## The compression of Grid graphs
### Compression algorithm
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/21.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
From **theorem 1**, the minimum edges 'quantity of the compressed graph, is the minimum vertex covering's elements quantity of the original graph. Therefore, for a grid graph, to find the minimum edge compression is to find the minimum point cover or the maximum independent set.

If $$G$$ is a grid and $$u$$ is a node which has two edges, and $$v$$ is the point where $$u$$ is connected, then there must be points on the opposite side that are not connected to $$u$$, and there must also be points on the opposite side of these points that are independent of each other, and these points will eventually form the maximum independent set.

Since $$u ∈ N$$, then $$N-u$$ must be a maximum independent set of $$G-u$$,$$v$$ (grid $$G$$ removes points $$u$$, $$v$$ and all edges incident to $$u$$,$$v$$. Then we can calculate the maximum independent set of $$G-u$$,$$v$$. Thus, our **Algorithm 2** holds.

### Example of reduction
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/22.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### The analysis of time complexity

The above algorithm is the way to find the compression of the grid graphs $$G$$.

**Step 1** *Set complementary sets*: the sets generated as $$$U,V$$$ are maximum independent set and the set of minimum vertex covering. The complementary property of the sets can therefore separate the complete vertexes. The time complexity of this step was $$O(2)$$, which can be recorded as $$O(1)$$.

**Step 2** *Input nodes*: As shown in the previous proof of the transferable between the grid graph and the general graph, it could be shown that the connection between the vertex can be refer to as edge. Referring to the step of finding $$u$$, the symbol is to check if the vertex have and only have to edges. As in the algorithm shows, as we found out $$u$$ and $$v$$, we then delete the edges linked. The latter work to discover $$u$$ and $$v$$ is therefore turn out to be the same way referring to find out the vertex with two edges. In the previous analysis of time complexity where used matrix to visualize the connection the tree graph, we could use the same idea here to consider the connection of grid graph.
As shown in the above figure, the time complexity can be computed as

$$\textbf{time complexity} = O(1*n)+O(2*n)+...++O(k*n)$$ where $$k \rightarrow n$$.

It could be calculated as

$$\textbf{time complexity}= O(\frac{n(n+1)}{2}n)$$.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/23.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
Therefore, the time complexity of this step can be shown as $$O(n^{3})$$.

**Step 3** *Find out minimum*: As demonstrated in the previous proof the minimum of the maximum independent set and the set of minimum vertex covering, shown as $$U,V$$ here, is equalled to the minimal of edges reduction. In the final step, checked the minimum of the $U,V$. This step the time complexity can be recorded as $$O(1)$$.

Therefore, the time complexity of the algorithm was the level of $$O(n^{3})$$. It could be completed in a polynomial time.

## The equivalence

We have found algorithms suitable for compressing different types of graphs to minimum edges. We will now show that finding minimal edge compression in general graphs is the NP- Complete problem, which is equivalent to the problems of finding minimal vertex covers and complete subgraphs in general graphs, both of which are NP-Complete.

The vertex cover problem is known to be a NP-Complete problem, it was one of the 21 NP-complete problems proposed by Karp \[1\]. It is frequently used as a starting point for NP-hardness proofs in computational complexity theory. For the proof, we could determine whether there is a subset V' of vertices of size at most k such that every edge in the graph is connected to a vertex in V', given a graph $$G(V, E)$$ and a positive integer $$k$$. The goal is to see if $$G$$ has a vertex cover with a maximum size of $$k$$. Because an NP-Complete problem is defined as one that is both in NP and NP hard, the proof that a problem is NP-Complete could be divided into two parts: First to prove that vertex cover is in NP and second to prove that vertex cover is in NP-Hard. It is stated by K. Biswas and S.A.M. Harun that finding a minimum vertex cover of a graph is NP-Complete \[2\]. Also, B. Brešar, F. Kardoš, J. Katrenič, and G. Semanišin have demonstrated that the k-Path Vertex Cover Problem is NP-complete for any fixed integer $$k≥ 2$$ \[3\]. However, S. Davis and S. Russell have certified that MIN-VERTEX-COVER is NP-hard, which means that it isn't even in NP \[4\].

As for the node-deleted complete subgraph problem, it has already been shown to be NP- complete \[1\]. This also been reiterated by Krishnamoorthy, M. and Deo, N., when the input graph is limited to be planar, the node-deleted \"complete\" subgraph problem can be handled in polynomial time \[5\]. This is based on the fact that for planar graphs, solutions to the maximum clique problem can be found in polynomial time \[6\].

## Conclusion

In conclusion, for general graphs, excluding node-deleted complete subgraph, under the compression rule that allowed nodes to be overlapped and edges to go into supernodes, finding the lowest number of edges is equivalent to finding the number of the MIN-VERTEX-COVER. As for two specific kinds of graph, tree and grid, excluding node-deleted complete subgraph, we have discussed algorithm 1 and 2 to find their MIN-VERTEX-COVER. Furthermore, the time complexity of these two algorithm has been discussed following. However, the node-deleted complete subgraph problem is NP-complete.

## References
\[1\] R.M.Karp, Reducibility among Combinatorial Problems, Complexity of Computer Computations, R.E. Miller and J. W. Thatcher, eds., Plenum Press, NY, 1972, pp. 85-104.

\[2\]K. Biswas and S.A.M. Harun, "Constraint Minimum Vertex Cover in K-Partite Graph Approximation Algorithm and Complexity Analysis", International Journal of Computer Science and Information Security, vol.4, no.12, 2009

\[3\]B. Brešar, F. Kardoš, J. Katrenič, and G. Semanišin, "Minimum k-path vertex cover," Discrete Applied Mathematics, vol. 159, no. 12, pp. 1189--1195, Jul. 2011

\[4\]S. Davis and S. Russell, "NP-Completeness of Searches for Smallest
Possible Feature Sets," AAAI Technical Report FS-94-02, 1994, pp.37-39

\[5\]Krishnamoorthy, M. and Deo, N., 1979. Node-Deletion NP-Complete Problems
\| SIAM Journal on Computing \| Vol. 8, No. 4 \| Society for Industrial
and Applied Mathematics\

\[6\]S. A. COOK, The complexity of theorem---proving procedures, Proc. of
Third Annual ACM Symp. on Theory of Computing, 1970, pp. 151-158.
