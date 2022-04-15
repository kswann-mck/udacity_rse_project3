# udacity_rse_project3
Udacity Robotics Software Engineer Project 3 Where Am I

This project uses implements Adaptive Monte Carlo Localization in ROS to localize a robot within a model of a building.

# Installation

## Prepare the VM

Run the following commands to make sure the required dependencies are installed.

```
sudo apt-get install ros-kinetic-navigation
sudo apt-get install ros-kinetic-map-server
sudo apt-get install ros-kinetic-move-base
sudo apt-get install ros-kinetic-amcl
sudo apt-get install libignition-math2-dev protobuf-compiler
```

## Install the Project

Run the following commands to install the project.

```
git clone https://github.com/kswann-mck/udacity_rse_project3.git
cd udacity_rse_project3/catkin_ws
rm -rf build
catkin_make
```

## Run the project

Open two terminal windows. In the first window run the following from within the `catkin_ws` directory inside the project. This will launch Gazebo, and RViz with the robot loaded in the Gazebo model.

```
source devel/setup.bash
roslaunch my_robot world.launch
```

In the second window run the following to launch the localization.

```
source devel/setup.bash
roslaunch my_robot amcl.launch
```

In the RViz window, open the saved config `rviz_config.rviz` from within the `catkin_ws` folder. You should see the robot has localized itself. You can ask it to move to a new location using the `2D Nav Goal` tool by clicking on a location and dragging. As the robot moves towards the location you should see the PoseArray arrows cluster together and become more "sure" of the robot's pose.

# Important Notes

There was a lot of confusion around how to get localization to work in this project, and a couple of things really helped me.

1. The location of the robot within the Gazebo model, and the location of the robot within the map viewed in RViz need to be the same in order for localization to work properly. The easiest way I found to do this was to first position the robot where I wanted it in the Gazebo model, by editing the robot's pose in the world.launch file, then launching the `amcl.launch` file and viewing the location of the robot within the map in RViz, and adjusting the initial pose parameters in the `amcl.launch` file until the postion of the robot in the map matched the position of the robot within gazebo.
2. There are a lot of parameters that can be tuned in the AMCL package. The assignment lists a few parameters, but I didn't find that very helpful, and in searching for better options, I found [this research paper](https://www.researchgate.net/publication/349602009_An_Extended_Analysis_on_Tuning_The_Parameters_of_Adaptive_Monte_Carlo_Localization_ROS_Package_in_an_Automated_Guided_Vehicle/fulltext/6037cd1a4585158939cd8ec5/An-Extended-Analysis-on-Tuning-The-Parameters-of-Adaptive-Monte-Carlo-Localization-ROS-Package-in-an-Automated-Guided-Vehicle.pdf) discussing the parameters and proposing some alternatives to the default settings. 
