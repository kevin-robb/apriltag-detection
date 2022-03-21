Several launch files must be run to get apriltag detection working with the camera.

 - `roslaunch usb_cam usb_cam-test.launch` to run the camera ROS driver and start publishing its image feed to `/usb_cam/image_raw`. Set camera USB port in the launch file.
 - `roslaunch apriltag_ros continuous_detection.launch` to start apriltag detection on images being published to `/usb_cam/image_raw`. Set input topic(s) in the launch file, and set apriltag details in tags.yaml in apriltag_ros/config.
 - `rosrun rqt_image_view rqt_image_view` opens an image viewer that allows the image topic to be selected from all available.
 - `realsense-viewer` starts an interface with our Intel RealSense Depth Camera D435 in which settings can be changed, firmware can be updated, and the RGB video feed can be seen.