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
      
* /tf
   * publish tf with robot_state_publisher http://wiki.ros.org/robot_state_publisher/Tutorials/Using%20the%20robot%20state%20publisher%20on%20your%20own%20robot
   * 注意要订阅两个： urdf 和 joint state topic
      * http://wiki.ros.org/urdf/Tutorials/Using%20a%20URDF%20in%20Gazebo 这个写了如何让gazebo发布joint state(原错/tf) 用roscontrol plugin
      * 然后再加上urdf 就有了tf
  * Rviz debug mode: rosconsole set /rviz_1585767957182131372 ros.rviz.message_filter debug
   
   * 检查urdf可否被应用的gazebo：```z sdf -p MODEL.urd ;  cat ~/.gazebo/gzsdf.log ```
   
* Joint state controller & position controller:
   * joint_state_controller 负责发布joint的状态信息 这样node like rviz 就可以订阅joint state 然后正确的显示出它的位置状态
   * joint_position_controller 负责来控制joint， 发布一个新的pose， state就会更新这个pose 
* 如何launch 这些controller
   * 这些controller都被集成在 ros_control 中 要想启动这些 先要定义一个config.yaml 里面declare了要启动哪一个controller 以及他们的发布频率。。。
   * 有了这些yaml file，在launch文件中把他们load进param server， 然后在启动controller manager时给予这些param 如下：
   ``` 
   <rosparam command="load"
            file="$(find urdf_sim_tutorial)/config/joints.yaml"
            ns="r2d2_joint_state_controller" />
  <rosparam command="load"
            file="$(find urdf_sim_tutorial)/config/head.yaml"
            ns="r2d2_head_controller" />

  <node name="r2d2_controller_spawner" pkg="controller_manager" type="spawner"
    args="r2d2_joint_state_controller
          r2d2_head_controller
          --shutdown-timeout 3"/>
   ```
      


