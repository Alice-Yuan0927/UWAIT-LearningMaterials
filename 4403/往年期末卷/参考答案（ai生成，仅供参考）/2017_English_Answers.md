# CITS4403 Final Examination 2017: English Answers

Suggested answers for revision, not an official marking guide. Questions are in bold; answers are in plain text.

**Q1. Explain how to construct a regular graph of size n and degree k when k is even (and less than n). [5 marks]**

Put n nodes around a circle. Connect each node to the next k/2 nodes clockwise and the next k/2 nodes anticlockwise, counting each undirected edge only once. For example, when k=4, each node connects to the two nodes on either side of it. Use wrap-around at the ends of the numbering. Because k is even and k<n, these neighbours are distinct. Every node has degree k, and the graph has nk/2 edges.

**Q2. Give two different methods for generating random graphs, and explain the difference in the types of graphs that they generate. [5 marks]**

In G(n,p), create n nodes and add each possible edge independently with probability p. The number of edges varies between runs.

In G(n,m), create n nodes and choose exactly m distinct edges uniformly from all n(n-1)/2 possible edges. Every generated graph has exactly m edges.

The first model fixes an edge probability; the second fixes the edge count. Setting m equal to the expected edge count of G(n,p) makes their averages comparable, but does not make the models identical.

**Q3. Give pseudocode for an algorithm for determining if a graph is connected or not. [5 marks]**

For an undirected graph, start at any node and use breadth-first search to find every node reachable from it. Mark a node when it is first added to the queue. The graph is connected if and only if every node is reached.

```text
is_connected(G):
    if G has no nodes:
        return True  # convention for this algorithm
    start = any node in G
    visited = {start}
    queue = FIFO queue containing start
    while queue is not empty:
        u = queue.remove_front()
        for each neighbour v of u:
            if v is not in visited:
                visited.add(v)
                queue.add_back(v)
    return size(visited) == number_of_nodes(G)
```

The empty-graph case is handled by the stated convention. For a directed graph, this test alone does not establish strong connectivity.

**Q4. What is the order of growth of the algorithm you described in question 3? [5 marks]**

With adjacency lists, breadth-first search takes O(n+m) time, where n is the number of nodes and m is the number of edges. Each node enters the queue at most once. Each undirected edge is inspected at most twice, once from each endpoint. The visited set and queue use O(n) extra space. With an adjacency matrix, scanning a whole row for each node instead gives O(n^2) time.

**Q5. Describe an efficient implementation of the Dictionary (or Map) data structure. What is the complexity of the three main operations? [5 marks]**

An efficient dictionary can use a hash table. Hash the key to choose a bucket, then store the key-value pair there. Handle collisions using a bucket list or an open-addressing scheme, and resize the table when its load factor becomes too high.

Lookup, insertion or update, and deletion take expected O(1) time with a suitable hash function and a controlled load factor. Insertions are amortised O(1) because occasional resizing is expensive. In the worst case, many collisions can make an operation take O(n) time.

**Q6. Explain what the single-source shortest path problem is and describe briefly how to solve it. [5 marks]**

The single-source shortest-path problem asks for the shortest distance, and possibly a path, from one chosen node to every other node.

For an unweighted graph, run breadth-first search from the source. Give the source distance zero and each newly discovered neighbour its parent's distance plus one. This finds minimum numbers of edges in O(n+m) time with adjacency lists.

For a graph with non-negative edge weights, use Dijkstra's algorithm instead, repeatedly expanding the node with the smallest tentative distance and relaxing its outgoing edges. Unreachable nodes have infinite distance.

**Q7. Describe two different explanations for the Small World Phenomenon. [5 marks]**

One explanation is the Watts-Strogatz model. Most links join nearby nodes, forming local groups, but a few long-range shortcuts connect those groups. Even a small number of shortcuts can greatly reduce average path length while preserving high clustering.

A second explanation is the Barabasi-Albert model. The network grows, and new nodes preferentially connect to nodes that already have many links. This creates hubs, which provide short routes between many nodes. The basic BA model explains a broad degree distribution, but usually has less clustering than real social networks.

**Q8. Explain how the "cliquishness" of a graph can be measured by a clustering coefficient. [5 marks]**

For a node u with k neighbours, there are k(k-1)/2 possible undirected edges between those neighbours. Count the number e that actually exist. Its local clustering coefficient is C(u)=e/[k(k-1)/2].

A value near one means that most of its neighbours know one another, so the neighbourhood is highly cliquish. A value near zero means few neighbours are connected. Average local coefficients to summarise the graph. For k<2, the coefficient is undefined in the course implementation; omit NaN values when averaging rather than silently changing the convention.

**Q9. What is Zipf's law? [5 marks]**

Zipf's law describes a rank-frequency relationship. Rank items from most frequent to least frequent. The frequency of the item at rank r is approximately proportional to 1/r: f(r)=C/r. Thus, the second-ranked item occurs about half as often as the first, and the third about one third as often.

Word frequencies are a common example. A log-log plot of frequency against rank is approximately a straight line with slope -1. This is a statement about rank and frequency, not directly a probability density over word counts.

**Q10. Do you consider Zipf's law to be an explanatory model, and why? [5 marks]**

Zipf's law is mainly descriptive. It summarises a pattern: frequency falls approximately as the inverse of rank. By itself, it does not say what process generated that pattern or why the exponent is near one.

An explanatory model would propose a mechanism, such as a specific process of growth and preferential selection, and show that the observed relationship follows from it. Several different mechanisms can produce similar rank-frequency curves, so fitting Zipf's law alone does not identify the cause.

**Q11. Explain how to use "preferential attachment" to create random graphs with a distribution of degrees that obeys a power law. [5 marks]**

Start with a small connected graph. Add one new node at a time and connect it to m distinct existing nodes. Choose each target with probability proportional to its current degree: P(i)=k_i/sum_j(k_j). Avoid self-loops and repeated edges.

Highly connected nodes are therefore more likely to gain further links: a rich-get-richer effect. Combining this preferential attachment with continued growth creates hubs and a broad degree distribution. In the standard BA model, the large-degree tail is approximately P(k) proportional to k^-3. Uniform random attachment does not produce the same tail.

**Q12. What is the demarcation problem? Explain how Popper proposed to address the demarcation problem. [5 marks]**

The demarcation problem asks how to distinguish science from pseudoscience or other non-scientific claims. Popper proposed falsifiability as the key criterion. A scientific claim must risk being wrong: there must be a possible observation or experiment that would contradict it.

For example, one genuine counterexample would refute the claim that all swans are white. A claim that can explain every possible result, and never allows a result to count against it, fails this test. Surviving tests supports a theory provisionally; it does not prove it true.

**Q13. Define one-dimensional Cellular Automata. [5 marks]**

A one-dimensional cellular automaton consists of a row of cells, each with a state from a finite set. Time advances in discrete steps. At each step, every cell's next state is determined by the same local rule, using its old state and the old states of nearby cells. Cells are normally updated simultaneously.

In an elementary binary CA, the inputs are the left, centre and right cells, each either zero or one. There are eight input configurations and 256 possible rules. Specify boundaries for a finite row; stacking successive rows gives a space-time diagram.

**Q14. Explain why Wolfram's demonstration of complex behaviour in cellular automata is more surprising than the complexity of chaotic systems. [5 marks]**

Chaotic systems can have simple deterministic equations, but their states usually vary continuously. A tiny difference in an initial real-valued state can grow rapidly, making long-term prediction difficult.

Wolfram showed that complex behaviour also arises in systems with discrete time, discrete space, only a few states per cell and a very small local rule. There is no need for continuous variables or finely specified real numbers. This makes the simplicity of the ingredients especially striking: rich patterns and computation can emerge from basic local updates.

**Q15. In the Game of Life, there is no initial condition that yields unbounded growth in the number of live cells. True or False? Explain your answer. [5 marks]**

False. A glider gun starts from a finite pattern and repeatedly emits gliders. The gun continues working while earlier gliders move away. On an unbounded grid, with no obstacles or collisions that destroy the output, more and more gliders remain alive, so the total number of live cells grows without bound.

A single glider is not enough to refute the claim: it moves but keeps a bounded number of live cells. The important feature is repeated production of additional live structures. A finite grid cannot support unlimited growth.

**Q16. Explain how a Cellular Automaton can produce an object of dimension about 1.56. [5 marks]**

Run an elementary CA such as Rule 18 from one live cell on an otherwise empty row. Place each new generation below the previous one. The resulting space-time pattern has repeated triangular structure and holes on several scales.

Count the live cells M(L) in growing portions of this pattern. If M(L) is approximately proportional to L^D, the slope of log M against log L estimates D. Rule 18 gives a value around 1.56-1.58, depending on the finite sample. The ideal triangular scaling gives log(3)/log(2), about 1.585. This dimension belongs to the space-time pattern, not to one individual row.

**Q17. How are Scientific Realism and Instrumentalism related to Reductionism and Holism? [5 marks]**

Realism versus instrumentalism concerns what a model says about reality. Realism asks whether the theory and its entities describe something that really exists; instrumentalism asks whether the model is useful for its purpose.

Reductionism versus holism concerns how an explanation is organised. Reductionism explains a system through smaller parts and lower-level laws. Holism focuses on interactions, organisation and collective properties.

These distinctions are related but not identical. A realist may regard a higher-level pattern as real, while an instrumentalist may use either a detailed reductionist model or a simple holistic one. There is no necessary one-to-one pairing.

**Q18. Explain how the concept of self-organized criticality might suggest that large earthquakes are unpredictable. [5 marks]**

If a fault system behaves like a self-organized critical system, slow stress accumulation can place it near a state where one small disturbance triggers a cascade. Similar small triggers can produce either a tiny event or a large rupture, depending on the whole interacting system.

There may therefore be no uniquely large trigger or reliable countdown announcing a large earthquake. A heavy-tailed size distribution may help describe long-term risk, while giving little information about the exact time and size of the next event. This is what the model suggests; it does not prove that all earthquake prediction is impossible.

**Q19. What is the fast Fourier transform, and what is its significance? [5 marks]**

The fast Fourier transform is an efficient algorithm for computing the discrete Fourier transform. It converts a sampled signal into frequency components, showing which frequencies are present and their amplitudes and phases. A power spectrum is obtained from squared Fourier magnitudes with the chosen normalisation.

A direct DFT needs O(N^2) work, while common FFT algorithms need O(N log N). This makes long signals practical to analyse. In critical-system studies, spectral analysis can reveal more power at low frequencies and an approximate power-law spectrum, rather than relying only on the appearance of a time-series plot.

**Q20. Explain how Boids are typical agent-based models. [5 marks]**

Boids model a flock using individual agents with positions and velocities. Each boid responds only to nearby neighbours, usually within a limited distance and field of view. Separation avoids crowding, alignment adjusts velocity towards neighbours' velocities, and cohesion steers towards their local centre.

Combine these steering effects with stated weights, update movement, and repeat. No leader or global flock shape is prescribed. Coordinated group motion emerges from local interactions. This makes Boids a typical agent-based model: autonomous individuals follow simple rules in an environment and produce collective behaviour.

**Q21. Explain how you might find a good solution to the iterated prisoner's dilemma problem. [5 marks]**

Represent a strategy as a rule that chooses cooperation or defection from the opponent's earlier actions. Test candidate strategies in repeated matches against a varied set of opponents and score their average payoffs. TFT is a useful starting candidate: cooperate first, then copy the opponent's previous move.

An evolutionary search can improve or discover strategies. Encode their rules as genotypes, initialise a varied population, play tournaments, select higher-scoring strategies to reproduce, and introduce mutation. Repeat and test the resulting strategies against opponents not used during selection, including noisy play. Success depends on the opponents and rules; there is no guaranteed universally best strategy.

**Q22. Discuss the claim that emergence is just ignorance. [5 marks]**

The claim has some force: we may call a pattern emergent simply because we do not yet understand how it follows from lower-level rules. Better knowledge could explain some apparently mysterious behaviour.

However, emergence can also describe a real distinction between levels of organisation. A traffic jam is a collective pattern created by interacting drivers, not a property of one driver. Even when all local rules are known, predicting their combined result may require running the simulation rather than using a short formula.

Therefore, emergence should prompt a search for mechanisms, not replace one. It is neither automatically ignorance nor proof of something beyond physical rules.

**Q23. Briefly review a chapter of a popular non-fiction book that you have read recently covering a topic related to complexity science. [10 marks]**

Sample review: "The Butterfly Effect", in James Gleick's Chaos: Making a New Science.

The chapter introduces Edward Lorenz's work on weather models and sensitivity to initial conditions. A small difference in the starting state can grow into a large difference in the later result. The central lesson is that deterministic rules do not guarantee reliable long-term prediction.

This connects to the course distinction between deterministic and predictable systems. It also explains why a simulation needs carefully specified initial conditions and why repeated or ensemble runs can be more informative than one forecast.

The chapter's strength is its accessible account of how a surprising computational result changed scientific thinking. Its limitation is that a vivid story is not a full mathematical treatment. Sensitivity alone should not be used as a complete definition of every kind of complexity. Overall, the chapter gives a clear entry point into chaos while leaving the formal analysis to further study.

This is an example review; use a chapter you have actually read when answering a personal-reading question.

Reference: [James Gleick's book page](https://around.com/chaos/); [publisher information](https://www.penguinrandomhouse.com/books/321477/chaos-by-james-gleick/).
