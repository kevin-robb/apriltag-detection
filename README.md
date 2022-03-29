# apriltag-detection

This repo details all that's necessary to detect AprilTags using an Intel RealSense D435 Depth Camera.

Setup:
 - First, install the ROS wrapper for the RealSense D435 depth camera to your system: `sudo apt-get install ros-$ROS_DISTRO-realsense2-camera`. Note: Using the standard usb_cam package did not work for this camera, and made all images display depth info as green, and nothing else.
 - Clone this repository, and ensure the `apriltag` and `apriltag_ros` submodules have their contents downloaded with the commands `git submodule init` and `git submodule update`.
 - In the workspace directory, run `catkin_make_isolated` to build the ROS workspace.
 - Set details of tags to search for in `tag_detection_pkg/config/tags.yaml`. We use the default tag family 36h11, but the specific IDs and real-world sizes of our tags must be specified under standalone_tags.
 - If the camera images aren't showing up, the `realsense-viewer` utility may be useful. This application starts an interface with the D435 camera that allows settings to be changed, firmware to be updated, and the RGB live feed to be previewed. If the camera feed doesn't show up, you likely need to install the proper drivers for your machine, or perform a firmware update on the camera.
 - The camera may need to be calibrated for apriltag detection.

Running it:
 - `roslaunch tag_detection_pkg tag_detection.launch` will startup the camera's ROS driver, the apriltag detection, and set all specified static tag transforms. This sets the camera's base tf frame to `camera_link`, and several ROS messages are published to topics beginning with "/camera/...". The default fixed frame in rviz is `map`, so we set this equal to the camera frame (for now). 
 - OPTIONAL: `rviz` to open rviz. Click "Add", select "By topic", and choose "/camera/color/image_raw" Camera to see the RGB image, and/or "/camera/depth/image_rect_raw" Camera and DepthCloud to see the image with depth information, and this depth projected on the 3D vizualizer, respectively.
 - OPTIONAL: `rosrun rqt_image_view rqt_image_view` opens an image viewer that allows the image topic to be selected from all available. This is an easy way to see detected tags overlaid on the camera feed by selecting the "/tag_detections/image" topic.
 - OPTIONAL: `rosrun tf tf_monitor` can help determine names and connections between published TF frames.

![A 3D DepthCloud shown in rviz.](kevin_is_a_pointcloud.png)