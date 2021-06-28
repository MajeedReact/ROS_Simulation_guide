# ROS_Simulation_guide
This ROS simulation guide will be done with a pre built robot from Turtlebot3 and using SLAM approach

### First of all make sure to know what type of ROS do you have, for this guide I will be using ROS melodic as well as Turtlebot3 melodic version.

1. Install ROS 1 on Remote PC using the following commands in the terminal: \
  `sudo apt-get update`\
  `sudo apt-get upgrade`\
  `wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic.sh`\
  `chmod 755 ./install_ros_kinetic.sh`\
  `bash ./install_ros_kinetic.sh`
   - If the installation above failed please refer to [the official ROS1 Melodic installation guide](http://wiki.ros.org/melodic/Installation/Ubuntu)
  
 2. Install Dependent ROS 1 Packages in one run
 
  ```
  sudo apt-get install ros-melodic-joy ros-melodic-teleop-twist-joy \
  ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc \
  ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan \
  ros-melodic-rosserial-arduino ros-melodic-rosserial-python \
  ros-melodic-rosserial-server ros-melodic-rosserial-client \
  ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server \
  ros-melodic-move-base ros-melodic-urdf ros-melodic-xacro \
  ros-melodic-compressed-image-transport ros-melodic-rqt* \
  ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers
  ```
  
  3. Install TurtleBot3 Packages \
  
    `sudo apt-get install ros-melodic-dynamixel-sdk`\
    `sudo apt-get install ros-melodic-turtlebot3-msgs`\
    `sudo apt-get install ros-melodic-turtlebot3`
     
     
### Down below is the installation of GAZEBO simulator

1. Install Simulation Package 
   - Move to src folder `cd ~/catkin_ws/src/`
   - Clone the repos `git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git`
   - `cd ~/catkin_ws && catkin_make`

2. Now we can launch the simulation into an empty world 
   - Set the default TURTLEBOT3_MODEL name to your model. 
  
     Incase if you want to use the burger model enter the following command 
    - `echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc`    
     In my case I will be using the waffle model
     
    - `echo "export TURTLEBOT3_MODEL=waffle_pi" >> ~/.bashrc` \
    
      to launch the simulator into an empty world `roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch`
      
      to launch into TurtleBot3 World 
      `roslaunch turtlebot3_gazebo turtlebot3_world.launch`\
      
      to launch into TurtleBot3 House 
      `roslaunch turtlebot3_gazebo turtlebot3_house.launch`\
      
      *NOTE*: If TurtleBot3 House is launched for the first time, downloading the map may take more than a few minutes depending the network status.
      *How to quit the simulator?* Go to terminal and press `CTRL` with `C`
      
### SLAM simulation 

1. To run SLAM node \
    `export TURTLEBOT3_MODEL=waffle_pi`\
    `roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping`
 
2. Run Teleoperation Node
    Open a new terminal from Remote PC with Ctrl + Alt + T and run the teleoperation node from the Remote PC. \
    `roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch` 
    ``` Control Your TurtleBot3!
         ---------------------------
         Moving around:
                w
           a    s    d
                x

         w/x : increase/decrease linear velocity
         a/d : increase/decrease angular velocity
         space key, s : force stop

         CTRL-C to quit```
