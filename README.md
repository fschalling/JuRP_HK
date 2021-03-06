# JuRP-HK Documentation
## GIT 101
Git is a version-control program (Google documents for code). It enables multiple people working with and in the same files, simuntainously. Also, uploading to the cloud = backup. 
### Alternative 1
Use the web browser interface to upload files through drag&drop.
### Alternative 2
Install a client to use the terminal commands below. Example guide: [http://happygitwithr.com/install-git.html](http://happygitwithr.com/install-git.html)
```
git clone https://github.com/fschalling/JuRP_HK.git

// First add the file to index
git add <file>

// Then merge all added files to a commit with an *mandatory* message 
git commit -m "The script now handles the X case"

// At last, upload to cloud
git push

// Download changes in the repository
// and merges with local files. add + commit changes before doing this!
git pull

// Prints out current status of files and more..
git status

```
## Start the software
1. On VICON_PC: Run *Vicon Tracker*
2. On VICON_PC: Run *C:\Program Files\Vicon\DataStream SDK\Win64\C\ViconDataStreamSDK_CTest.exe*
3. On USER_PC: Run *vicon_control/start*
4. On USER_PC: in *vicon_control.perspective - rqt* check *Markers* and then *Connect*
5. On USER_PC: Run *repos/JuRP_HK/motion_planner/motion_planner.m*

## Useful commands
* Add setup-file to the terminal's environment variables (here setup.bash for ROS Kinetic)

 ```>> echo source /opt/ros/kinetic/setup.bash >> ~/.bashrc```

* Uninstall packages (here ROS and all its sub packages)

```>> sudo apt-get remove ros-*```

* Install ROS Packages for Gazebo v9 (the version needs to be specified explicitly)
 
 ```>> sudo apt-get install ros-indigo-gazebo```

* Run a ROS launch file
 
 ```>> roslaunch path/to/file/file.launch```
 or
 
 ```>> roslaunch <ros_package> <launchfile>```
 
 * Before `roslaunch` is called rosdep must be created/updated

```
>> sudo rosdep init
>> rosdep update
```

* Publish message to a ROS topic 
 
 ```>> rostopic pub <topic_name> <message_name> <value>```
 example with a large message
 ```
 >> rostopic pub /cmd_vel geometry_msgs/Twist "linear:
  x: 0.2
  y: 0.0
   z: 0.0
angular:
   x: 0.0
   y: 0.0
   z: 0.1"
 ```
  
* Stop everything that has to do with ROS

```>> killall -9 rosout roslaunch rosmaster gzserver gzclient```

* Launch Matlab

 ```>> MATLAB_2018/bin/matlab```

* Print a ROS Topic to terminal
 
 ```>> rostopic echo <topic>```

* Setup a ROS master and list to a serial ROS node (on port /dev/ttyACM0) _http://wiki.ros.org/rosserial_arduino/Tutorials/Hello%20World_
```
>> roscore
>> rosrun rosserial_python serial_node.py /dev/ttyACM0
>> rostopic echo chatter
``` 


* Setup a a ROS master and a topic “toggle_led” which is read on the serial node _http://wiki.ros.org/rosserial_arduino/Tutorials/Blink_
```
>> roscore
>> rosrun rosserial_python serial_node.py /dev/ttyACM0
>> rostopic pub toggle_led std_msgs/Empty --once
``` 

## Useful links

* Install ROS Kinetic
[http://wiki.ros.org/kinetic/Installation/Ubuntu](http://wiki.ros.org/kinetic/Installation/Ubuntu)
* Install Gazebo
[http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install](http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install)

## How to ___.

* _Start streaming data from vicon via UDP_: 
On the Vicon PC run Programfiles/vicon/datastreamsdk/win64/ViconDataStreamSDK_Ctest.exe

# Ball Trajectory Documentation
## Samples
The ball trajectory estimater has n recorded samples with properties as: 

1. A throw mainly in YZ-plane
2. A throw mainly in XZ-plane
3. A throw diagonally

Each sample has three files as
```
/ball_trajectory/samples/samplen.mat
--------------
points: 300 ros objects
x_points: 300 x coordinates
y_points: 300 y coordinates
z_points: 300 z coordinates
sample_time_rel: 300 relative sample times 
```
and figures (*sn_xz.jpg*, *sn_yz.jpg*) of the trajectory. Below is the two planes for sample1:

![XZ_plane](/ball_trajectory/samples/s1_xz.jpg)
![YZ_plane](/ball_trajectory/samples/s1_yz.jpg)

