# NoteForPeopleTracking
----
## slam:
* 打开激光
  * roslaunch velodyne_pointcloud VLP16_points.launch
* 打开建图
  * roslaunch hdl_graph_slam hdl_graph_slam_501.launch 【注：使用实体激光时，需要commen out其中的一个node；501是应用在室内的luanch，400是应用在室外环境的（耦合了机器人里程计？）；要把sensor height这个参数调整到激光的实际高度，推荐高度在1.5m左右，准确度较高；】
* 打开可视化
  * roscd hdl_graph_slam/rviz/
  * rviz -d hdl_graph_slam.rviz 
* 保存地图为pcd文件（destination修改为自己的路径）
  * rosservice call /hdl_graph_slam/save_map "utm: false resolution: 0.01 destination: '/home/arvin/Documents/temp6.pcd'" 

----
## trakcing：
* 开激光驱动
  * roslaunch velodyne_pointcloud VLP16_points.launch
* 打开tracking包
  * roslaunch hdl_people_tracking hdl_people_tracking.launch 【注：使用实体激光时，需要comment out hdl_localization.launch中的一个node；hdl_people_tracking.launch中的enable_classification的意义是在聚类后再做一步行人检测，建议把它改成false，否则会导致 当人离激光较近时，人会丢失（由于视距原因，人的特征超出激光的视野了）；记得在hdl_localization.launch中的globalmap_pcd改为slam时pcd的保存位置】
* 打开可视化
  * roscd hdl_localization/rviz/
  * rviz -d hdl_localization.rviz 

----
## todo：
* 对探测到的人进行二次滤波，可以根据该人在膨胀后的costmap中的数值来进行删减
* 激光和rgbd的匹配

----
