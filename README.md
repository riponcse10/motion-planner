# Motion planner for self driving cars

In this project we will be implementing many of the behavioral and local planning concepts. The goal of this project will be to have a functional motion planning stack that can avoid both static and dynamic obstacles while tracking the center line of a lane, while also handling stop signs. To accomplish this, we will implement behavioral planning logic, as well as static collision checking, path selection, and velocity profile generation.

# Install the CARLA simulator

We use CARLA simulator version 0.9.11 to implement the project. The CARLA simulator can be downloaded from the website as a stanalone folder or docker image.

# Implementing the Motion Planner

Most important files of the project are "**behavioral_planner.py**", "**collision_checker.py**", "**local_planner.py**", "**path_optimizer.py**", and "**velocity_planner.py**" class files There are 5 main aspects of the planner we implement: behaviour planning logic, path generation, static collision checking, path selection, and velocity profile generation. 

## Behaviour Planning Logic

In this part of the project, we implement the behavioral logic required to handle a stop sign. We use a state machine that transitions between lane following, deceleration to the stop sign, staying stopped, and back to lane following, when it encounters a stop sign. All of the code for the behavioral planner is contained in behavioral_planner.py.

## Path Generation

For the path generation section of the project, the majority of the mathematical code for generating spiral paths is given to you. However, you will need to compute the goal state set (the set of goal points to plan paths to before path selection) using the get_goal_state_set() function, as well as some of the path generation helper functions. In particular, you will implement thetaf(), which computes the yaw of the car at a set of arc length points for a given spiral, optimize_spiral(), which sets up the optimization problem for a given path. Finally, once the optimization is complete, the resulting spiral will be sampled to generate the path. This functionality needs to be implemented in sample_spiral(). The required details about each of these functions are given in the code comments in the files local_planner.py and path_optimizer.py. Please complete all TODOs for this assignment.

## Static Collision Checking

For this part of the motion planner we implement `circle-based` collision checking on our computed path set using the `collision_check() `function. You will implement the circle location calculation for each point on the path. For futher details, please refer to the given code comments. Please complete all TODOs for this assignment.

## Path Selection

The path selection portion of the project involves you evaluating an objective function over the generated path set to select the best path. The goal of this section is to eliminate paths that are in collision with static obstacles, and to select paths that both track the centerline of the global path. To encourage robust obstacle avoidance, we will also need to add a term that penalizes how close the planned path is to other paths in the path set that are in collision with a static obstacle. You will implement path selection in the select_best_path_index() function within collision_checker.py. For further details, please refer to the given code comments. Please complete all TODOs for this assignment.

## Velocity Profile Generation

The last step of the project is velocity profile generation. This velocity planner will handle stop signs, lead dynamic obstacles, as well as nominal lane maintenance. This is all captured in the compute_velocity_profile() function in velocity_planner.py. You will be implementing the physics functions at the end of the file which will be used for velocity planning. For further details, please refer to the given code comments. Please complete all TODOs for this assignment.


# Running the CARLA simulator

In one terminal, start the CARLA simulator at a 30hz fixed time-step:

**Ubuntu:**

```
1./CarlaUE4.sh /Game/Maps/Course4 -windowed -carla-server -benchmark -fps=30
```

**Windows:**

```
./CarlaUE4.exe /Game/Maps/Course4 -windowed -carla-server -benchmark -fps=30
```

Note that both the **ResX=<pixel_width>** and **ResY=<pixel_height>** arguments can used to create a fixed size window, if you find the simulation to run too slow. See the CARLA installation guide for more details on how to use the arguments.

# Running the Python client (and controller)

In another terminal, change the directory to go into the "Course4FinalProject" folder, under the "PythonClient" folder.

Run your controller, execute the following command while CARLA is open:

**Ubuntu** 

```
python3 module_7.py
```

