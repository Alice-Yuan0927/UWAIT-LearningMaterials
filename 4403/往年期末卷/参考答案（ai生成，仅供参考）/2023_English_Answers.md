# CITS4403 Final Examination 2023: English Answers

Suggested answers for revision, not an official marking guide. Questions are in bold; answers are in plain text.

**Q1. Define and explain the concept of 2-Dimensional Cellular Automata (2-D CA) in the context of complexity science. Include an example of a 2-D CA that produces a complex system. [10 marks]**

A two-dimensional cellular automaton consists of a grid of cells. Each cell has one state from a specified set, and time advances in discrete steps. A local transition rule determines its next state from its current state and neighbouring states. The same rule applies across the grid, usually with synchronous updates. The model must specify its neighbourhood, initial configuration and boundary conditions.

The Game of Life is an example. Each cell is alive or dead and has eight Moore neighbours. A live cell survives with two or three live neighbours and otherwise dies. A dead cell becomes live with exactly three live neighbours. Calculate all next states from the old grid before replacing it.

These simple rules can produce oscillators, moving gliders and glider guns. The rules do not contain instructions for those objects; they arise from interactions among cells. This illustrates emergence and shows that complex collective behaviour does not require complicated individual rules.

**Q2. Explain how reaction-diffusion could be responsible for animal patterns. [5 marks]**

Suppose two interacting chemicals spread through developing skin. One acts as an activator that encourages local pigment production and its own production; the other inhibits the process and spreads farther or faster.

Under suitable reaction and diffusion rates, small initial differences grow into a stable spatial pattern. Local activation and longer-range inhibition can produce spots or stripes without a separate instruction for every marking. Different parameters and boundaries produce different patterns. This is a possible mechanism for some animal markings, not a claim that every marking has the same cause.

**Q3. How does one verify the existence of a "percolating cluster" in percolation simulation? Explain the term of phase change and how it is determined in the context of percolation simulation. [10 marks]**

A percolating cluster is a connected route through porous cells that spans the grid, for example from top to bottom. Wet the top source boundary and repeatedly spread water to dry porous cells with a wet von Neumann neighbour. If water reaches the bottom, a spanning cluster exists. If wetting stops before that, it does not.

A phase change is a qualitative change in the system's large-scale behaviour as a control parameter varies. Here, increasing the probability p that a cell is porous changes the system from usually non-spanning to usually spanning.

To locate the transition, choose a range of p values. For each value, generate many independent grids and record the fraction that percolate. Plot that fraction against p and refine the rapidly rising region. A crossing probability near one half can define a finite-grid estimate. Repeat with larger grids to assess finite-size effects; the sharp critical transition is an idealisation of the large-system limit.

**Q4. A wide variety of systems display a common set of behaviours and characteristics when they are at or near a critical point. Illustrate three common behaviours exhibited by critical systems, providing concrete examples for each behaviour. [9 marks]**

First, fractal or approximately self-similar spatial structure can occur. For example, clusters near a percolation threshold contain irregular branches and gaps on several scales, and their mass can scale with a non-integer dimension.

Second, event sizes may have heavy-tailed distributions. In a critical sandpile, small avalanches are common but occasional very large avalanches occur; there is no single typical avalanche size that adequately describes the range.

Third, activity can show pink-noise-like temporal structure. In the sandpile's toppling time series, power is greater at low frequencies and decreases approximately as a power of frequency over a scaling range.

These are empirical signatures to measure, not automatic consequences of any complicated picture. Their observation supports a critical-system interpretation but should be checked quantitatively.

**Q5. Why do so many natural systems have properties of critical systems? Provide a possible explanation for this phenomenon. [5 marks]**

One possible explanation is self-organized criticality. Some systems are slowly driven and lose accumulated material or stress through threshold-triggered events. Their own feedback can bring them towards a critical regime without an outside observer tuning a parameter precisely.

The sandpile illustrates this: adding grains raises heights, while toppling redistributes grains and boundary losses remove them. The system can then produce events over many scales. This offers a reason critical-like behaviour might be common. It is a hypothesis to test in each real system, not proof that every heavy-tailed process is self-organized critical.

**Q6. In the sand pile model, during each time step, each cell is checked to see whether it exceeds a critical value, K. If the critical value K=3, when the sand pile model achieves equilibrium, what are the possible values of all the cells? Explain your answer. [5 marks]**

Every cell must have a value of 0, 1, 2 or 3. Heights are non-negative integers, and toppling occurs only when a value is greater than K=3. A cell with four or more grains would still topple, so the configuration would not yet be at equilibrium. A value of three is stable. Equilibrium means that no cell needs to topple; it does not mean that all cells have the same height.

**Q7. Explain the purpose of the provided count_cells(a) function, especially in what circumstances the following code is used. The parameter a is a Boolean array. [10 marks]**

The supplied function is:

```python
def count_cells(a):
    n, m = a.shape
    end = min(n, m)
    res = []
    for i in range(1, end, 2):
        top = (n - i) // 2
        left = (m - i) // 2
        box = a[top:top+i, left:left+i]
        total = np.sum(box)
        res.append((i, i**2, total))
    return np.transpose(res)
```

It measures how the number of selected cells grows with observation scale. True means that a cell belongs to the set of interest, such as sandpile cells with one chosen height. False cells do not contribute.

The function reads the array dimensions and uses the smaller dimension as its size limit. For each odd side length i below that limit, it extracts an approximately centred i-by-i square. Because a is Boolean, summing the square counts its True cells. It stores the side length i, square area i^2, and selected-cell count. Transposing returns three sequences containing those quantities across scales.

The function supports quantitative fractal analysis. Remove zero counts, plot log(cell count) against log(side length), and estimate the slope over a meaningful scaling range. A filled area scales as L^2; a line-like set scales roughly as L. Intermediate scaling can support a fractal interpretation. The function collects counts; it does not itself fit the slope or prove fractality. It counts cells inside growing boxes, rather than counting occupied boxes in a tiled covering.

**Q8. Outline three elements of agent-based models. [6 marks]**

The three elements are agents, an environment, and rules for behaviour and interaction.

Agents are the individual entities being simulated. They have states or attributes, such as position, wealth, vision or velocity, and these may differ between individuals.

The environment provides the space, resources or other conditions in which agents operate, such as the sugar grid in Sugarscape.

Rules specify how agents make decisions, change state and interact with other agents or the environment. Repeated application of those rules produces the system's overall behaviour.

**Q9. What are the two main types of interaction in agent-based modelling? [4 marks]**

Agent-agent interaction occurs when one agent directly responds to another, such as a boid aligning with nearby boids or a driver braking behind another car.

Agent-environment interaction occurs when agents respond to and modify their surroundings. In Sugarscape, agents move towards sugar, harvest it, and leave less for later agents. The environment therefore also provides an indirect route through which agents affect one another.

**Q10. Explain why the segregation we see in Schelling's model is an emergent property. [5 marks]**

No agent is instructed to segregate the whole grid. Each resident only checks its local neighbourhood and moves if its own modest similarity requirement is not met. A move changes the neighbourhoods of other residents, potentially causing further moves.

These local decisions can create large same-type regions, even when residents would accept mixed neighbourhoods. Segregation is therefore a population-level pattern produced by interactions and feedback, rather than the stated aim or property of a single resident. The result demonstrates a possible mechanism, not the absence of discrimination in real societies.

**Q11. In 1996, Joshua Epstein and Robert Axtell proposed Sugarscape, an agent-based model of an "artificial society" intended to support experiments related to economics and other social sciences. Describe the Sugarscape model in detail, including the agent's attributes, rules, and the original configuration of the Sugarscape grid. [15 marks]**

Sugarscape places agents on a two-dimensional resource grid. The course configuration has two peaks with sugar capacity 4, surrounded by concentric regions with capacities 3, 2 and 1. Start cells at their stated capacities and place 400 agents at distinct random locations. After agents act, each cell typically regrows one unit of sugar, up to its capacity.

An agent has a position, a sugar store or wealth, a vision range and a metabolism rate. In versions with ageing, it also has an age and a maximum lifespan. Initial positions and attributes are sampled from stated distributions, and agents occupy distinct cells.

During its turn, an agent examines available cells along the four grid directions within its vision, including its present location. It chooses the cell with the most sugar, preferring the nearer cell if sugar amounts are tied. If sugar and distance are both tied, choose randomly. It cannot move into another agent's occupied cell.

The agent moves, harvests the sugar into its store, and leaves that site's current sugar depleted. It then pays its metabolic cost. In the lab version, a negative remaining store causes starvation. An ageing version also removes agents that reach their lifespan. State whether dead agents are replaced, since this changes population dynamics.

Shuffle the agents' action order, apply their turns, and regrow the environment according to the stated update schedule. Competition, unequal abilities and local resource depletion can generate unequal wealth and spatial migration patterns without a central allocation plan.

**Q12. Outline five different attributes that would influence the results of the Sugarscape model. [5 marks]**

1. Vision range: how far an agent can search for sugar, affecting its opportunities.
2. Metabolism: how much sugar it consumes per step, affecting survival and savings.
3. Initial sugar endowment: the buffer available before the agent must find more resources.
4. Maximum lifespan, in an ageing version: how long an agent can accumulate resources before removal or replacement.
5. Initial position: whether it starts near a rich sugar peak or in a poor region.

These attributes affect access to resources, survival and the resulting wealth distribution. Their distributions across agents matter as well as their average values.

**Q13. A very simple agent-based model of traffic evenly spread out along a road could easily seriously overestimate the flow. Explain how to make a slightly more complicated, and slightly more realistic model of individual car behaviour that can suggest much more realistic and much lower traffic flows. [5 marks]**

A perfectly regular model can keep cars evenly spaced and moving smoothly, producing an unrealistically high flow. Add small random variations to individual driving, such as occasional slowing, while limiting each car's speed according to the gap ahead.

One driver's slowdown makes the following driver brake; the disturbance can grow into a backward-moving stop-and-go wave. Cars then spend time moving slowly or stopping, so average speed and flow fall even without an accident or obstruction. Run past the initial transient and compare distance travelled per unit time at the same road density.

**Q14. Describe three minimum features that are sufficient to produce evolution. [6 marks]**

Three features are needed:

1. Replication with inheritance: agents produce offspring that retain their characteristics.
2. Variation: individuals differ, and mutation or another mechanism can introduce new inherited differences.
3. Differential survival or reproduction: those differences affect the chance of surviving or leaving offspring.

Selection can then change the population's inherited characteristics over generations. Copying alone produces no new variation, and variation without fitness-related selection does not by itself produce adaptation to the environment.

**Q15. In the simulation of evolution, choose_dead(self, fits) uses is_dead = np.random.random(n) < 0.1, giving every agent the same probability of dying. Specify which part can be changed to achieve differential survival and explain how it works. [5 marks]**

Replace the constant death test with a test based on the agent's fitness. Assuming fits contains valid survival probabilities between zero and one:

```python
def choose_dead(self, fits):
    n = len(self.agents)
    is_dead = np.random.random(n) > np.asarray(fits)
    return np.nonzero(is_dead)[0]
```

For fitness f, the probability of death is 1-f. A fitter agent is therefore less likely to die. The original line ignores fits and gives every agent death probability 0.1, so it cannot select through differential survival. Keep the comparison direction correct: using random<fits to mark deaths would make higher fitness increase mortality. If raw fitness is outside [0,1], first map it to a valid survival probability.

**Q16. In the late 1970s, Robert Axelrod organised a tournament to compare strategies for playing Prisoner's Dilemma. A simple strategy that did surprisingly well was "tit for tat", or TFT. Describe this strategy and discuss how its characteristics offer a possible answer to the "problem of altruism". [15 marks]**

Tit for tat cooperates in the first round of a match. After that, it copies the opponent's action from the previous round. If the opponent cooperates, TFT cooperates next; if the opponent defects, TFT defects next. It uses past behaviour, not advance knowledge of the opponent's current move.

TFT is nice because it does not defect first. It is retaliating because exploitation produces a response in the next round. It is forgiving because it returns to cooperation when the opponent does. It is non-envious: it can achieve a good overall score through mutual cooperation without needing to beat every opponent in each match.

The problem of altruism asks why costly helping persists when selfish individuals appear able to exploit helpers and reproduce more successfully. Repeated interactions change the incentives. Two TFT players can gain the mutual-cooperation payoff repeatedly. An always-defect player can exploit TFT initially, but then receives retaliation rather than unlimited benefits.

Consequently, cooperative behaviour can improve long-term fitness under suitable conditions. Natural selection may then favour inherited tendencies towards cooperation, retaliation and forgiveness. This offers a mechanism by which individually beneficial selection can support apparently altruistic behaviour.

The result depends on repeated encounters, payoffs and the mix of opponents. TFT is not universally optimal, and errors can start cycles of retaliation. The tournament provides a possible explanation for cooperation, not a complete account of human morality.
