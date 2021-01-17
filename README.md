# calculator
a not so scientific calculator with all basic features and and keyboard support. will definitely like to get any bugs
<launch>

  <arg name="model" default="$(find ros_robotics)/urdf/dd_robot4.urdf"/>
  <arg name="gui" default="true" />
  <arg name="rvizconfig" default="$(find urdf_tutorial)/rviz/urdf.rviz" />

  <param name="robot_description" command="$(find xacro)/xacro.py $(arg model)" />
  <param name="use_gui" value="$(arg gui)"/>

  <node name="joint_state_publisher" pkg="joint_state_publisher" type="joint_state_publisher" />
  <node name="robot_state_publisher" pkg="robot_state_publisher" type="robot_state_publisher" />
  <node name="rviz" pkg="rviz" type="rviz" args="-d $(arg rvizconfig)" required="true" />

</launch>

#!/usr/bin/env python

import rospy
from geometry_msgs.msg import Twist

# def stopper():
#    rospy.loginfo('stopping turtlebot')
#    cmd_vel.publish(Twist())
#    rospy.sleep(1)



rospy.init_node('turtle_control',anonymous='true')
rospy.loginfo('press ctrl+c to stop turtle bot')


cmd_vel = rospy.Publisher('cmd_vel',Twist,queue_size = 10)
rate = rospy.Rate(10)
mov_cmd = Twist()
mov_cmd.linear.x = 0.05
mov_cmd.angular.z = 0.0

while not rospy.is_shutdown():
            cmd_vel.publish(mov_cmd)
            rate.sleep()

#rospy.on_shutdown(stopper())
