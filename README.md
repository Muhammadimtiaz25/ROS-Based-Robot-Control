# ROS-Based-Robot-Control
#!/usr/bin/env python

import rospy
from geometry_msgs.msg import Twist

def move_robot():
    # Initialize the node
    rospy.init_node('robot_controller', anonymous=True)

    # Create a publisher to the /cmd_vel topic
    pub = rospy.Publisher('/cmd_vel', Twist, queue_size=10)

    # Set the rate of sending messages (10 Hz)
    rate = rospy.Rate(10)

    # Create a Twist message to send to the robot
    move_cmd = Twist()

    # Set linear and angular velocities
    move_cmd.linear.x = 0.5  # Move forward at 0.5 m/s
    move_cmd.angular.z = 0.0  # No rotation

    # Continuously send commands until ROS is shut down
    while not rospy.is_shutdown():
        pub.publish(move_cmd)
        rate.sleep()

if __name__ == '__main__':
    try:
        move_robot()
    except rospy.ROSInterruptException:
        pass
