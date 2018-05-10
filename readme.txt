mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
cd ~/catkin_ws/src
git clone https://github.com/caudaz/RoboND-Perception-Project
cd ~/catkin_ws
rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y

(----- for sensor stick features capture ---------)
cp -pR ~/Downloads/robotND1-proj3-master/class_code/L17_Exercise-3/sensor_stick/ ~/catkin_ws/src/RoboND-Perception-Project/.
chmod 755 -R ~/catkin_ws/src/RoboND-Perception-Project/sensor_stick/

cd ~/catkin_ws
catkin_make

------------------------------
Errors in files: pr2_motion.cpp AND pr2_pick_place_server.cpp
Ex: cast variable using static_cast
bool right_success = right_move_group.move();
bool right_success = static_cast<bool>(right_move_group.move());
------------------------------

export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/models:$GAZEBO_MODEL_PATH
source ~/catkin_ws/devel/setup.bash
cd ~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/scripts
chmod u+x pr2_safe_spawner.sh
./pr2_safe_spawner.sh




(----- for sensor stick features capture ---------) TERMINAL1
export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/sensor_stick/models
source ~/catkin_ws/devel/setup.bash
roslaunch sensor_stick training.launch 

(----- for sensor stick features capture ---------) TERMINAL2
source ~/catkin_ws/devel/setup.bash
rosrun sensor_stick capture_features.py
NOTE: capture_features.py list is changed: models =['biscuits','soap','soap2','book','glue','sticky_notes','snacks','eraser']
NOTE: output is training_set.sav saved to ~/.



(----- for sensor stick features training ---------) TERMINAL
export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/sensor_stick/models
source ~/catkin_ws/devel/setup.bash
rosrun sensor_stick train_svm.py
NOTE: output is ~/model.sav



(----- for pr2_robot PREDICTIONS ---------) TERMINAL1
export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/models:$GAZEBO_MODEL_PATH
source ~/catkin_ws/devel/setup.bash
roslaunch pr2_robot pick_place_project.launch


(----- for pr2_robot PREDICTIONS ---------) TERMINAL2
export GAZEBO_MODEL_PATH=~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/models:$GAZEBO_MODEL_PATH
source ~/catkin_ws/devel/setup.bash
rosrun pr2_robot project_template.py
NOTE: project_template.py will call model.sav
NOTE: output prediction labels will show in RVIZ window
NOTE: output to terminal: 
[INFO] [1525964533.106980, 1112.401000]: Detected 3 objects: ['biscuits', 'soap', 'soap2']
[INFO] [1525964533.155272, 1112.426000]: yaml sent



===============
PROJECT FILES
===============

main file to modify:
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/scripts/project_template.py

to change the name of the world:
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/launch/pick_place_project.launch

worlds 1 2 3:
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/worlds/test*.world

pick lists for worlds 1 2 3
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/config/pick_list_*.yaml

FINAL OUTPUT SUBMISSION AFTER FEATURES AND TRAINING (3 .yaml files)
~/catkin_ws/src/RoboND-Perception-Project/pr2_robot/config/output.yaml (sample output)
should be called output_1.yaml output_2.yaml output_3.yaml
