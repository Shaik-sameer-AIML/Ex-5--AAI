<H3>ENTER YOUR NAME: Shaik Sameer</H3>
<H3>ENTER YOUR REGISTER NO: 212221240051</H3>
<H3>EX. NO.5</H3>
<H3>DATE: 25/03/2024</H3>
<H1 ALIGN =CENTER> Implementation of Kalman Filter</H1>
<H3>Aim:</H3> To Construct a Python Code to implement the Kalman filter to predict the position and velocity of an object.
<H3>Algorithm:</H3>
Step 1: Define the state transition model F, the observation model H, the process noise covariance Q, the measurement noise covariance R, the initial state estimate x0, and the initial error covariance P0.<BR>
Step 2:  Create a KalmanFilter object with these parameters.<BR>
Step 3: Simulate the movement of the object for a number of time steps, generating true states and measurements. <BR>
Step 3: For each measurement, predict the next state using kf.predict().<BR>
Step 4: Update the state estimate based on the measurement using kf.update().<BR>
Step 5: Store the estimated state in a list.<BR>
Step 6: Plot the true and estimated positions.<BR>

<H3>Program:</H3>

#Kalman Filter Constructor
```
class KalmanFilter:
  def __init__(self,F,H,Q,R,x0,p0):
    self.F= F
    self.H=H
    self.Q=Q
    self.R=R
    self.x=x0
    self.P=p0
  def predict(self):
    self.x =np.dot(self.F, self.x)
    self.P =np.dot(np.dot(self.F,self.P),self.F.T)+self.Q
  def update(self,z):
    y=z-np.dot(self.H,self.x)
    s=np.dot(np.dot(self.H,self.P),self.H.T)+self.R
    k=np.dot(np.dot(self.P,self.H.T),np.linalg.inv(s))
    self.x =self.x+np.dot(k,y)
    self.P=np.dot(np.eye(self.F.shape[0])-np.dot(k,self.H),self.P)

#defining values

import numpy as np
dt= 0.1
F=np.array([[1,dt],[0,1]])
H=np.array([[1,0]])
Q=np.diag([0.1,0.1])
R=np.array([[1]])
x0=np.array([0,0])
p0=np.diag([1,1])
kf=KalmanFilter(F,H,Q,R,x0,p0)

#true values - here we can't take true values, so we assigning values by our own
#estimate-values -using constructor Kalman Filter

true_states =[]
measurements=[]
for i in range(100):
  true_states.append([i*dt,1])
  measurements.append(i*dt+np.random.normal(scale=1))
est_states=[]
for z in measurements:
  kf.predict()
  kf.update(np.array([z]))
  est_states.append(kf.x)



#plotting estimate and true value

import matplotlib.pyplot as plt
plt.plot([s[0] for s in true_states],label='true')
plt.plot([s[0] for s in est_states],label='estimate')
plt.legend()
plt.show()
```
<H3>Output:</H3>

![314508445-98964738-ef54-4b80-9788-e60de25a2ffe](https://github.com/Shaik-sameer-AIML/Ex-5--AAI/assets/93427186/fed3d062-1f80-417e-83fb-89363ca6644a)


<H3>Results:</H3>
Thus, Kalman filter is implemented to predict the next position and   velocity in Python



