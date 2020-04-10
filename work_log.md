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
   * [pi_face_tracker](http://wiki.ros.org/pi_face_tracker)
   * Upper_body_detector 
   
   *pedsim: https://github.com/pirobot/svl_pedsim_gazebo
   

