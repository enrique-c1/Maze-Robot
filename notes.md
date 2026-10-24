/scan
    Lidar data. It's a LaserScan message: an array of distances to the nearrest obstacle at each angle around the robot(360 degrees). Nav2 uses it to mark obstacles in the costsmaps, AMCL compares it against the map to work out where the robot is, and slam_toolbox uses it to build a map
/cmd_vel
    Command that tells the robot how to move. It carries a Twist messages with a forward speed (linear.x) and turning speed (angular.z). Whoever wants the robot to move publishes here
/odom
    robots estimate of its own motion calculates from its wheels (how far each has turned). Its an Odometry message with position, orientation, and velocity, relative to where the robot started. It drifts over time because of wheel slip which is corrected using /scan.
/map
    map of the enviroment, an occupancy grid: a 2D gride where each cell is marked free, occupied(wall), or unknown. 

LOOP:
    /scan + /odom -> localization or SLAM -> /map and robot pose -> Nav2 planes a path -> /cmd_vel -> robot moves -> new /scan and /odom