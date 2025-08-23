* Classical task planning relies on limiting the search space to avoid the intractability of a huge space, whereas motion planning relies on sampling based planners to deal witdh continuous high dimension. 
* Hierarchical Task Networks  (HTNs)
	* helps to avoid expanding unnecessary branches of the hierarchy 
	* prunes infeasible plans before producing low-level plans
	* (mythical) *downward refinement property*
		* > given that a concrete solution exists every abstract solution can be refined to a concrete-level solution without backtracking across abstract levels 
		* theoretical but not very practically relevant 
* Commitment in sampling parameters during search
	* Early-commitment (or binding) -> sample action parameters from continuous space before search
	* Least-commitment (or optimistic) -> symbolic plan as a skeleton, then sampling feels in the parameters




---
## References
[Integrated Task and Motion Planning (TAMP) in robotics](https://robohub.org/integrated-task-and-motion-planning-tamp-in-robotics)
	[The Downward Refinement Property](https://www.ijcai.org/Proceedings/91-1/Papers/045.pdf)
[Dynamics and Motion of a Six Degree of Freedom Robot Manipulator](https://drive.google.com/file/d/1JC7FDInGSkEgZwHdW6Kn-7C8Y4w0dJTC/view?usp=sharing)  

