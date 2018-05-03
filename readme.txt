$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make

$ cd ~/catkin_ws/src
$ git clone https://github.com/caudaz/RoboND-Perception-Project

$ cd ~/catkin_ws
$ rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y

$ cd ~/catkin_ws
$ catkin_make

------------------------------
Errors in files:
pr2_motion.cpp
pr2_pick_place_server.cpp
Solution: cast variable using static_cast
example1
bool right_success = right_move_group.move();
bool right_success = static_cast<bool>(right_move_group.move());
example2
left_success = left_move_group.move();
left_success = left_move_group.move());
------------------------------

export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/models:$GAZEBO_MODEL_PATH

source ~/catkin_ws/devel/setup.bash

cd ~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/scripts
chmod u+x pr2_safe_spawner.sh
./pr2_safe_spawner.sh

