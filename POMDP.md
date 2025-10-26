## Brief Introduction to MDPs
* How to balance actions that have immediate return vs long term benifit?
* Markov process allows for automation of the decisions for modeled problems in uncertain environments
* If the problem can be modeled as MDP we can solve it the decisions for it.
* Initial assumptions
	* We have the following components: 
		* Set of [[#States]]
		* Set of actions
		* Effects of Actions
		* Immediate value of actions 
	* Additionally: 
		* actions and states are discrete
		* time is uniform and discrete
### States
* the state of the world
### Actions
* set of choices you could make
* have an immediate effect on the world
### Transitions
* action effect on the state
* some can be probabilistic (in MDPs)
	* the framework supports representation of probabilistic effects of an action

### Immediate Rewards
*  Automation necessitates that an action taken at a state has an associated cost with it. Whenever the action is taken the cost is incurred.
> [!question] Most processes that I'm going to deal within robotics have a fairly complicated cost for them. 
> 1. Is it possible to not have immediate rewards associated with the state transition.
> 2. How differently are the rewards structured with partial observability.

## Markovian Process
* A huge assumption is that the next state only depends on the current state and action. 


## Value Iteration Algorithm
>* Mapping from states to actions, which represents the best actions to take for each state
	* this may vary based on a horizon length
	* if the value of each state is present then this is easy
>* Computes this value function by finding a sequence of value functions, each one derived from a previous one. 

Calculates the cost of function by expanding the horizon and checking the end value after the transitions, this maybe a bit more complex when probabilities are starting to get involved 


## POMDP

Even though the POMDP are still MDPs and the Markovian dynamics still apply because we need to constantly must monitor our history to determine the probability of being in a specific state, the process overall is non-Markovian. 

> [!note] I still dont fully understand why having the process be Markovian is so important, I assume it is because it is a requirement to use MDP tools and algorithms to solve the problem but is that all? 

> POMDP is problem of finding a mapping from probability distribution over states to actions. 	
- [ ] Rephrase this into layman's terms. Specifically focus on what probability distribution really mean.



---
[Brief Introduction to MDP's](https://www.pomdp.org/tutorial/mdp.html)