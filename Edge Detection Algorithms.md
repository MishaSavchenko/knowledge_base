Refs: [wiki](https://en.wikipedia.org/wiki/Edge_detection)

- Points at which image brightness changes sharply, has discontinuities     

- Likely to correspond to
    

-  discontinuities in depth
    
- Discontinuities in surface orientation
    
- Changes in material properties
    
- Variations in scene illumination  
    

- Step detection in one dimensional signals
    
- APplying edge detection to an image
    

- Yields set of connected edges indicating bondaries of the object allowing for smaller size of data that need to be analyzed
    

- Edge Properties 
    

- Extracted edges can be classified as 
    

- Viewpoint dependent
    

- Reflects the geometry of the scene (occluding objects)
    

- Viewpoint independent
    

- Inherent properties of the three dimensional objects such as surface markings and surface shape
    

- Simple Edge Model
    

- Edges obtained from natural images are affected by the following 
    

- Focal blur 
    
- Penumbral blur
    
- Shading at a smooth object
    

- Gaussian Smoothed Step Edge 
    

- Simplest extension of the ideal step edge model
    

- Approaches
    

- Search Based 
    

- Detection of edges based on edge strength 
    

- First Order derivative expression
    

- Gradiaent magnitude 
    

- Search for local directional maxima 
    

- Zero-Crossing Based
    

- Second order derivative expression 
    

- Zero-crossing of the laplacian 
    
- Zero-crossing of non-linear differential expression 
    

- Canny Edge Detector
    

-   
    

- Thresholding and Linking 
    
- EdgeThinning