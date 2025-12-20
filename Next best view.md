---
tags:
  - perception
  - robotics
---

"sequential planning task where in each step a new measurement of the environment is obtained and location of the next measurement is determined based on all previous measurements"
* potentially useful for manipulation if combined with object localization/classification

[optimal camera placement][https://www2.eecs.berkeley.edu/Pubs/TechRpts/2012/EECS-2012-69.pdf]

known scene + visibility objective throw it together into optimization solver and figure out what is the optimal camera placement, duh

local visibility objectives 
	camera configuration C observes feature x to produce metric of how well the feature is viewed R 
		camera configuration
			pose, focal length, etc...
			multiple cameras as well
			illuminations as well
		feature 
			edge, point, facet, etc...


a simpler formulation of the problem uses [[Foreshortened Length]] of the feature on the image plane! 
	
> what do high fidelity camera hardware simulations look like? whats under the hood? what is considered?




