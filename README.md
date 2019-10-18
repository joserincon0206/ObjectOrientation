# ObjectOrientation
This is a video of an algorithm that effectively detects the orientation of an object using its principal components and center of mass. Please open the gif file to see it working. 

The main assumptions of the algorithm: 

1. Objects will be transported on a coveyor belt, i.e., there is a plane-like structure that supports them. 
2. I have access to a time-of-flight camera to obtain the 3D shape of the scene. 

The main ideas of the algorithm: 

1. Using Ransac find the best fit for a plane. This will be assumed to be the surface that is holding the objects. 
2. Assign threshold for objects that are not on the plane. This will effectively give me clusters of the objects. 
3. For each object is the cluster, compute their centroid using PCA and its principal components.
4. Based on the direction of the principal components, obtain a line profile. Also, obtain a line profile in the intersection of the 
object with the plane. 
5. The line profiles are very noisy. For that reason, some type of smoothing is recommended. The best solution I found was to see each line profile as a 2D function, compute its Fourier Coeffients and only use the first 4 coeffients to reconstruct the signal. This was a very powerful and useful thing to do. 
6. With the 3 line profiles, compute the line curvature. 
7. Assume that the tip of the object will be effectively the highest curvature along the three profiles. 

