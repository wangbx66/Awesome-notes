## FSP
### The Bottomline
The general idea of FSP is to find Nash Equilibrium (recall Nash Existence Theorem: if finite many players and possible actions, Nash Equilibrium exists). That is, once the learning process convergences, the agent stands by the strategy aquired during the learning process and does not change it according to their opponent. It doesn't try to learn about or exploit the opponent's flaws, also with an exploitibility of zero itself. Though, the agent adapts its actions based on the opponent, of course.  

### Fictitious Play
So how to reach that Nash Equilibrium? It's as simple as repeated making each play learn a strategy counter their opponents (starts with anything e.g. uniform). At each iteration, each player treats their opponents as a unified, fixed game environment, and developes a best response toward that environment. Note the adaption of all the players are conducted simultanously. After infinite many (billions of in practice) rounds of such kind of adaptions, all players are expected to own the same strategy which belongs to the Nash Equilibrium.

### Convergence
One key observation is that, if fictitious play ever converges, it converges to the Nash Equilibrium (Fudenberg and Levine 1998, Proposition 2.2). Theoretically, if the game is zero-sum and there's only two players in the game, where each player at any situation has finite many actions to select from, FSP is guaranteed to converge. In the theory instead of the strategy of the player, it is the average over time strategy which is guaranteed to converge, leaving the possiblility that the strategy oscillates. In practice, we should monitor if the exploitibility continue decreases.

### NFSP
That's it (Heinrich 2016). Just use reinforcement learning to learn the counter strategy. The algorithm is likely slow as it repeatedly conducts reinforcement learning ...

### CFR
Counterfactual Regret (Bowling 2015) is the more accurate, but computational inefficient way to learn the counter strategy. It basically enumerate all information set and decide the probability distribution over the action set of all that information set (recall that information set aka decision point of all possible state with the observed information, no matter what the hidden information is). The stated paper achieves an exploitibility of 1bb/10000 per hand.  

It's clearly stated that during the training process the agent DOES LOOK AT THEIR OPPONENTS STRATEGY IN AN EXPLICIT WAY. This is not cheating, since what we're trying to do is just learn the counter and achieve the Nash Equilibrium. When we do have the Nash, we won't bother looking at the opponent's strategy at all.  

The way it improves over time is by summing the total amount of regret it has for each action at each decision point, where regret means: how much better would I have done over all the games so far if I had just always played this one action at this decision, instead of choosing whatever mixture over actions that my strategy said I should use? Positive regret means that we would have done better if we had taken that action more often. Negative regret means that we would have done better by not taking that action at all. After each game that the program plays against itself, it computes and adds in the new regret values for all of its decisions it just made. It then recomputes its strategy so that it takes actions with probabilities proportional to their positive regret. If an action would have been good in the past, then it will choose it more often in the future.
