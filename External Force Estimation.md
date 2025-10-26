
#### Sliding Mode Momentum Observers for Estimation of External Torques and Joint Acceleration
DOI: 10.1109/ICRA.2019.8793529



"well established" momentum observer
	- how does it actually work? 
	-  how can we implement it?
> "first-ordered filtered versions of external torques..."
> "... therefore achieves asymptotic convergence only for constant external torques."
- *Im still a little bit confused about what "first-ordered" actually implies*
	- so the implication is that it is limited to a identifying forces that are applied in the same way/consistently over a period of time (?)
	- meaning that forces with more complex profiles might not be captured within this solution.
> finite convergence of the estimated torques to the real ones, as well as a finite-time estimation of the joint acceleration.
* so essentially given enough time/measurement the estimated will be equal to the real one, and the joint acceleration will also be determined
	* *but does it capture the linear aspect of wrenches? *
		* *extending the observers from into the task space allows for estimation of external wrench *
> finite-time behavior of the observers is obtained using sliding mode techniques 

**elastic joint will need to be extended separately**  

- *an additional assumption might also have to be made that the wrench is applied to the end effector only*

> ... one mus set an empirically obtained threshold to discriminate the occurence of real collision and decrese the probability of false positves. 

- *seems like there is always going to be noise and the momentum observer actually factors that in, kindda*
- *tunning is still required, but I wonder if that can be autonmated*
s





*so there is a big question about what to do when the dynamics of the robot are not exactly known or at the very least how to we discover the dynamics without disassembling the mechanism*
		*its a tiny bit fucked cause we are assuming that inertial values of a each of the links are known where they are just fucking guestimated*
			*figuring out how to actually get them from a assembled robot would be really dope*
				* cause if we have the current, efforts, velocities, positions -> shouldnt we able to get a semi accurate Mass matrix/inertial  *


### Further Reading
 - S. Haddadin, A. De Luca, and A. Albu-Schäffer, “Robot collisions:
A survey on detection, isolation, and identification,” IEEE Trans. on
Robotics, vol. 33, no. 6, pp. 1292–1312, 2017.
	- overview of collision identification 
- A. de Luca and R. Mattone, “Actuator failure detection and isolation
using generalized momenta,” in IEEE Int. Conf. on Robotics and
Automation (ICRA), Taipei, Taiwan, Sept. 2003, pp. 634–639.
	the intial implementation of the momentum observer  
- A. Levant, “Sliding order and sliding accuracy in sliding mode
control,” International Journal of Control, vol. 58, no. 6, pp. 1247–
1263, 1993.
- J. A. Moreno and M. Osorio, “A Lyapunov approach to second-order
sliding mode controllers and observers,” in IEEE Conf. on Decision
and Control, Cancun, Mexico, Dec. 2008, pp. 2856–2861






