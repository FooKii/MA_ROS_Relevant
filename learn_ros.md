* rqt_graph 查看节点图
* Install ROS packages from source:
    * [如何优雅的从源码安装ros软件包](https://blog.csdn.net/bluewhalerobot/article/details/88908320) [rosdep for dependencies installation and catkin_make for the environment]
*[Turtlebot3-gazebo安装，remote pc](http://emanual.robotis.com/docs/en/platform/turtlebot3/pc_setup/#install-dependent-packages)

* Question: why is package sometimes installed into opt/ros-version/share but sometime local at the git clone directory
    * involves the variable: $ROS_PACKAGE_PATH
    * where does rospack list search? prob. not only the $ROS_PACKAGE_PATH
        * 【答】ros命令只在$ROS_PACKAGE_PATH下搜寻，所以要想成功运行package有两种方法
            * 1. 将package安装到ros path下
                * 《如何安装到ros path下？》
            * 2. 安装后将package path添加到 ros path 中， 但每次terminal 关闭 添加就失效了。 为此要修改bashrc 最后一行添加 source ~/<es_path>/devel/setup.bash

* Question: rviz 中的 fix frame, 如何现实所有的在不同frame 下的sensor画面
    * [Answer] 用tf包工具发布global fixed frame到topic所在坐标系的tf关系, example:
    `rosrun tf static_transform_publisher 0.0 0.0 0.0 0.0 0.0 0.0 map xxx 100` xxx 映射为map
        
 * Connect Gazebo with ROS
   * spawn model from urdf file: 
      1. ```rosrun gazebo_ros spawn_model -file `rospack find MYROBOT_description`/urdf/MYROBOT.urdf -urdf -x 0 -y 0 -z 1 -model MYROBOT``` spawn_model 是 gazebo_ros package 的一个小 script
      2. http://gazebosim.org/tutorials?tut=ros_roslaunch&cat=connect_ros， 在model.config 里< sdf tag >直接使用urdf file
      3. Plugin: Sensor pluglin 要与link相联 《这可能是有时候gazebo内发布的影像坐标颠倒的原因》，link不是joint， joint 才会规定坐标系
      4. 直接include plugin 
      


