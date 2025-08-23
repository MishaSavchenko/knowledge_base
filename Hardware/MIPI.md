https://www.e-consystems.com/blog/camera/technology/what-is-a-mipi-camera-how-does-mipi-camera-work/

- Mobile Industry Processor Interface 
	* convenient ways of interfaces cameras with host processors 
- Evolution
	1. CSI-1
		1. original standard interface architecture
	2. CSI-2
		1. 2005 final version had protocol divided into layers
			1. Physical Layer
			2. Lane Merger Layer
			3. Low-Level Protocol Layer
			4. Pixel to Byte Conversion Layer
			5. Application Layer
		2. 2017 Version
			1. support RAW-16 and RAW-20 color depths 
			2. increase virtual channels from 4 to 32
			3. reduce Latency Reduction and Transport Efficiency (LRTE)
		3. 2019 3rd version
			1. support for RAW-24 color depth
		4. Most common
	3. CSI-3
		1. high speed, bidirectional protocal for image and video transmission
* MIPI interface connects image sensor with embedded board to control and process image data
* Better resolution and frame rate than the older parallel interface camera modules (Digital Video Port) 
* MIPI vs USB
	* USB -> at most 5 gigabits per sec, more likely 3.6 gigabits per sec
	* MIPI -> at most 6 gigabits per sec, more likely 5 gigabits per sec 
		* makes the proess more efficient and faster than USB
* 