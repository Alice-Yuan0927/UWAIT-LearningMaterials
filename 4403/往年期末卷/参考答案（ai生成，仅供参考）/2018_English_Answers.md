# CITS4403 Final Examination 2018: English Answers

Suggested answers for revision, not an official marking guide. Questions are in bold; answers are in plain text.

**Q1. Give pseudocode for an algorithm for determining if a graph is connected or not. [5 marks]**

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

**Q2. Describe, using random graphs, an example of a surprisingly abrupt change in a property of a complex object when only gradual changes are made in parameters that govern the relationships between its components. [5 marks]**

Generate Erdos-Renyi graphs G(n,p) for a fixed large n while gradually increasing p. At very small p, the graph contains isolated nodes and small components. When the mean degree (n-1)p passes about one, a giant connected component appears: a single component contains a substantial fraction of the nodes.

Full connectivity is a different threshold, occurring around p=log(n)/n for large n. Its probability rises sharply from near zero to near one. Thus, a small change in an edge-generation parameter can cause a large change in global structure. Finite graphs have a probabilistic transition, not a guarantee at one exact value.

**Q3. Describe two different explanations for the Small World Phenomenon. [5 marks]**

One explanation is the Watts-Strogatz model. Most links join nearby nodes, forming local groups, but a few long-range shortcuts connect those groups. Even a small number of shortcuts can greatly reduce average path length while preserving high clustering.

A second explanation is the Barabasi-Albert model. The network grows, and new nodes preferentially connect to nodes that already have many links. This creates hubs, which provide short routes between many nodes. The basic BA model explains a broad degree distribution, but usually has less clustering than real social networks.

**Q4. Explain what the single-source shortest path problem is and describe briefly how to solve it. [5 marks]**

The single-source shortest-path problem asks for the shortest distance, and possibly a path, from one chosen node to every other node.

For an unweighted graph, run breadth-first search from the source. Give the source distance zero and each newly discovered neighbour its parent's distance plus one. This finds minimum numbers of edges in O(n+m) time with adjacency lists.

For a graph with non-negative edge weights, use Dijkstra's algorithm instead, repeatedly expanding the node with the smallest tentative distance and relaxing its outgoing edges. Unreachable nodes have infinite distance.

**Q5. Explain the difference between a heavy-tailed distribution and one that follows a power law. [5 marks]**

A heavy-tailed distribution has an upper tail that falls more slowly than an exponential, so extreme values remain relatively likely. A power-law tail has the more specific form P(X>x) approximately C*x^-alpha for large x.

A power law is heavy-tailed, but not every heavy-tailed distribution is a power law. For example, a lognormal distribution is heavy-tailed without having a single asymptotic power-law exponent. A genuine power-law tail is approximately straight on an appropriate log-log tail plot, but a short straight-looking section alone is not sufficient evidence.

**Q6. Explain how to use preferential attachment to create random graphs with a distribution of degrees that obeys a power law. [5 marks]**

Start with a small connected graph. Add one new node at a time and connect it to m distinct existing nodes. Choose each target with probability proportional to its current degree: P(i)=k_i/sum_j(k_j). Avoid self-loops and repeated edges.

Highly connected nodes are therefore more likely to gain further links: a rich-get-richer effect. Combining this preferential attachment with continued growth creates hubs and a broad degree distribution. In the standard BA model, the large-degree tail is approximately P(k) proportional to k^-3. Uniform random attachment does not produce the same tail.

**Q7. Consider the one-dimensional Wolfram-style Cellular Automaton called "Rule 18" operating on an infinite row of cells starting with only one cell on. Draw what the row looks like after 0, 1, 2 and 3 steps. [5 marks]**

Rule 18 has output bits 00010010 for neighbourhoods ordered 111,110,101,100,011,010,001,000. Only neighbourhoods 100 and 001 produce a live cell. Apply the rule synchronously.

Using 1 for a live cell and 0 for a dead cell:

```text
position  -3 -2 -1  0  1  2  3
t = 0      0  0  0  1  0  0  0
t = 1      0  0  1  0  1  0  0
t = 2      0  1  0  0  0  1  0
t = 3      1  0  1  0  1  0  1
```

All cells outside the displayed window are zero at these times. Each row uses only the previous row, not values already updated in the current row.

**Q8. Explain why Wolfram's demonstration of complex behaviour in cellular automata is considered more surprising than the complexity of chaotic systems. [5 marks]**

Chaotic systems can have simple deterministic equations, but their states usually vary continuously. A tiny difference in an initial real-valued state can grow rapidly, making long-term prediction difficult.

Wolfram showed that complex behaviour also arises in systems with discrete time, discrete space, only a few states per cell and a very small local rule. There is no need for continuous variables or finely specified real numbers. This makes the simplicity of the ingredients especially striking: rich patterns and computation can emerge from basic local updates.

**Q9. In the Game of Life, there is no initial condition that yields unbounded growth in the number of live cells. True or False? Explain your answer. [5 marks]**

False. A glider gun starts from a finite pattern and repeatedly emits gliders. The gun continues working while earlier gliders move away. On an unbounded grid, with no obstacles or collisions that destroy the output, more and more gliders remain alive, so the total number of live cells grows without bound.

A single glider is not enough to refute the claim: it moves but keeps a bounded number of live cells. The important feature is repeated production of additional live structures. A finite grid cannot support unlimited growth.

**Q10. Using the Game of Life explain realism versus instrumentalism. [5 marks]**

Scientific realism treats successful theories as attempts to describe what really exists and how it behaves. Instrumentalism treats theories mainly as tools for organising observations and making useful predictions, without requiring their entities to be literally real.

In the Game of Life, a realist can treat a glider as a genuine higher-level structure with a stable identity and behaviour. An instrumentalist can regard the glider as a useful label for a changing pattern of live cells. Both can predict its movement. Their disagreement concerns the interpretation of the pattern, not the update rules.

**Q11. Explain briefly how reaction-diffusion could be responsible for animal patterns. [5 marks]**

Suppose two interacting chemicals spread through developing skin. One acts as an activator that encourages local pigment production and its own production; the other inhibits the process and spreads farther or faster.

Under suitable reaction and diffusion rates, small initial differences grow into a stable spatial pattern. Local activation and longer-range inhibition can produce spots or stripes without a separate instruction for every marking. Different parameters and boundaries produce different patterns. This is a possible mechanism for some animal markings, not a claim that every marking has the same cause.

**Q12. Outline how to simulate percolation with a cellular automaton. [5 marks]**

Use a two-dimensional grid. Independently mark each cell porous with probability p or blocked with probability 1-p. Mark the top row as a wet source boundary. Other cells begin dry.

At each synchronous step, a dry porous cell becomes wet if at least one of its four von Neumann neighbours is wet. Wet cells stay wet, and internal blocked cells never become wet. Stop when the bottom is reached or when no new cells become wet. Reaching the bottom demonstrates a top-to-bottom percolating cluster. Repeat independent grids at different p values to estimate crossing probabilities.

**Q13. Explain how the concept of self-organized criticality might suggest that large earthquakes are unpredictable. [5 marks]**

If a fault system behaves like a self-organized critical system, slow stress accumulation can place it near a state where one small disturbance triggers a cascade. Similar small triggers can produce either a tiny event or a large rupture, depending on the whole interacting system.

There may therefore be no uniquely large trigger or reliable countdown announcing a large earthquake. A heavy-tailed size distribution may help describe long-term risk, while giving little information about the exact time and size of the next event. This is what the model suggests; it does not prove that all earthquake prediction is impossible.

**Q14. Explain how we can use a box counting algorithm to estimate fractal dimension. [5 marks]**

First choose the set to measure, such as cells in a particular state, and turn it into a Boolean mask. Cover it with square boxes of side length epsilon. Count N(epsilon), the number of boxes containing at least one selected cell. Repeat for several box sizes.

For a fractal, N(epsilon) is approximately proportional to epsilon^-D over a useful range of scales. Plot log N against log(1/epsilon); the slope estimates the fractal dimension D. Avoid scales dominated by individual pixels or the finite outer boundary. Check that the scaling persists across several scales and, if possible, larger patterns. One attractive picture or two data points is insufficient.

**Q15. Use an example from the computational modelling course to explain and illustrate the idea of an emergent property. [5 marks]**

An emergent property is a collective property produced by interactions, rather than a property or explicit goal of one component. In Boids, each agent uses local separation, alignment and cohesion rules. No agent is given a global picture of the flock or instructed to create a particular formation.

Nevertheless, many agents can organise into coordinated moving groups. Flocking is the emergent property: it belongs to the interacting population, not to an isolated boid. The explanation lies in the feedback between local decisions and the changing arrangement of neighbours.

**Q16. Explain how Schelling's model of segregation is a holistic model rather than a reductionist one. [5 marks]**

A holistic model focuses on interactions and collective behaviour, rather than expecting the whole system to be understood by studying one component in isolation. It may deliberately simplify individual components to retain the relationships that matter.

For example, Schelling's model gives residents very simple preferences and movement rules. The main question is how their repeated interactions change the whole neighbourhood. Large segregated regions can appear even though no resident is instructed to create them. A reductionist approach would focus more on detailed explanations of individual behaviour; the two approaches can complement each other.

**Q17. A very simple agent-based model of traffic evenly spread out along a road could easily seriously overestimate the flow. Explain how making a slightly more complicated, and slightly more realistic model of individual car behaviour, can suggest much more realistic and much lower traffic flows. [5 marks]**

A perfectly regular model can keep cars evenly spaced and moving smoothly, producing an unrealistically high flow. Add small random variations to individual driving, such as occasional slowing, while limiting each car's speed according to the gap ahead.

One driver's slowdown makes the following driver brake; the disturbance can grow into a backward-moving stop-and-go wave. Cars then spend time moving slowly or stopping, so average speed and flow fall even without an accident or obstruction. Run past the initial transient and compare distance travelled per unit time at the same road density.

**Q18. Explain how it is possible to make a reasonably realistic model of a complex object like a flock of birds by just making a simple model of an individual bird. [5 marks]**

Boids model a flock using individual agents with positions and velocities. Each boid responds only to nearby neighbours, usually within a limited distance and field of view. Separation avoids crowding, alignment adjusts velocity towards neighbours' velocities, and cohesion steers towards their local centre.

Combine these steering effects with stated weights, update movement, and repeat. No leader or global flock shape is prescribed. Coordinated group motion emerges from local interactions. This makes Boids a typical agent-based model: autonomous individuals follow simple rules in an environment and produce collective behaviour.

**Q19. Outline some of the mechanisms necessary for a process of evolution to allow agents to adapt to an environment. [5 marks]**

Three features are needed:

1. Replication with inheritance: agents produce offspring that retain their characteristics.
2. Variation: individuals differ, and mutation or another mechanism can introduce new inherited differences.
3. Differential survival or reproduction: those differences affect the chance of surviving or leaving offspring.

Selection can then change the population's inherited characteristics over generations. Copying alone produces no new variation, and variation without fitness-related selection does not by itself produce adaptation to the environment.

**Q20. Explain how simulations of evolution can be used for optimisation, for example finding the arguments that give the maximum value of a function. [5 marks]**

Represent each candidate argument vector x as an agent's genotype. Define fitness from the objective f(x), with higher objective values producing greater selection probability. Start with a varied population of valid candidates.

Evaluate fitness, favour better candidates as parents, copy their genotypes, and apply mutation; crossover may also be used. Enforce the argument constraints and repeat for many generations. Keep track of the best solution found and repeat the search from different starting populations. If raw objective values are negative, convert them to valid selection weights, for example using ranks. The method searches for good solutions but does not guarantee a global optimum.

**Q21. Suppose that we have a population of agents capable of using a strategy to play the iterated Prisoner's Dilemma. Suppose we allow the strategies to evolve with fitness governed by success at the game. Describe some of the interesting population changes that may be observed. [5 marks]**

In the course simulations, an initially defecting population can be invaded by more cooperative strategies. Cooperative agents can benefit from playing one another, raising average fitness. But a population that becomes too trusting can be invaded by defectors, so cooperation and average fitness may rise and fall rather than settle at one fixed optimum.

Mutation introduces strategies with different amounts of cooperation, retaliation and forgiveness. Retaliation can help protect cooperation, and not every agent must retaliate if enough of the population does. TFT need not dominate an evolving population. These are possible, parameter-dependent dynamics, not fixed numerical outcomes for every implementation.

**Q22. Explain the "problem of nice". Describe a solution. [5 marks]**

The problem of nice is the apparent conflict between cooperation and individual advantage. In a one-round Prisoner's Dilemma, defection gives the better individual payoff whatever the opponent does. More broadly, if helping costs an individual and benefits others, selfish individuals seem likely to outcompete helpers. Why, then, does altruism persist?

One solution is reciprocal cooperation in repeated encounters. Tit for tat cooperates first, retaliates after defection, and resumes cooperation when the opponent cooperates. Cooperation can then bring repeated benefits, while retaliation limits exploitation. Under suitable conditions, cooperative traits can improve long-term reproductive success. This is a possible explanation, not a guarantee that unconditional kindness always wins.

**Q23. Briefly review a chapter of a popular non-fiction book that you have read recently covering a topic related to complexity science. [10 marks]**

Sample review: "The Butterfly Effect", in James Gleick's Chaos: Making a New Science.

The chapter introduces Edward Lorenz's work on weather models and sensitivity to initial conditions. A small difference in the starting state can grow into a large difference in the later result. The central lesson is that deterministic rules do not guarantee reliable long-term prediction.

This connects to the course distinction between deterministic and predictable systems. It also explains why a simulation needs carefully specified initial conditions and why repeated or ensemble runs can be more informative than one forecast.

The chapter's strength is its accessible account of how a surprising computational result changed scientific thinking. Its limitation is that a vivid story is not a full mathematical treatment. Sensitivity alone should not be used as a complete definition of every kind of complexity. Overall, the chapter gives a clear entry point into chaos while leaving the formal analysis to further study.

This is an example review; use a chapter you have actually read when answering a personal-reading question.

Reference: [James Gleick's book page](https://around.com/chaos/); [publisher information](https://www.penguinrandomhouse.com/books/321477/chaos-by-james-gleick/).
