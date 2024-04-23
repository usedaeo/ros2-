
     . install/setup.bash
     
colcon build --packages-up-to <name-of-pkg>

 
  坐标系  rviz
 ros2 launch deliverbot_description deliverbot_description_xacro.launch.py 
 
控制车
 ros2 run teleop_twist_keyboard teleop_twist_keyboard 
 

ws_tool8_fangzhen

仿真环境  已有odon scan depth imu 等
ros2 launch deliverbot_description mygazebo.launch.py 

雷达里程计

ros2 launch rf2o_laser_odometry rf2o_laser_odometry.launch.py


处理雷达信息   scan-> scanL 
 ros2 run chulilaser myleasr



处理深度   depth-> depth_scan
ros2 launch depthimage_to_laserscan depthimage_to_laserscan-launch.py


融合  scanL + depth_sacn     尽量面向90度   60度
ros2 launch ira_laser_tools laserscan_multi_merger.launch 


 融合雷达里程计

ros2 launch robot_localization ekf.launch.py

融合 odon 雷达里程计 imu

ros2 

建图  使用 融合里程计+ 融合后的雷达
ros2 launch myrobot_cartographer cartographer.launch.py 

