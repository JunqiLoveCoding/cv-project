# cv-project
computer vision class projects in Spring 2019, Tandon school of engineering, NYU

## Stereo

### Introduction
Stereo is a commonly used method to get depth information from two images. The main process of constructing stereo is firstly getting two images(left image and right image) with two calibrated cameras, and then rectifying images to compute disparity, and finally generating a depth map. The key point of computing disparity is to find correspondence points between the two images with epipolar lines. To simplify this problem, the pair of images usually taken by parallel cameras to rectify the images, so the scanlines are horizontal epipolar lines. This kind of stereo is called binocular stereo. The basic method of finding correspondences is block matching algorithm, which is a dense stereo method to output the disparity of two images for every pixel. 

### Environment
  - numpy
  - opencv
  
### Method
Here we implement **block matching** method and three cost functions to compute disparity.

* Algorithm  
**Input :** left grayscale image L, right grayscale image R, scan window size S, scan range &sigma;  
**for each** pixel p<sub>i</sub> **in** L:  
&nbsp;&nbsp;&nbsp;&nbsp;select a window of size S in L with p<sub>i</sub> as the centre point  
&nbsp;&nbsp;&nbsp;&nbsp;**for each** pixel p<sub>j</sub> **on** the scanline of p<sub>i</sub> **in** R:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** p<sub>j</sub> is in the scan range &sigma;:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;select a window of size S in R with p<sub>j</sub> as the centre point  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;compare two windows with match metric and get the cost of block matching  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;select pixel p<sub>min</sub> with minimum cost in R  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;compute disparity between p<sub>i</sub> and p<sub>min</sub> 
generate a disparity map for every pixel in L  
map the disparity map to depth map  
**Output :** disparity map  

+ Cost Functions
  - Sum of squared differences (SSD)  
  - Sum of absolute differences (SAD)  
  - Normalized cross-correlation (NCC)  
  
### Result
The test data we used is the pentagon scene from Carnegie Mellon Vision.  
![alt text](/stereo/pentagon_left.bmp "Left") ![alt text](/stereo/pentagon_right.bmp "Right")

