3) gamepad_control

Description : Receives input from a gamepad/joystick and translates it to a message that will be used by two SDC2130 controlled motors. Current configuration uses a PS3-Dualshock like controller. The gamepad node translates the gamepad message to a "gp_functions" message which the gamepad_listener node can listen to and manipulate it to send different commands to the SDC controller node. At the moment the gamepad_listener is redundant as it simply relays the message but as functionality is added to the robot it will become more important. The gpsim is a test node, which can be used to test keyboard input.

Currently supported : 2 movement spots for controlling the two motors' speed (analog sticks and D-pad) and 12 available function spots (buttons and analog stick when pushed in), without taking into consideration combined button presses.

To run :

    roscore
    rosrun joy joy_node
    rosrun gamepad_control gamepad / gpsim
    rosrun gamepad_control gamepad_listener

4) sdc2130

Description : A ROS wrapper for the Linux C++ API provided by Roboteq for its controllers. It issues movement commands to two motors controlled by and SDC2130. Currently provides a maximum speed of 200, with it being controlled by the analog sticks (the further the analog stick is pushed, the more the corresponding motor's speed is increased, with a maximum of 200) to simulate acceleration.

Supported Functions :
+ Independent Movement to the two motors via the analog sticks
+ Using the D-pad overrides the analog sticks enabling maximum speed forward and backwards movement as well as in place turns
+ Immediate Shutdown by pressing the Start Button
+ 5-Second Halt Using the O Button, during which all movement orders transmited via gamepad are ignored
+ Pressing the triangle button stops the robot, ignoring all movement orders, until triangle is pressed again
+ Basic Odometry Functionality : By pressing the X button odometry is initialized, setting the position of the vehicle at 0,0 and an angle of 0 degrees. From that point on, each time the X button is pressed, the vehicle's position is recorded in a text file named roboskel_log.txt located in the ~/.ros directory.

To run :

    roslaunch sdc2130 gremote.launch
