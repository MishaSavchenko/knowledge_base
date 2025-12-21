---
refs: https://underactuated.mit.edu/contact.html
tags:
  - robotics
  - dynamics
---
Hybrid dynamics with impact discontinuities at the collision event and constrained dynamics during contact.


Trajectory optimization
Lyapunov analysis 
LQR


## Description of Hybrid System

* Hybrid system = A system that is both continuous and discrete in time.
	* Autonomous hybrid systems: internal dynamics can cause discrete changes without any exogenous input
* Hybrid system can be described by modes, guards, and resets
	* modes: sets  of continuous dynamics
		* can have multiple guards
	* guards: continuous functions whose [[Zero-Level Set]] describes the conditions which trigger and event
		* associated to particular mode
		* at most one reset 
		* "witness functions"
	* resets: describe the update to the state that is triggered by the guard
		* "transitory functions"


## Hybrid Trajectory Optimization

Two different kinds of trajectory optimizations: 
1. The sequence of modes is already known
	* Stitching multiple individual mathematical programs into a single mathematical program, with the boundary conditions to make  sure that resets and guards are maintained  
2. The sequence of modes needs to be discovered
	* Direct Shooting
		* taking gradients through the guard/reset map
		* prone to local minima
		* taking the gradient of the cost by using methods like backpropagation through time 
			* using backprogration through time can be done in discrete and continuous times and combined for hybrid cases
		* Three parts to this 
			* continuous adjoint equation to solve the continuous models 
			* discrete adjoint equation to handle jump discontinuity 
			* Saltation Matrix: gradient of the variations relative to the contact time  



Modeling Approaches for Hybrid Systems 
* Minimal coordinates modeling 
* Floating base coordinates
* maximal coordinates 