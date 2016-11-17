## FSP
### The Bottomline
The general idea of FSP is to find Nash Equilibrium. That is, once the learning process convergences, the agent stands by the strategy aquired during the learning process and does not change it according to their opponent. Though, the agent adapts its actions based on the opponent, of course.  

### Fictitious Play
So how to reach that Nash Equilibrium? It's as simple as repeated making each play learn a strategy counter their opponents. At each iteration, each player treats their opponents as a unified, fixed game environment, and developes a best response toward that environment. Note the adaption of all the players are conducted simultanously. After infinite many rounds of such kind of adaptions, all players are expected to own the same strategy which belongs to the Nash Equilibrium.

### Convergence
One key observation is that, if fictitious play ever converges, it converges to the Nash Equilibrium (Fudenberg and Levine 1998, Proposition 2.2). Theoretically, if the game is zero-sum and there's only two players in the game, where each player at any situation has finite many actions to select from, FSP is guaranteed to converge.

### NFSP
That's it (Heinrich 2016). Just use reinforcement learning to learn the counter strategy. The algorithm is likely slow as it repeatedly conducts reinforcement learning ...

### CFR
Counterfactual Regret is the more accurate, but computational inefficient way to learn the counter strategy. It basically enumerate all information set and decide the probability distribution over the action set of all that information set (recall that information set of all possible state with the observed information, no matter what the hidden information is).
