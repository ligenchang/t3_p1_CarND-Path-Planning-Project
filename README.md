# CarND-Path-Planning-Project
This is the first project of term 3 of Self-Driving Car Engineer Nanodegree Program. I have learnt how to do prediction, behavior planning and trajectory generation.
[//]: # (Image References)

[image1]: ./images/result.png "Path panning result"

### Goals
In this project, the goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.

### How to generate path

The path generation includes following 5 steps:
1. Firstly I use sensor fusion information from simulator to check if the car's current line is too close to the car in front of it, if it's too close, we need redeuce the velocity gradually
2. I need to check if the car's left and right lane has space to make sure the car can change lane if the front car of current lane moves too slow. When making the lane change, will check which lane's car is far from the current car and will switch to that lane to reduce the probablity of blocking. Also, can't forget to wait unitl the car's lane switching is successful then we can do next lane change in order to avoid the frequent lane changing.
3. Then will check the car's previous path points, if the number is too small, it will use the current car's state to generate the path. Otherwise, I will use previous path point list's last 2 elements plus the current car's s value + 30, 60 ,90 to predicate the direction of car in fucture
4. To help the car's transition become smooth, I re-use pervious path's points and also utilize the spline lib to generate the new path

This is the result of project code which was running in simulator:
![path planning][image1]


## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

# Result Video
Result video can be seen from here:
[link to result.mov](./result.mov)