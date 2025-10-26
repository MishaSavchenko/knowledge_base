## Intro
* Reasoning about the state of the world using internal model and coming up with a sequence of action, or a plan, to achieve a goal
* It would be "overkill" to use task planning for simple, repetitive tasks
> [!question] Simple and repetitive tasks can be complex in different ways... Un-calibrated systems may need multiple repetitive actions to do "local calibration". Like securing the grasp on an object.
## PDDL
*  Planning Domain Definition Language
* Context matters, similarly defined actions can achieve different goals in different environments
* Task-Agnostic Domain 
* Task-Specific Domain
> [!note] Im still not entirely sure what the difference is between task agnostic and specific domains
* *action language* -> most of the is composed of actions/*operators* 
	* each action is composed out of 
		* Parameter -> 
			 * ```Allow the same type of action to be executed for different combinations of objects that may exist in our world.```
		* Precondition -> the pre-req required to allow taking an action from the state
		* Effects -> change of the state after the action is taken
> [!question] Maybe this is the issue... Do effects have to be known and defined? If so it might be difficult to describe actions that require continuous improvements 

* represents the world using states and actions 
* The necessary details that go into describing an action, help to limit the size of the space that the algorithm for task planning has search in.
## State-Space Search
* Forward Search -> start with initial state and expand the graph until goal is reached. 
* Backward Search -> start with goal state(s) and work backwards until the initial state is reached.
* The traversal of the graph can be selected for breadth or depth, additionally if actions have cost associated with them addition searching methodologies can be involved
* Pruning search graphs based to previously visited states will have prevent infinite cycles and expanding unnecessary actions
* Defining heuristics for complex plans can be tricky and depending on the domain there are literature that can give you a hint in the right direction.
	* Heuristic planner examples
		* Heuristic Search Planning (HSP)
		* Fast Forward (FF)
		* **Fast Downward** 
			* seems to be the standard.
## Alternative Search Methods
* Plan-space planning (PSP)
* Planning Graphs
* Partial Order Planning









---
## References
[Task Planning in Robotics](https://roboticseabass.com/2022/07/19/task-planning-in-robotics/)