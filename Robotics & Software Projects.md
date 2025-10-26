
* Even Monitoring Tools for ROS  2
	* Dan was describing DataDog and how they use it to get alert for problems and that engineer on the call tackles
	* I think something similar and small can be done for local distributed computational robot 
	* led me to this [ROSMonitoring](https://github.com/autonomy-and-verification-uol/ROSMonitoring)
		* [published paper](https://iris.unige.it/bitstream/11567/1035245/1/ROSMonitoring_ICRA2020.pdf)
	* [[Monitoring Tools]]
	* and generally reading about verification frameworks
	* [[Robot Logging]]

* Open source BD Choreographer 
	* https://dev.bostondynamics.com/docs/concepts/choreography/choreographer.html
	* https://github.com/Geonhee-LEE/mpc_ros
	* https://github.com/rst-tu-dortmund/mpc_local_planner
	* I feel like a huge question is what exactly do I want to "shape"?
		* like joint space trajectories
		* but also end effector trajectories
		* but also dynamics aspects of that as well
			* so twists?
			* and wrenches? 
			* and center of mass representation
		* the choreo should have feedback to allow error checking / proofreading the choreo
	* i also probs need some base research on what animation type of tools there are for creating choreo 

* MPC(lite, like a bare-bones)  Implementation in Mujoco 
	* so like the point is to dip my toessies into MPC 
		* Keeping is super simple
	* Use existing robot models that mujoco supports 
	* read about the theory and write into code documentation 
	* think before you write 
	* read before you write
	* Rules Of Engagement: 
		* Min. 1 our at a time. 
		* Intentionality
			* I am going to start working on X, this necessary for Y
			* or 
			* I cant do Y until I solve X 
* 