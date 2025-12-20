---
tags:
  - robotics
  - projects
---
I guess that are a couple of components to this project 
Lets start with Valkyrie as an example of starting up an arbitrary process that has really complex start up procedure 


* Part of the reason why I think Valkyrie is a great example is that despite, what so many people are going to claim, its a pretty cool piece of hardware! 
* It a development platform that was seemingly developed by folks who know some about robotics, but fuck all about architecture software development, and production level code
	* and while this might be kindda fucking mean, its the slop that they made that I have to eat, i guess 
* Valkyrie Platform Characteristics : 
	* Distributed system over 3 (or more) machines
		* console, for the user to interface with 
		* on-board A (Link) (Controls) 
		* on-board B (Zelda) (Perception) 
		* logging, for storing massive amounts of data
		* VR console, for VR application
	* Console computer dictates the start up procedure
		* defining the robot 
		* starting up controllers
		* defining the environment
		* starting up the perception subsystem(s)
		* starting up applications for the different modules that the platform supports
			* stance generation
			* motion planning 
			* vr interface 
			* directional control
			* etc... 