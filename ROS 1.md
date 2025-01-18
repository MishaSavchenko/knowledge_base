---
tags:
  - robotics
  - ros
---
## Patterns 
### Communication
Refs: [ROS.org](http://wiki.ros.org/ROS/Patterns/Communication)
- Topics
	- Continuous data streams 
	- Data might be published and subscribed at any time independent of any senders/receivers
	- Many to many connections
	- Callbacks receive data once it is available 
	- Publisher sends out data
- Services  
	- Remote procedure calls that terminate quickly 
	- Querying the state of a node 
	- Doing calculation such as IK
	- Not for longer running processes 
	- Simple blocking call
	- Semantically for processing requests
- Actions
	- Discrete behavior that move a robot or runs for longer time
	- Provides feedback during execution
	- Most important property is that actions should be preempted and preemption should always be implemented cleanly by action servers 
	- Keep state for the lifetime of a goal 
	- Slow perception routines which take several seconds to terminate or initating a lower level control mode are good use cases 
	- Complex non-blocking background processing 
	- Semantically for real worlf actions

- Topic Remapping 
	- Avoids topic name collisions
		- Gives a node ROS API
- Publishing Spatial / Geometric Data
	- Coordinate frames should be published