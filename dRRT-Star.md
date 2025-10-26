

* Extension of dRRT 
	* dRRT is a multi-robot motion planner
* informed, asymptotically-optimal
* mainly focuses on the multi robot motion planning problem
	* but potentially can be extended to "bi-manual manipuation"
* When robots are in a very close proximity to each other
	* collision is more likely to happen
	* thinking about robots in a de-coupled manner is counter productive
	* using the robots' composite space might be more prudent.
* dRRT
	* managed to achieve completeness (and efficiency) in finding paths in high dimensional composite space 
	* leveraged an "implicit representation of the composite space"
		* "implicit representation" is a graph which corresponds to the tensor product of roadmaps explicityl constructed for each robot.
	* does not provide any path quality guarantees
* 


Questions / Further Research  
* what is 'tensor product of roadmaps in the composite space'?