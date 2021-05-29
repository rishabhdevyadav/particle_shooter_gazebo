# particle_shooter_gazebo
Gazebo plugin for particle shooter\
ORIGINAL REPO: https://bitbucket.org/theconstructcore/particle_shooter/src/master/

![Alt text](https://github.com/rishabhdevyadav/particle_shooter_gazebo/blob/main/particle_shooter/gif/simulation.gif)

## Launch
```bash
roslaunch particle_shooter main.launch
```

Sometime Gazebo will lag or give erros even after terminating the launch file.\
Wait for few seconds and give command ```  killall -9 gazebo & killall -9 gzserver  & killall -9 gzclient     ```

## MINIMAL PARAMETERS TO BE TUNED

### model.sdf
REFERENCE: http://gazebosim.org/tutorials/?tut=ros_urdf

Here you can define properties of small sphere. Add or remove property from above reference. 
```bash
mass: <mass>
inertia: <inertia>
size: <radius>
friction coefficient: <mu> & <mu2>
Contact stiffness: <kp> 
damping: <kd>
maximum velocity: <max_vel>
particle contact surface property: <contact>
<velocity_decay>
<self_collide> (enable or disable)
<kinematic> (enable or disable)
<gravity> (enable or disable)
```
Among all most important is "gravity". You can enable (1) or disable (0) the gravity effect on particle.\
You can see "model name=particle_sphere". So all these property are applied to model named "particle_sphere" only.\
Play with last 4 parameter to see the effects.


### particle_shooter.world
In simulation, there are set of spheres which will be realsed from a particular origin and disappear automatically after a certian time.

Here you can increse number of particle (100 right now, more than original) by calling ```<uri>model://particle_sphere</uri>``` \
and naming each particle by different title``` <name>particle_sphere100</name>  ```. 

```bash
the speed new particle will come: <reset_frequency> (most important para)
<x_axis_force> (intial force in x direction)
<y_axis_force> (intial force in y direction)  
<z_axis_force> (intial force in z direction)

<x_origin>
<y_origin>
<z_origin>

<random_range> (origin point will have some range; if 0 then all particle will relase same origin)
```
We are giving force in y-direction and due to gravity particle is falling down. Increase(decrease) the mass and decrese(increase) the force,
particle will fall near to its origin. You can control how far spheres to be thrown.

Give some value to ```<random_range>``` so that particle seems scattered on floor.

TIP1: You can create "model name=particle_sphere2" having no gravity effect or some other physical property (maas) in sdf.\
      So that, behaviour of particle_sphere and particle_sphere2 will be different in simulation.\
TIP2: Increase the particle and <reset_frequency>


# SKID STEER ROBOT
REFERENCE: https://github.com/aditirao7/auto_trav

![Alt text](https://github.com/rishabhdevyadav/particle_shooter_gazebo/blob/main/auto_trav/skid_steer.png)

### launch 
```
roslaunch mybot_gazebo mybot_world.launch
```
Original repo has been modified by commenting sensors like camera, lidar, imu, gps.\
For reference, uncomment them in file ``` mybot.gazebo ``` and ```mybot.xacro  ```

```
rostopic pub -r10 /cmd_vel geometry_msgs/Twist "linear:
  x: 1.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 1.5"
```
