Things that I would like to learn:
* Being able to simulate arbitrary hardware and it's characteristics can be very useful for robot design.
	* URDF can give you: joint, links 
		* other software can use additional information in the urdfs to characterize actuators, cameras, and transmissions.
* Seems like simulating hardware itself, i.e. how the joint behaves when current is applied to it? can be incredibly complicated since it depends on a variety of factors
	* specific hardware component characteristics
	* firmware
	* other interrelated hardware components
> [!question] are there any other things im missing from this list? and how is robotics hardware usually simulated at this level?

* simulating the joints in the way they are defined in the urdf, and using the limits defined in the urdf would not allow for verification and validation of the transmissions, and the hardware interfaces. However it does lend itself to an easier simulation of kinematics, and to a limited extent dynamics.
> [!question] What is the extent the dynamics can be represented MUJOCO?
* 

Hardware <-> hardware interface <-> controllers 