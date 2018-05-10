mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make

cd ~/catkin_ws/src
git clone https://github.com/caudaz/RoboND-Perception-Project

cd ~/catkin_ws
rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y

(----- for sensor stick---------)
cp -pR ~/Downloads/robotND1-proj3-master/class_code/L17_Exercise-3/sensor_stick/ ~/catkin_ws/src/RoboND-Perception-Project/.
chmod 755 -R ~/catkin_ws/src/RoboND-Perception-Project/sensor_stick/

cd ~/catkin_ws
catkin_make

------------------------------
Errors in files: pr2_motion.cpp AND pr2_pick_place_server.cpp
Ex1: cast variable using static_cast
bool right_success = right_move_group.move();
bool right_success = static_cast<bool>(right_move_group.move());
Ex2:
left_success = left_move_group.move();
------------------------------

export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/models:$GAZEBO_MODEL_PATH
source ~/catkin_ws/devel/setup.bash
cd ~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/scripts
chmod u+x pr2_safe_spawner.sh
./pr2_safe_spawner.sh

(----- for sensor stick---------) TERMINAL1
export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/sensor_stick/models
source ~/catkin_ws/devel/setup.bash
roslaunch sensor_stick training.launch

(----- for sensor stick---------) TERMINAL2
source ~/catkin_ws/devel/setup.bash
rosrun sensor_stick capture_features.py


=====
Files
=====

main file to modify:
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/scripts

worlds 1 2 3:
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/worlds/test*.world

to change the name of the world:
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/launch/pick_place_project.launch

pick lists for worlds 1 2 3
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/config/pick_list_*.yaml
