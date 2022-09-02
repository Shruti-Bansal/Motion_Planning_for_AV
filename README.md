# Motion_Planning_for_AV

In this project, we implement two of the main components of a traditional hierarchical planner: The Behavior Planner and the Motion Planner. Both will work in unison to be able to:

1. Avoid static objects (cars, bicycles and trucks) parked on the side of the road (but still invading the lane). The vehicle must avoid crashing with these vehicles by executing either a “nudge” or a “lane change” maneuver.
2. Handle any type of intersection (3-way, 4-way intersections and roundabouts) by STOPPING in all of them (by default)
3. Track the centerline on the traveling lane.

To accomplish this, we implement:

1. Behavioral planning logic using Finite State Machines - FSM
2. Static objects collision checking.
3. Path and trajectory generation using cubic spirals
4. Best trajectory selection though a cost function evaluation. This cost function will mainly perform a collision check and a proximity check to bring cost higher as we get closer or collide with objects but maintaining a bias to stay closer to the lane center line.

# Performance on CARLA
After the implementation in code, the car behaves well in CARLA simulator avoiding all obstacles in it's path to complete the route. It avoids the three vehicles parked on the lane and roadside, and turn smoothly on the two intersections. Behavioral planning makes the follow lane and change lane left/right states, then six trajectories are generated by cubic spirals method all the time. The trajectory of the motion with the lower cost is implemented for the ego vehicle.

<img src="https://github.com/Shruti-Bansal/Motion_Planning_for_AV/blob/main/images/pic1.png">
<img src="https://github.com/Shruti-Bansal/Motion_Planning_for_AV/blob/main/images/pic2.png">
<img src="https://github.com/Shruti-Bansal/Motion_Planning_for_AV/blob/main/images/pic3.png">

#Summary
The traditional hierarchical planner has three layers: Behavior planning, Trajectory generation and Motion planning.

Behavior planning: Finite state machines is used to divide the behavior actions on the road into finite states, such as, follow lanes, stop, decel to stop, change lanes.Cost functions are used to make beahvior level decisions.

Trajectory Generation: Generates drivable trajectories. For the unstructured enviornment, such as the parking lot, the hybrid A* is suitable for trajectory generation and for the structured environment, such as the highway traffic road, the sampling based polynomial trajectory generation is implemented.

Motion planning: Path Planning, Velocity Profile Generation and Collision detection.Sigle step minimum jerk polynominal isn't implemented due to the discontinuty of the curvature and first derivative curvature. Cubic sprial is implemented for generating the trajectory. Rimpson rule is used for solving the (x,y) position of the ego vehicle due to the no-close form solution. The velocity profile is generated according to the linear acceleration and compositional linear accelertion conditions. Collision check is done on the basis of 3 circles each enclosing the ego vehicle and obstacle vehicles.
