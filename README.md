# orbital-mechanics-simulator
from math import *
import numpy as np
import matplotlib.pyplot as plt

#plan 
#import functions for accelation in the x and y direction
#import functions for the vecloty and functions for the displacement 
#import functions the forward euler 
#import functions for rk4

#longer version for now 
#constants 
G = 6.67430*1e-11
M = 5.972*1e24

#the radius of the earth
RE = 6.371*1e6 


h = 1

#the accalaration in both the x and y axis
n = 0

ax = [0]*5000
ay = [0]*5000

vx = [0]*5000
vy = [0]*5000


vx[0]= 0
vy[0]= 7700


sx = [0]*5000
sy = [0]*5000

sx[0] = 6.771 *1e6 
sy[0] = 0 





print (ax) 
print (ay)

# apply this to the velcoity then apply that to the displacement then go again, however we can create a function instead! 

while n < 4999:
    
     
    
    ax[n] = (-G*M *sx[n])/(sx[n]**2 + sy[n]**2)**(3/2)
    ay[n] = (-G*M *sy[n])/(sx[n]**2 + sy[n]**2)**(3/2) 

    vx[n+1]= ax[n]*h + vx[n]
    vy[n+1]= ay[n]*h + vy[n]

    sx[n+1]= vx[n]*h + sx[n]
    sy[n+1]=vy[n]*h + sy[n]

    radius = np.sqrt(sx[n+1]**2 + sy[n+1]**2)

    if radius <= RE:
        print("Spacecraft has collided with Earth")
        break
    

    n = n+1 

plt.plot(sx, sy)
plt.axis('equal')
plt.xlabel('x position (m)')
plt.ylabel('y position (m)')
plt.title('Orbit using Forward Euler')
plt.show()
