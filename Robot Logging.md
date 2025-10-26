I guess that are a couple of components to this project 
Lets start with Valkyrie as an example of starting up an arbitrary mechanism that has really complex start up procedure 

* Part of the reason why I think valkyrie is a great example is that despite, what so many people are going to claim, its a pretty cool piece of hardware! 
* It a development platform that was seemingly developed by folks who know some about robotics, but fuck all about architecture software development, and production level code
	* and while this might be kindda fucking mean, its the slop that they made that I have to eat, i guess 
* Requirements for Valkyrie: 
	* Distributed system
		* console 
		* on-board A (Link) (Controls) 
		* on-board B (Zelda) (Perception) 
		* logging 
	* Console computer dictate the start up procedure
		* defining the robot 
		* starting up controllers
		* defining the environment
		* starting up the perception subsystem
		* starting up applications for the different modules that the platform supports
			* stance generation
			* motion planning 
			* vr interface 
			* directional control
			* etc... 
