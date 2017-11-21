RUBRIC CHECKPOINTS

Valid Trajectories

Car drives without incident:
  - Car is avoids hitting other cars, exceeding max jerk or acceleration, and to choose a path which keeps it on the highway driving within lanes

The car drives according to the speed limit:
  - The car is given a reference velocity which influences the spacing of the x and y points pushed to next_x_vals and next_y_vals (lines 419-421)
  - The reference velocity is increased only when it is less that 49mph, unless it is too close to a car in front of it (line 412-417)

Max Acceleration and Jerk are not exceeded:
  - Velocity is only increased or decreased by .1 m/s in a .02s step (5 m/s^2 acceleration)
  - Anchor points representing a drivable path for the car were used to compute a spline (lines 334-390) so that points along this spline could be chosen that would form a nice continuous path and minimize jerk. The points were chosen a distance apart so that the car would maintain the desired velocity (lines 401-403, 419-421).

Car does not have collisions:
  - A check is performed to see if there is a car in front of the test car and that the car in front's future location is within 30m of the test car's future location (lines 279-300). If there is a car in front, then the too_close flag is triggered. 
  - The isLaneEntryPossible function (lines 163-185) determines if there is a car that will be within 50m of the test car's future location so that the car only enters the lane if it has ample space to make a safe lane change. Depending on the current lane of the test car, whether there is a safe lane to change into is checked and then the lane of the car is switched (lines 305-319). 
  - The car will also slow down if it is too close to another car, which is necessary in instances when there are traffic jams and a lane change is not possible (lines 412-417).

The car stays in its lane except for changing lanes:
  - The car's trajectory is interpolated from points which are transformed to xy coordinates based on frenet coordinates and map waypoints. The frenet d is designated as being in the middle of the target lane (lines 365-367).
  - The car remains in the same lane except for a lane change. Once the lane is changed, the anchorpoints used to calculate the spline are in the target lane, so the lane change will be executed in under 3 seconds (should be within the 1 second of the 50 0.02 second steps). 

The car is able to change lanes:
  - When there is a slower moving vehicle in front, then the adjacent lanes are checked for traffic (305-319, 163-185) and the car switches into that lane.







