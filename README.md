# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

## Writeup

# MP.1
std::vector was used by removing the first element when the length exceeds a threshold

# MP.2
standard implemantion from CV was used by using the functions prototype as provided in "matching2D.hpp"
divided in a function for Harris (already provided) and function for ShaiTomasi and another function for modern detector

# MP.3
keypoints removal using the cv::Rect::contains functions from the keypoints detects in MP.2

# MP.4
as in MP.2 standard open cv was used, the challenge however was to sometimes the detected keypoints with certain alogrthims didnt work with descriptors, trial and error had to be done with some manual modifictions  that was needed (AKAZE not accepting point with class -1 for example)

# MP.5
FLANN and KNN were implemented as per the lessons and previous tutorials 

# MP.6
distance ratio was implemented as per the previous tutorials with a values of 0.4 for better matching results 

# MP.7
|detector| points | time(ms)|
|------|-------|-------|
|shi-tomasi|120|16|
|harris|20|14.4|
|FAST|150|1.5|
|BRISK|280|26|
|ORB|100|17|
|AKAZE|150|40|
|SIFT|130|75|


# MP.8
for the combinination from MP.7 the focus for the detector was on FAST for its speed and HARRIS for its low point count which will make matching faster but also because its timing it among the lowest after FAST

the observation was that SIFT as descriptors didnt work with both FAST and HARRIS and the result more or less was the same with all other descriptors alogorthims 


# MP.9

same as MP.8 with time measurement
even though HARRIS produced far less point which meant less time for the matching and descriptors extraction however the huge time taken by the feature extraction itself didn't break even
top 3 combination recommended are 
1-2 FAST detector  +  BRIEF| BRISK averaging 2.5 ms for detection + 1.5 ms for descriptors
3   FAST detector  +  ORB          averaging 2.5 ms for detection + 6 ms for descriptors
