# CITS4403 Final Examination 2024: English Answers

Suggested answers for revision, not an official marking guide. Questions are in bold; answers are in plain text.

**Q1. Describe the steps to construct a Watts-Strogatz Graph. [4 marks]**

Place n nodes around a circle. Initially connect each node to the k/2 nodes immediately on either side, so every node has k neighbours; use an even k<n.

Consider each original undirected edge once. With probability p, keep one endpoint fixed and reconnect the other to a randomly chosen legal node. Exclude self-loops and duplicate edges. The number of edges stays the same, although individual degrees can change. A small amount of rewiring introduces long-range shortcuts while retaining many local links.

**Q2. Compare how the Watts-Strogatz and Barabasi-Albert models explain the "small world" phenomenon in social networks. [6 marks]**

One explanation is the Watts-Strogatz model. Most links join nearby nodes, forming local groups, but a few long-range shortcuts connect those groups. Even a small number of shortcuts can greatly reduce average path length while preserving high clustering.

A second explanation is the Barabasi-Albert model. The network grows, and new nodes preferentially connect to nodes that already have many links. This creates hubs, which provide short routes between many nodes. The basic BA model explains a broad degree distribution, but usually has less clustering than real social networks.

**Q3. Explain the key differences between 1-dimensional and 2-dimensional Cellular Automata. [6 marks]**

A 1D CA has a line of cells; a 2D CA has a grid extending in two spatial directions. An elementary binary 1D CA reads the left, centre and right cells. A 2D CA often uses four von Neumann neighbours or eight Moore neighbours, together with the centre state where needed.

Both use local rules and discrete time, usually updating synchronously. A 1D evolution is often displayed by stacking generations vertically: the vertical direction represents time, not a second spatial dimension. A 2D evolution is usually shown as successive frames.

For binary states, three-cell inputs give 8 configurations and 256 possible rules. A full 3-by-3 input gives 512 configurations and 2^512 possible rules. Neither dimension inherently requires binary states.

**Q4. In a 2-D CA simulating percolation, cells are porous with probability p and non-porous otherwise. All cells begin dry except the wet top row. A porous cell becomes wet if it has a wet von Neumann neighbour; non-porous cells stay dry. (a) How can one check if a randomly initialised array contains a percolating cluster? [3 marks] (b) Describe the process to estimate the critical value of p at which the percolation probability rises rapidly. [6 marks]**

(a) Treat the wet top row as the water-source boundary. Repeatedly wet dry porous cells that have a wet four-neighbour, keeping existing wet cells wet and internal blocked cells dry. If water reaches the bottom, there is a top-to-bottom percolating cluster. If no new cells become wet before that, there is none.

(b) Fix the grid size and boundary rules. Choose several p values and generate many independent random grids at each one. Test every grid using part (a). Estimate the percolation probability as the number that percolate divided by the number tested.

Plot this fraction against p. Refine the region where it rises rapidly, using smaller parameter steps and more trials. A crossing probability near one half can define a finite-grid estimate. Repeat with larger grid sizes to check finite-size effects and report statistical uncertainty rather than treating one successful run as the threshold.

**Q5. In a sandpile model with a critical value K=3, what are the possible values of the cells' states when the model reaches equilibrium? Explain your answers. [4 marks]**

The possible values are 0, 1, 2 and 3. Cell heights are non-negative integers, and toppling occurs only when a height exceeds three. Any cell with four or more grains would still topple, losing four grains and sending one to each orthogonal neighbour, so the model would not yet be stable. A value of three is allowed. Equilibrium means that no cell needs to topple, not that all cells have the same value.

**Q6. Visually identifying a fractal pattern of a 2D Cellular Automaton can be deceiving. Explain the detailed quantitative process for determining whether a pattern is fractal. [6 marks]**

Define the target set, for example cells at one sandpile height, and form a Boolean mask. In the lab's method, use centred square windows with several increasing side lengths L and count the selected cells M(L) in each window.

If M(L) is approximately proportional to L^D, a log-log plot of M against L should be approximately straight over a useful range. Exclude zero counts, fit the slope, and interpret it as an estimated dimension D.

Avoid scales dominated by single cells or the array boundary. Check several scales, different centres and larger arrays where possible. Stable non-integer scaling supports a fractal interpretation. Visual similarity or a short straight segment alone does not establish fractality. Alternatively, conventional covering box counting estimates D from occupied-box counts against inverse box size.

**Q7. Explain the two main types of interaction in Agent-based Modelling. [4 marks]**

Agent-agent interaction occurs when one agent directly responds to another, such as a boid aligning with nearby boids or a driver braking behind another car.

Agent-environment interaction occurs when agents respond to and modify their surroundings. In Sugarscape, agents move towards sugar, harvest it, and leave less for later agents. The environment therefore also provides an indirect route through which agents affect one another.

**Q8. Identify and explain three different instances where randomness is involved in the Sugarscape model. [6 marks]**

First, initial positions and attributes are sampled randomly, including sugar endowment, metabolism and vision. This gives agents different starting opportunities and abilities.

Second, shuffle the agents' action order at each time step. Otherwise, the same agents could always get first access to contested resources.

Third, use random tie-breaking when several unoccupied cells offer the same maximum sugar at the same minimum distance. This prevents an artificial preference for one direction. These are three different roles for randomness: initialisation, scheduling and decision tie-breaking.

**Q9. How would you configure the Sugarscape model so that its simulation outcomes clearly exhibit emergent properties? Explain how it contributes to the emergence of complex behaviours. [5 marks]**

Use the two-peak sugar landscape and initially place agents in distinct cells near the lower-left corner. Retain local searching, harvesting, metabolism and resource regrowth, with a suitable spread of vision ranges.

Agents move towards accessible sugar. As earlier agents deplete cells, others must wait for regrowth or find resources elsewhere. The population can form travelling migration waves towards and between the peaks. In the classroom example, diagonal waves appear even though individual movements follow grid directions.

The waves are emergent: no rule tells the population to form or move as a wave. They arise from local choices and agent-environment feedback. Record spatial density over time and repeat trials to check that the pattern is robust.

**Q10. A genotype is a sequence of N binary digits. If N=4 and the simulation starts with one agent at every location of the fitness landscape, how many agents are present initially? Explain your answer. [6 marks]**

Each of the four positions can independently be zero or one. The number of possible genotypes is therefore 2^4=16, covering every string from 0000 to 1111. Each genotype is one location in the fitness landscape. With exactly one agent at each location, the initial population contains 16 agents.

These locations are genotypes, not physical places. The population equals 2^N here because the question explicitly specifies one agent per possible genotype; that is not true for every initialisation method.

**Q11. Describe three different methods for initialising the locations of agents on a fitness landscape and justify the initial level of population variability for each method. [9 marks]**

First, place one agent at every possible genotype. This gives 2^N agents and complete coverage of genotype space, with the largest possible number of distinct genotypes. It becomes expensive as N grows.

Second, sample a fixed number of agents at random locations in genotype space. This usually produces substantial variation, but repeated genotypes are possible and some locations may be missed. Actual variability depends on population size and sampling.

Third, place every agent at the same genotype. The population initially has zero genetic variability. Copying alone cannot create new types; mutation or another mechanism introducing new genetic combinations is needed for variation to appear.

**Q12. The supplied population-evolution code uses a constant death probability in choose_dead and uniform parent sampling in choose_replacements. Identify which parts to modify for differential survival and differential reproduction, describe the changes, and explain their effects. [8 marks]**

Modify the death test inside choose_dead and the parent selection inside choose_replacements. The original code ignores the fitness input in both places: it uses a fixed death probability of 0.1 and samples parents uniformly.

```python
def choose_dead(self, ps):
    # ps must contain survival probabilities in [0, 1].
    n = len(self.agents)
    is_dead = np.random.random(n) > np.asarray(ps)
    return np.nonzero(is_dead)[0]

def choose_replacements(self, n, weights):
    weights = np.asarray(weights, dtype=float)
    # Assume finite, non-negative weights.
    total = weights.sum()
    p = weights / total if total > 0 else None
    parents = np.random.choice(
        self.agents, size=n, replace=True, p=p
    )
    return [parent.copy() for parent in parents]
```

For survival probability f, death now occurs with probability 1-f. Fitter agents are less likely to die. If raw fitness is not in [0,1], map it to valid probabilities first.

For reproduction, normalising weights makes a parent's selection probability proportional to its fitness. Sampling with replacement allows the same parent to have several offspring; copying preserves its genotype. If every weight is zero, this example falls back to uniform selection.

This retains the original code's pre-replacement parent pool. If only surviving agents may reproduce, restrict and renormalise the parent pool accordingly; do not describe the shown code as survivor-only selection.

**Q13. Given opponent-history tuples [(None,None), (None,'D'), (None,'C'), ('C','D'), ('C','C'), ('D','D'), ('D','C')], encode the genotypes for (1) always defect, (2) always cooperate, and (3) tit for tat. Each tuple gives the opponent's previous two actions. [6 marks]**

Using exactly the order in the question:

1. Always defect: DDDDDDD.
2. Always cooperate: CCCCCCC.
3. Tit for tat: CDCDCDC.

TFT starts with C when no round has been played. After that, it copies the opponent's most recent move, which is the second entry of each tuple. Therefore, its seven actions are C,D,C,D,C,D,C. The genotype depends on the order of the history list; a string memorised from a differently ordered list may be wrong.

**Q14. Describe the process to evaluate the tendency of Niceness and Retaliating in the simulation of evolutionary dynamics of Prisoner's Dilemma tournaments. [6 marks]**

After each evolutionary time step, examine the population's strategy genotypes and record two measures.

For niceness, count all C entries across every strategy table and divide by the total number of entries. With M agents and seven entries each, niceness is the number of C entries divided by 7M. This is the course's genotypic measure, not just first-round cooperation.

For retaliation, compare the tendency to defect after the opponent's latest D with the tendency to defect after its latest C. Under the question's history order, the D-ending entries are 1,3,5 and the C-ending entries are 2,4,6. Exclude opening entry 0. Compute the fraction of D responses in each group and subtract the second fraction from the first, then average across agents.

TFT has contrast 1, while an always-defect strategy has contrast 0: defection alone is not evidence of retaliation. Plot the population measures over generations and repeat runs to distinguish persistent trends from random fluctuations.

**Q15. Design a Cellular Automaton to simulate forest-fire spread. Include (1) cell states, (2) initial configuration, (3) rules, (4) randomisation, and (5) quantification of outcomes. [15 marks]**

1. Cell states: use a two-dimensional grid with empty, tree, burning and ash states. Empty and ash cells cannot transmit fire. Specify a four-cell von Neumann neighbourhood and open boundaries.

2. Initial configuration: independently place trees with a chosen probability rho. Other cells are empty. Ignite one randomly selected existing tree or a stated small set of trees. Record the initial tree count. Assume the simulated fire is short enough that trees do not regrow.

3. Rules: a burning tree becomes ash after one step. A healthy tree with b burning neighbours ignites with probability 1-(1-q)^b, where q is the independent transmission probability from one burning neighbour. A tree with no burning neighbours stays a tree. Empty and ash cells remain unchanged. Compute every next state from the old grid and apply updates together. Stop when no cells are burning.

4. Randomisation: randomise tree placement, the chosen ignition location and transmission trials. State the distributions, record seeds and run many independent repetitions. This separates one lucky outcome from a general trend.

5. Quantification: measure the fraction of initial trees burned, fire duration, maximum number of simultaneously burning cells, and whether fire reaches the opposite boundary. Compare these measures across tree densities or transmission probabilities, reporting averages and variability. Wind, terrain and varying tree types are omitted assumptions that limit realism.
