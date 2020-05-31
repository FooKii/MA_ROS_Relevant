* 25.03.20
    * pedsim, still no human model
* 26.03.20
    * WIP:robotino3 with sensor working
* 27.03.20
   * Read gazebo tutorial, to attach sensors: ```<include> & <joint>```
   * tmr: read sensor and actor section
* 31.03.20
   * the reason for < Cam_view in robotino > is the bad scale & make for mesh file
   * decide to make a self-easy 2-wheel robot, all on own
* 01.04.20
   * debug, create a lauch file #discussion, would be better if i use urdf but instead i used sdf, cause robotino has different shape also can be converted to urdf later. Kinect & laser works fine now
   * try integrate with ppl_detec -- how to pass argument in launch file
* 04.04.20
   * Regarding /tf topics in gazebo. To publish /tf, a < robot_state_publisher > is needed, but it only supports urdf file, not sdf. So considering switch from sdf to urdf + gazebo files
   *  to publish /tf topics:
      *  using urdf file and method described above
      *  gazebo itself publishes /gazebo/joint_state & /model_state, this can transforms to a /tf topic. There's a existing node doing this, see: http://wiki.ros.org/gazebo2rviz
   * Method 1 is chosen cause urdf file is more needed later in real robot and has a wider use
   * A quick try: add ros control plugin in sdf file, see if any /tf publishment  
      ```[ERROR] [1586045338.023356025, 6.958000000]: GazeboRosControlPlugin missing <legacyModeNS> while using DefaultRobotHWSim, defaults to true.This setting assumes you have an old package with an old implementation of DefaultRobotHWSim, where the robotNamespace is disregarded and absolute paths are used instead.If you do not want to fix this issue in an old package just set <legacyModeNS> to true.``` is given and still no /tf topics
* 05.04.20
   * create urdf for 2_wheel_robot without sensors and vislized in rviz. Note: the origin's reference frame in .urdf file is different from the < pose > tag in sdf file
   * urdf and gazebo file for 2 wheel robot with sensors, to be brought into gazebo to check functionality, next step is to learn "creating ros package" casue the reletive path included in the urdf file need the package first to be installed
* 06.04.20
   * finish Cmakelist and package.xml, adding lauch folder and config folder
   * Next: 
      * to have /tf we need robot_state_publisher
         * robot_state_publisher needs urdf file & joint state
            * so first need joint state working, reference http://wiki.ros.org/urdf/Tutorials/Using%20a%20URDF%20in%20Gazebo
* 07.04.20
   * packages can be built now
   * joint positions wrong in rviz
   * joint positions fixed in rviz
   * in gazebo, no /tf info about wheel hinge, reason is that joint_state_publisher is integrated as a plugin in gazebo, this plugin is not working correctly.
   * all joint works correctly with /tf now
   * Next, a bug fix with laser sensor

* 08.04.20
   * laser plugin bug caused by gpu fixed
   * integrated leg_detector, bug caused by odom_combined
   * bug fixed, leg_detector functional.

* 09.04.20
   * integrate face_detection.

* 10.04.20
   * Upper_body_detector
   * strands/upper_body_detector: might need /map, at least for tracking
      * advised to use fix_groundplane, ```roslaunch ground_plane_estimation ground_plane_fixed.launch [parameter_name:=value]```
      * hog: 方向梯度直方图
   * fixed strands/upper_body, now working
   
* 13.04.20
   * strands with fusion
   
* 14.04.20
   * Spencer with single_rgbd
   
* 15.04.20
   * Spencer with fusion
   * next: pedsim for tracking 
* 16.04.20
   * Pedsim in gazebo
   * bag file
* 19.04.20
   * A world with pedsim and robot
   * check if tracking is functioning
* 20.04.20
   * Still some pedestrian went out of sensor-range
   * Next step would be modify ped-sim crowd moving area
   * extract ground_truth from pedsim [this will need a msg converter]
* 21.04.20
   * Msg converter from tf to actor_pose
   
* 22.04.20
   * vel_converter

* 23.04.20
   * adjust: orientation from spencer/tacker has z = 1, but gt mostly only w =1

* 11.05.20
   * Set up for gazebo-experiment of detection uncertainty
      1. static leg
      2. static upper
      
* 12.05.20
   * A evaluate-system for single moving person
      1. modify pedsim
      2. modify gt-msgc_conversion
      3. python-script to plot the data, 2 trajectories and a chart of err distribution
    
* 20.05.20
   * Python scripts to compare motion vectors
   
* 23.05 - 27.05
   * trajectory of speed vector -- done
   * randomized speed -- smooth and path -- to modify pedsim
   * tracking with upper_body alone
   * horizotal path
   * diagonal path
   
* 31.05
   * Check if rotational speed indeicate large err
   * angular twist not implemented, orientation can be used (0, 0, sin(theta/2), cos(theta/2))
   * we can write a script to compare if orientation is changed, thus giving a indicate
