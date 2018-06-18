# Unscented Kalman Filter Project 

The goal is to implement Unscented Kalman Filter to estimate the state of a moving object of interest with noisy lidar and radar measurements.

[//]: # (Image References)
[image1]: ./images/kf.png


### Setup
* Download Simulator [here](https://github.com/udacity/self-driving-car-sim/releases)
* Install uWebSocketIO [here](https://github.com/uWebSockets/uWebSockets)

### Basic Build Instructions
1. Make a build director  `mkdir build && cd biuld`
2. Compile: `cmake .. && make`
3. Run it: `./UnscentedKF`

### Implementation
The code for Kalman Filter is in the file `ukf.cpp`. I followed the Sensor Fusion algorithm as described in the preceding lesson. 

![alt text][image1]

#### First Measurements

I used the first measurements to initialize the state vectors and covariance matrices.

I did this in lines 100 to 120 in the function `ProcessMeasurement()` of `ukf.cpp`.

#### Prediction

Upon receiving a measurement after the first, the algorithm predicts object position to the current timestep and then update the prediction using the new measurement.

I did the prediction in lines 141 to 182 in the function `Prediction()` of `ukf.cpp`.

Prediction consists of 3 steps:

##### 1. Generate Sigma Points
I did this in lines 423 to 439 in the function `GenerateSigmaPoints()` of `ukf.cpp`.

##### 2. Predict Sigma Points
I did this in lines 366 to 314 in the function `PredictSigmaPoints()` of `ukf.cpp`.

##### 3. Predict Mean and Covariance
I did this in lines 166 to 178 in the function `Prediction()` of `ukf.cpp`.


#### Update

Update consists of 2 steps:

1. Predict Measurement
2. Update State

There are 2 types of sensor, lidar and radar. I handled the lidar and radar measurements differently. 

I did this for lidar in lines 188 to 251 in the function `UpdateLidar()` of `ukf.cpp`. And the radar measurements in lines 257 to 347 in the function `UpdateRadar()`.



### Result
I successfully obtained an RMSE [0.0693, 0.0835, 0.3336, 0.2380], which satisfies the requirement RMSE <= [.09, .10, .40, .30].

If using only radar, I obtained an RMSE [0.1552, 0.2030, 0.3954, 0.2952].

If using only lidar, I obtained an RMSE [0.1082, 0.0984, 0.6162, 0.2637].