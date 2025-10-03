# coffee_cup_delivery_sensor_fusion

# Simulation
source ~/ros2_ws/install/setup.bash
ros2 launch the_construct_office_gazebo starbots_ur3e.launch.xml

# moveit2 packages for simulation
ros2 launch starbot_moveit_config move_group.launch.py

# hole detection for pointcloud
ros2 run basics_sensor_data complete_pipeline

# pick and place launch after hole detection is launched
ros2 launch moveit2_scripts pick_and_place_simulation.launch.py

# Real robot
# download pcl library 
sudo apt update
sudo apt install -y python3-pcl

# launch the website first
ros2 launch website_launch_pkg launch_website.launch.py

# launch the calibration test and press submit button for intial tests in website.
ros2 launch website_launch_pkg calibration_test.launch.xml

# if calibration is fine then launch the pick and place
ros2 launch website_launch_pkg complete_pipeline.launch.xml

# for mqtt download the pubfile and in the corresponding repo launch
cd ~/python_scripts
python3 pub_mqtt.py 

# similarly the sub file and in the corresponding repo launch
cd ~/ros2_ws/src/mqtt
python3 sub_mqtt.py
