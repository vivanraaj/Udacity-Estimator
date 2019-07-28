# Writeup #


## Criteria ##


### 1. Determine the standard deviation of the measurement noise of both GPS X data and Accelerometer X data. ###

I first recorded the noisy sensor data measurement for 'GPS X' and 'Accelerometer X' and calculated its standard deviation using numpy's standard deviation module. Then, I included these value for 'MeasuredStdDev_GPSPosXY' and 'MeasuredStdDev_AccelXY' in 'config/6_Sensornoise.txt'.

### 2. Implement a better rate gyro attitude integration scheme in the UpdateFromIMU() function. ### 

I used a non-linear approach for the filter with Euler forward method. By first using the rotation matrix based of present Euler angles, then integrating the body rate into new Euler angles and finally implementing them in QuadEstimatorEKF.cpp.

### 3. Implement all of the elements of the prediction step for the estimator ### 

The rotation matrix is required in the transition function and I have used the attitude.Rotate_BtoI(<V3F>) to perform these rotation from body frame to global frame. The implementation is done in the function PredictState() in QuadEstimatorEKF.cpp.

Next, I took the Jacobian of g to perform a linear approximation of the system and implemented them and  
Rbg' to predict the state covariance forward in the function Predict() in QuadEstimatorEKF.cpp.

I tuned the parameters of QPosXYStd and QVelXYStd in 
QuadEstimatorEKF.txt to capture the magnitude of the error.

### 4. Implement all of the elements of the prediction step for the estimator ###  ### 

First, I tuned the parameter QYawStd so that it approximately captures the magnitude of the drift. Since megnetometer reports yaw in the global frame, we used this information and implemented them in the UpdateFromMag() in QuadEstimatorEKF.cpp.

### 5. Implement the GPS update. ### 

Firt, I tuned the process noise model in QuadEstimatorEKF.txt to approximately captures the magnitude of the drift.
Next, by we incorporated the position and velocity information from GPS measurements together with its partial derivative into the function UpdateFromGPS() in QuadEstimatorEKF.cpp.

### 6. Adding Your Controller. ### 
I replaced the current controller with my previous project's controller in QuadController.cpp and retuned the controller parameters in QuadControlParams.txt.
