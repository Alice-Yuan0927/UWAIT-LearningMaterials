# CITS4403 Final Examination 2016: English Answers

Suggested answers for revision, not an official marking guide. Questions are in bold; answers are in plain text.

**Q1. Explain how software libraries and their dependencies could be represented as a graph. What properties would you expect this graph to have. [5 marks]**

Represent each library as a node. Add a directed edge A to B when library A depends on library B. Following outgoing edges then reveals direct and indirect requirements. In-degree counts how many libraries directly depend on a library; out-degree counts its direct dependencies.

Expect a sparse, uneven network: many specialised libraries have few dependants, while a few common utility libraries act as hubs. It may have layers and modules. A dependency system may enforce an acyclic graph, but cycles are possible unless explicitly forbidden. A heavy-tailed degree distribution is plausible, not guaranteed solely by this representation.

**Q2. Give two different methods for generating random graphs, and explain the difference in the types of graphs that they generate. [5 marks]**

In G(n,p), create n nodes and add each possible edge independently with probability p. The number of edges varies between runs.

In G(n,m), create n nodes and choose exactly m distinct edges uniformly from all n(n-1)/2 possible edges. Every generated graph has exactly m edges.

The first model fixes an edge probability; the second fixes the edge count. Setting m equal to the expected edge count of G(n,p) makes their averages comparable, but does not make the models identical.

**Q3. Describe an algorithm for determining the average shortest path length between any two vertices in a graph. [5 marks]**

For a connected, unweighted, undirected graph, run breadth-first search from every node. Each BFS gives distances from its source to all other nodes. Sum distances over unordered pairs u<v, then divide by the number of pairs, n(n-1)/2. Equivalently, sum ordered distinct pairs and divide by n(n-1).

Use adjacency lists and a FIFO queue. Do not include a node's distance to itself. If the graph is disconnected, some distances are infinite; report that the whole-graph average is not finite, or explicitly restrict the calculation to a chosen connected component.

**Q4. What is the order of growth of the algorithm you described in question 3. [5 marks]**

One BFS takes O(n+m) time with adjacency lists. Repeating it for all n source nodes takes O(n(n+m)) time. For a sparse connected graph with m=O(n), this is O(n^2). For a dense graph with m=O(n^2), it is O(n^3).

If distances are summed after each BFS, rather than storing every distance table, the extra working space is O(n), excluding the graph itself. The stated time bound applies to the unweighted BFS algorithm in Question 3.

**Q5. Describe an efficient implementation of the Dictionary (or Map) data structure. What is the complexity of the three main operations. [5 marks]**

An efficient dictionary can use a hash table. Hash the key to choose a bucket, then store the key-value pair there. Handle collisions using a bucket list or an open-addressing scheme, and resize the table when its load factor becomes too high.

Lookup, insertion or update, and deletion take expected O(1) time with a suitable hash function and a controlled load factor. Insertions are amortised O(1) because occasional resizing is expensive. In the worst case, many collisions can make an operation take O(n) time.

**Q6. Describe Schelling's model of racial segregation, and what its significance is. [5 marks]**

Place two types of residents and some empty homes on a grid. Each resident checks the fraction of occupied neighbours of its own type. A resident who falls below a modest satisfaction threshold moves to an empty home. Repeat the process; residents with no occupied neighbours need an explicit convention.

Large same-type regions can form even when residents accept mixed neighbourhoods and nobody aims to segregate the whole city. Each move changes other residents' neighbourhoods, creating feedback. The model shows that mild local preferences can be sufficient for strong segregation. It does not prove that racism is absent from real housing patterns.

**Q7. Describe the long tail property and give two different systems where this property may arise. [5 marks]**

A long-tailed distribution contains many small or common values and relatively few extremely large values, but those extremes remain important. In the usual heavy-tail interpretation, the upper tail decays more slowly than an exponential, so extreme values are much less negligible than in a thin-tailed distribution.

Examples include the number of links to web pages, where a few pages are huge hubs, and wealth, where a small number of people hold very large amounts. A long tail does not automatically mean an exact power law, and a log-log plot alone does not prove one.

**Q8. What is the demarcation problem. Explain how Popper proposed to address the demarcation problem. [5 marks]**

The demarcation problem asks how to distinguish science from pseudoscience or other non-scientific claims. Popper proposed falsifiability as the key criterion. A scientific claim must risk being wrong: there must be a possible observation or experiment that would contradict it.

For example, one genuine counterexample would refute the claim that all swans are white. A claim that can explain every possible result, and never allows a result to count against it, fails this test. Surviving tests supports a theory provisionally; it does not prove it true.

**Q9. Do you consider Zipf's law to be an explanatory model, and why? [5 marks]**

Zipf's law is mainly descriptive. It summarises a pattern: frequency falls approximately as the inverse of rank. By itself, it does not say what process generated that pattern or why the exponent is near one.

An explanatory model would propose a mechanism, such as a specific process of growth and preferential selection, and show that the observed relationship follows from it. Several different mechanisms can produce similar rank-frequency curves, so fitting Zipf's law alone does not identify the cause.

**Q10. What are the characteristic properties of a Pareto distribution? [5 marks]**

A Pareto distribution is a heavy-tailed distribution for positive values above a minimum x_min. Its upper-tail probability is P(X>=x)=(x_min/x)^alpha for x>=x_min, where alpha>0. Its density is proportional to x^(-(alpha+1)).

Most values are relatively small, but very large values remain more likely than under an exponential tail. The tail is scale-free: multiplying x by a fixed factor changes the tail probability by a fixed factor. Smaller alpha means a heavier tail. The mean is finite only for alpha>1, and the variance only for alpha>2. The 80/20 rule is an example, not a requirement of every Pareto distribution.

**Q11. Explain the differences between randomness and complexity? [5 marks]**

Randomness concerns unpredictability or the use of chance. Complexity concerns rich organisation, interactions and behaviour that are difficult to summarise or predict from individual parts.

A fair sequence of coin tosses is random but need not contain meaningful interacting structures. Conversely, Rule 110 and the Game of Life use deterministic rules yet can produce complex structures and computation. A complex system may include randomness, but randomness is neither required nor sufficient for organised complexity. Some mathematical complexity measures assign high complexity to random strings; the distinction here concerns the course's dynamical and organisational meaning.

**Q12. What is the Church-Turing thesis and how is it related to universality? [5 marks]**

The Church-Turing thesis says that any function calculable by an effective mechanical procedure can be computed by a Turing machine. It links the informal idea of an algorithm to a formal model of computation, so it is a thesis rather than an ordinary theorem about that informal idea.

A universal Turing machine can simulate any other Turing machine when given its encoded program and input. Other universal systems, such as Rule 110, can simulate universal computation too. Universality concerns which computations a system can perform, not whether it performs them efficiently.

**Q13. Describe the four main classes of one dimensional cellular automata. [5 marks]**

Wolfram's four main classes describe typical long-term behaviour:

1. Class 1 settles into a uniform state.
2. Class 2 settles into stable structures or simple repeating patterns.
3. Class 3 produces irregular, chaotic-looking patterns.
4. Class 4 produces persistent, interacting structures within a mixture of order and irregularity. Moving structures can carry information and interact.

These are qualitative categories of the observed dynamics. A deterministic rule can produce Class 3 or Class 4 behaviour; complicated-looking output does not require a random update rule.

**Q14. "In the game of life, all initial states eventually reach a simple repeating pattern." Discuss whether this claim is true or false. [5 marks]**

The claim is false on the usual unbounded grid. Some patterns die out, some become still lifes, and some become oscillators, but these examples do not cover every initial condition. A finite glider gun continually emits gliders. Although the gun itself repeats, the complete pattern contains an increasing number of gliders moving away, so the full configuration does not settle into a fixed repeating state.

Boundary assumptions matter. A deterministic Game of Life on a fixed finite grid has only finitely many configurations, so eventually it must repeat a previous configuration. That finite-state argument does not apply to an unbounded grid.

**Q15. How are scientific realism and instrumentalism related to reductionism and holism? [5 marks]**

Realism versus instrumentalism concerns what a model says about reality. Realism asks whether the theory and its entities describe something that really exists; instrumentalism asks whether the model is useful for its purpose.

Reductionism versus holism concerns how an explanation is organised. Reductionism explains a system through smaller parts and lower-level laws. Holism focuses on interactions, organisation and collective properties.

These distinctions are related but not identical. A realist may regard a higher-level pattern as real, while an instrumentalist may use either a detailed reductionist model or a simple holistic one. There is no necessary one-to-one pairing.

**Q16. Define fractal dimension and give an example of something with non-integer dimension. [5 marks]**

Fractal dimension measures how the detail or occupied mass of a pattern scales when the observation scale changes. In box counting, if N(epsilon) boxes of side epsilon are needed to cover a set and N(epsilon) is proportional to epsilon^-D, then D is its box-counting dimension.

The Sierpinski triangle contains three half-sized copies of itself. Its dimension satisfies 3=2^D, giving D=log(3)/log(2), approximately 1.585. It is more space-filling than a line but does not fill a two-dimensional area.

**Q17. What does it mean to say a system is computationally irreducible? [5 marks]**

It means that, in general, there is no shortcut that predicts the system's detailed outcome substantially faster than carrying out its evolution step by step. Knowing the local rules is not enough to produce a simple formula for every future state.

For example, to determine a particular later configuration of a complex CA, we may have to run the CA through the intervening generations. This does not make it random or uncaused. Nor does it rule out every useful prediction: coarse statistics, special initial states or bounds may still be easier to calculate.

**Q18. What is the fast Fourier transform, and what is its significance? [5 marks]**

The fast Fourier transform is an efficient algorithm for computing the discrete Fourier transform. It converts a sampled signal into frequency components, showing which frequencies are present and their amplitudes and phases. A power spectrum is obtained from squared Fourier magnitudes with the chosen normalisation.

A direct DFT needs O(N^2) work, while common FFT algorithms need O(N log N). This makes long signals practical to analyse. In critical-system studies, spectral analysis can reveal more power at low frequencies and an approximate power-law spectrum, rather than relying only on the appearance of a time-series plot.

**Q19. Describe the sand pile model of Bak, Tang and Wiesenfeld, and what can we infer from it. [5 marks]**

Use a grid of non-negative integer sand heights. Add grains slowly. With K=3, any cell higher than three topples: it loses four grains and gives one to each orthogonal neighbour. Repeat until all cells are stable; grains sent beyond an open boundary are lost. Then add another grain.

A single grain can trigger avalanches of many sizes. The model shows how local threshold rules, slow driving and dissipation can generate self-organized critical behaviour, including broad avalanche-size distributions. It offers a possible mechanism for scale-free events without carefully tuning an external parameter. Similarities do not prove that every real avalanche-like system follows this exact model.

**Q20. Give three characteristics of agent based models. [5 marks]**

First, agents are individual entities with their own states or attributes, which may differ between agents. Second, each agent follows behavioural rules using locally available information rather than requiring central control. Third, agents interact with one another and with an environment, changing the conditions for later decisions.

Repeated interactions can generate collective patterns not specified as an overall instruction. For example, simple resident movement rules can create segregation. An ABM need not have intelligent human-like agents, and neither randomness nor a discrete grid is required in every ABM.

**Q21. Describe how a two dimensional cellular automaton could be used to model crowd dynamics in a crowded train station. [10 marks]**

Divide the station floor into a two-dimensional grid. Each cell is empty floor, a wall or obstacle, an exit, or occupied by one person. Specify the cell size and time step, and start with a chosen crowd density and entry pattern.

Give each occupied cell a destination or direction label. At each step, a person may move into an empty neighbouring floor cell. Prefer moves that reduce distance to the destination, but include a probability of hesitation or a different choice. Use local occupancy to prevent movement through people or walls.

Compute proposed moves from the old grid. If several people choose the same cell, resolve the conflict randomly so that at most one enters. Apply accepted moves together. Remove people who reach their exit and add arrivals at stated entry rates.

Measure exit flow, travel time, queue length and crowd density near bottlenecks. Repeat trials while varying entrance rates, exit widths or obstacle layouts. Compare results with observations. The grid model simplifies body size, pushing and continuous movement, so it should not be treated as a complete description of a real crowd.

**Q22. Do you think the complexity of systems can be objectively measured? Present a reasoned argument for your answer. [10 marks]**

Particular aspects of complexity can be measured objectively once the object, representation and method are specified. Examples include entropy, compression length, fractal dimension, network structure and the resources needed for prediction. Two researchers using the same data and procedure should obtain comparable results.

However, these measures capture different things. A random bit string has high entropy and is difficult to compress, yet may contain little organised structure. A highly ordered repeating sequence is easy to describe. A living system or a Class 4 CA combines regularity, interacting structures and variation, which a single entropy value may not capture.

Measurements also depend on scale and representation. A detailed description of cells may give a different impression from a description of a moving glider. Exact algorithmic complexity is itself not generally computable.

Therefore, I would not claim that one universal number objectively ranks the complexity of every system. I would choose several clearly defined measures that fit the scientific question, state the scale and assumptions, and compare systems using that shared framework.
