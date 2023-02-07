## Project Description

The goal of this project is to implement '[SparseLeap-an effective empty space skipping technique](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8017589)' during volume rendering phase of the NeRF(Neural Radiance Fields). In this project, we have used Lego data set is for training the NeRF. The NeRF is first trained using the Stratified and Heirarchical volume sampling. once the training is completed, Sparseleap is used to render the novel view from the trained NeRF. Stratified and Heirarchical volume sampling sampled a point uniformaly along the ray irrespective of the sampled point is in empty space or not. Sparseleap strategically skip the empty space and sampled a point only where objects lies. Hence, Sparseleap impove the computational efficiency of the volume rendering phase in NeRF.   

## What is NeRF (Neural Radiance Fields)?

NeRF or better known as Neural Radiance Fields is a state-of-the-art method that generates novel views of complex scenes by optimizing an underlying 
continuous volumetric scene function using a sparse set of input views. The input can be provided as a blender model or a static set of images.
The input is provided as a continuous 5D function that outputs the radiance emitted in each direction (θ; Φ) at each point (x; y; z) in space, 
and a density at each point which acts like a differential opacity controlling how much radiance is accumulated by a ray passing through (x; y; z).

![img2](https://user-images.githubusercontent.com/90370308/217326977-27fb759e-cd09-4478-97e9-fdb4ac833ec2.png)
*The figure above represents the steps that optimizes a continuous 5D (x; y; z; θ; Φ) neural radiance field representation 
(volume density and view-dependent color at any continuous location) of a scene from a set of input images. Here in this example of drum set, 
approximately 100 images were given as input with various x, y, z, θ, and Φ values for each of them.*

A continuous scene can be described as a 5D vector-valued function whose input is a 3D location x = (x; y; z) and 2D viewing direction (θ; Φ), and whose 
output is an emitted color c = (r; g; b) and volume density (α). To generate a Neural Radiance Field from a particular viewpoint following steps were 
done:
  1. March camera rays through the scene to generate a sampled set of 3D points
  2. Use those points and their corresponding 2D viewing directions as input to the neural network to produce an output set of colors and densities
  3. Use classical volume rendering techniques to accumulate those colors and densities into a 2D image
  
![img1](https://user-images.githubusercontent.com/90370308/217326921-6ed2bf04-27ae-4b7d-85c1-ff4e2165910f.png)
*(a) Sampling 5D coordinates (location and viewing direction) along camera rays; (b) feeding those locations into an MLP to produce a color and 
volume density; c)using volume rendering techniques to composite these values into an image; (d) optimize the scene representation by minimizing 
the residual between synthesized and ground truth observed images*

The Optimization here is happening for a deep fully connected multi-layer perceptron without using any convolutional layers. Also, gradient descent is 
used to optimize this model by minimizing the error between each observed image and the corresponding views rendered from the representation.

## What is Sparseleap?
