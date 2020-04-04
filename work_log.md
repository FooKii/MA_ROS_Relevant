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

