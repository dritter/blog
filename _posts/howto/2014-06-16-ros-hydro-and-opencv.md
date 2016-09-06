---
layout: post
title: ROS Hydro and OpenCV
category: How-To
tags: ros opencv program how-to
description: ros know how series
---

Tested on:

- ROS Hydro
- Ubuntu 12.04 Precise Pangoline
- Logicool c270h webcam

ROS supports many camera drivers which let us control the camera parameters like resolution, frame rate etc., and publish raw images for further processing by the code. Here, i will be using `uvc_camera` USB camera driver written by Ken Tossell.

We will:

1. Launch the `uvc_camera` driver to start publishing the images.
2. Subscribe to these images using image_transport
3. Convert the images from ROS image message format to OpenCV image format using `cv_bridge`
4. Process them using OpenCV commands
5. Convert the images from OpenCV image message format to ROS image message using `cv_bridge`
6. Publish the processed images using `image_transport`

Software for Testing Webcam
---------------------------

Before moving ahead, it is important to make sure whether your webcam works or not in linux. There are some open-source programs like:

1.  Cheese uses the gstreamer library, which utlilizes the video4linux2 API to capture video and stills from a webcam. It can also apply some special effects. Type the following to install it.

        sudo apt-get install cheese

2.	GUVCView is a graphical front-end for UVC drivers built using GTK+. It is way better than cheesefor controlling webcam and recording audio/video. Type the following to install.

        sudo apt-get install guvcview

3.  check image_view is installed by typing
        
        roscd image_view

    and install mjpegtools by

        sudo apt-get install mjpegtools

4.  To test the webcam,
open a terminal type dmesg click enter
after it stops type lsusb click enter
try the cam in by type in guvcview 



Install Camera Drivers to work with ROS
---------------------------------------

Open the terminal window, go to the directory where you would like to install the camera driver package. In my computer, I installed it in the home directory (go there by typing cd in the terminal window).
Install the package by typing:

    sudo apt-get install ros-hydro-camera-umd

or for groovy:
    
    ros-groovy-usb-cam

Once installed, type in the terminal:

    roscd uvc_Camera
    roscd usb_cam

If you are now in the uvc_camera directory, then the installation was successfull


Find which device is the camera connected to.
---------------------------------------------

1.  Open Terminal Window
2.  Disconnect the camera from the computer and type the following in the terminal:

        ls /dev/video*

    If you dont have any other cameras connected to your computer you would see no output, else you would see something like

        /dev/video0

    Remember the number of devices listed in this step.
3.	Now connect the camera to your computer and repeat step 2. You should see a new device added to the list like:

        /dev/video0

    So, the camera is connected to `/dev/video0`. We will used this information in the next section.


Create a new package for image processing
-----------------------------------------

> FOR GROOVY!! CHANGE `uvc_camera` into `usb_cam`

1.  Open a new terminal window and in the home directory, type the following:
	for rospack:
    
        roscreate-pkg tutorialROSOpenCV image_transport roscpp std_msgs opencv2 cv_bridge uvc_camera

    for catkin: (NOTE!!: no need to include opencv or opencv2 for catkin in groovy/hydro, because it is always embedded as stand-alone package)
    
        catkin_create_pkg tut_ros_opencv image_transport roscpp std_msgs cv_bridge uvc_camera

2.	We will now create a launch directory where we would store the file used to launch the `uvc_cameranode` in order for it to start publishing the images. Change directory:

        cd tutorialROSOpenCV

	Now make a new directory under it called launch:

        mkdir launch

	This is where we will store the launch file.

3.	Change directory:

        cd launch

	Create the new launch file by typing:

        subl uvcCameraLaunch.launch

    paste the following FOR HYDRO:

    ```xml
    <!--xml-->
    <launch>
      <node ns="camera" pkg="uvc_camera" type="uvc_camera_node" name="uvc_camera" output="screen">
        <param name="width" type="int" value="640" />
        <param name="height" type="int" value="480" />
        <param name="fps" type="int" value="30" />
        <param name="frame" type="string" value="webcam" />
        <param name="device" type="string" value="/dev/video0" />
      </node>
    </launch>
    ```

    PASTE THE FOLLOWING FOR GROOVY:

    ```xml
    <launch>
      <node name="usb_cam" pkg="usb_cam" type="usb_cam_node" output="screen" >
        <param name="video_device" value="/dev/video0" />
        <param name="image_width" value="640" />
        <param name="image_height" value="480" />
        <param name="pixel_format" value="mjpeg" />
        <param name="camera_frame_id" value="usb_cam" />
        <param name="io_method" value="mmap"/>
      </node>
      <node name="image_view" pkg="image_view" type="image_view" respawn="false" output="screen">
        <remap from="image" to="/usb_cam/image_raw"/>
        <param name="autosize" value="true" />
      </node>
    </launch>
    ```

	Save and exit. Notice the parameter device with value: `/dev/video0`. Change this to the actual device path. Refer to previous section.

4.	Before making this package you need to tell ROS where to find it. Gain root access in the terminal and type:

    ```sh
	cd
	subl .bashrc
    ```

	> !! WARNING!! ONLY FOR ROSPACK !!
	> A text editor should open up. Next add the following line at the end:
    > 
	> ```sh
    > export ROS_PACKAGE_PATH=~/tutorialROSOpenCV:$ROS_PACKAGE_PATH
	> ```

	Save and Exit the text editor.
	Restart the terminal, gain root access, and type:
	For Rospack:
	
    ```sh
    rosmake tutorialROSOpenCV
    ```

	For catkin:
	```sh
    catkin_make
    ```

	In the rosmake results you should notice:

    ```sh
	[ rosmake ] Results:
	[ rosmake ] Built 50 packages with 0 failures.
    ```

	If you notice some failures, you may not have root access.


Test the Launch script
-----------------------

In order to make sure that the package uvc_camera is in fact publishing the images, we will now run the node and check the output.

1.  In a new terminal type:

	For Rospack:
    ```sh
    roslaunch tutorialROSOpenCV uvcCameraLaunch.launch
    ```

    For catkin:
    ```sh
    roslaunch tut_ros_opencv uvcCameraLaunch.launch
    ```
    
    If your webcam has an integrated light indicator, you should see it light up.

2.  Now we will make sure that the images are being published. Open up another terminal window and type:

    ```sh
    rostopic list
    ```

    You should see the following topics being published:

    ```sh
    /camera/camera_info
    /camera/image_raw
    /camera/image_raw/compressed
    /camera/image_raw/compressed/parameter_descriptions
    /camera/image_raw/compressed/parameter_updates
    /camera/image_raw/theora
    /camera/image_raw/theora/parameter_descriptions
    /camera/image_raw/theora/parameter_updates
    /rosout
    /rosout_agg
    ```

3.	Lets look at the topic `/camera/image_raw`. Type:

    ```sh
	rosrun image_view image_view image:=/camera/image_raw
    ```

	You should see a new window pop-up with a continuous streaming video capture output of the webcam. Press <kbd>Ctrl</kbd>+<kbd>C</kbd> to exit. Lets look at the format of this topic. Type

    ```sh
	rostopic info /camera/image_raw
    ```

	You should see something like this:

    ```sh
    Type: sensor_msgs/Image

    Publishers:
     * /uvc_cam_node (http://username-computername:port/)

    Subscribers: None
    ```

	`sensor_msgs/Image` is a ROS image format which contains the header, height, width, step, and image data. Refer to: [http://www.ros.org/doc/api/sensor_msgs/html/msg/Image.html]() for more information.




4.	Lets look at the topic `/camera/camera_info`. Type:

	```sh
    rostopic info /camera/camera_info
    ```

	You should see something like this:

    ```sh
    Type: sensor_msgs/Image

    Publishers: 
     * /camera/uvc_camera (http://username-computername:port/)

    Subscribers: None
    ```

	`sensor_msgs/CameraInfo` is a ROS information format which contains the header, height, width, distortion model params, binning params and ROI (region of interest) params. Refer to: [http://www.ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html]() for more info.

    You can view the contents of this topic by typing:

    ```sh
	rostopic echo -c /camera/camera_info
    ```

Write the code for image processing
-----------------------------------

1.  In a new terminal window, type the following:
	For Rosbuild:
    
    ```sh
    roscd tutorialROSOpenCV/src
    ```

    For catkin:
    ```sh
    roscd tut_ros_opencv/src
    ```

    We will now create the source file which will contain the code. Type:

    ```sh
    subl main.cpp
    ```

    The following program inverts the colors of the image captured from the webcam. Paste the following code in the file:

    ```c++
    //Includes all the headers necessary to use the most common public pieces of the ROS system.
    #include <ros/ros.h>
    //Use image_transport for publishing and subscribing to images in ROS
    #include <image_transport/image_transport.h>
    //Use cv_bridge to convert between ROS and OpenCV Image formats
    #include <cv_bridge/cv_bridge.h>
    //Include some useful constants for image encoding. Refer to: http://www.ros.org/doc/api/sensor_msgs/html/namespacesensor__msgs_1_1image__encodings.html for more info.
    #include <sensor_msgs/image_encodings.h>
    //Include headers for OpenCV Image processing
    #include <opencv2/imgproc/imgproc.hpp>
    //Include headers for OpenCV GUI handling
    #include <opencv2/highgui/highgui.hpp>
     
    //Store all constants for image encodings in the enc namespace to be used later.
    namespace enc = sensor_msgs::image_encodings;
     
    //Declare a string with the name of the window that we will create using OpenCV where processed images will be displayed.
    static const char WINDOW[] = "Image Processed";
     
    //Use method of ImageTransport to create image publisher
    image_transport::Publisher pub;
     
    //This function is called everytime a new image is published
    void imageCallback(const sensor_msgs::ImageConstPtr& original_image)
    {
        //Convert from the ROS image message to a CvImage suitable for working with OpenCV for processing
        cv_bridge::CvImagePtr cv_ptr;
        try
        {
            //Always copy, returning a mutable CvImage
            //OpenCV expects color images to use BGR channel order.
            cv_ptr = cv_bridge::toCvCopy(original_image, enc::BGR8);
        }
        catch (cv_bridge::Exception& e)
        {
            //if there is an error during conversion, display it
            ROS_ERROR("tutorialROSOpenCV::main.cpp::cv_bridge exception: %s", e.what());
            return;
        }
     
        //Invert Image
        //Go through all the rows
        for(int i=0; i<cv_ptr->image.rows; i++)
        {
            //Go through all the columns
            for(int j=0; j<cv_ptr->image.cols; j++)
            {
                //Go through all the channels (b, g, r)
                for(int k=0; k<cv_ptr->image.channels(); k++)
                {
                    //Invert the image by subtracting image data from 255              
                    cv_ptr->image.data[i*cv_ptr->image.rows*4+j*3 + k] = 255-cv_ptr->image.data[i*cv_ptr->image.rows*4+j*3 + k];
                }
            }
        }
         
     
        //Display the image using OpenCV
        cv::imshow(WINDOW, cv_ptr->image);
        //Add some delay in miliseconds. The function only works if there is at least one HighGUI window created and the window is active. If there are several HighGUI windows, any of them can be active.
        cv::waitKey(3);
        /**
        * The publish() function is how you send messages. The parameter
        * is the message object. The type of this object must agree with the type
        * given as a template parameter to the advertise<>() call, as was done
        * in the constructor in main().
        */
        //Convert the CvImage to a ROS image message and publish it on the "camera/image_processed" topic.
            pub.publish(cv_ptr->toImageMsg());
    }
     
    /**
    * This tutorial demonstrates simple image conversion between ROS image message and OpenCV formats and image processing
    */
    int main(int argc, char **argv)
    {
        /**
        * The ros::init() function needs to see argc and argv so that it can perform
        * any ROS arguments and name remapping that were provided at the command line. For programmatic
        * remappings you can use a different version of init() which takes remappings
        * directly, but for most command-line programs, passing argc and argv is the easiest
        * way to do it.  The third argument to init() is the name of the node. Node names must be unique in a running system.
        * The name used here must be a base name, ie. it cannot have a / in it.
        * You must call one of the versions of ros::init() before using any other
        * part of the ROS system.
        */
            ros::init(argc, argv, "image_processor");
        /**
        * NodeHandle is the main access point to communications with the ROS system.
        * The first NodeHandle constructed will fully initialize this node, and the last
        * NodeHandle destructed will close down the node.
        */
            ros::NodeHandle nh;
        //Create an ImageTransport instance, initializing it with our NodeHandle.
            image_transport::ImageTransport it(nh);
        //OpenCV HighGUI call to create a display window on start-up.
        cv::namedWindow(WINDOW, CV_WINDOW_AUTOSIZE);
        /**
        * Subscribe to the "camera/image_raw" base topic. The actual ROS topic subscribed to depends on which transport is used.
        * In the default case, "raw" transport, the topic is in fact "camera/image_raw" with type sensor_msgs/Image. ROS will call
        * the "imageCallback" function whenever a new image arrives. The 2nd argument is the queue size.
        * subscribe() returns an image_transport::Subscriber object, that you must hold on to until you want to unsubscribe.
        * When the Subscriber object is destructed, it will automatically unsubscribe from the "camera/image_raw" base topic.
        */
            image_transport::Subscriber sub = it.subscribe("camera/image_raw", 1, imageCallback);
        //OpenCV HighGUI call to destroy a display window on shut-down.
        cv::destroyWindow(WINDOW);
        /**
        * The advertise() function is how you tell ROS that you want to
        * publish on a given topic name. This invokes a call to the ROS
        * master node, which keeps a registry of who is publishing and who
        * is subscribing. After this advertise() call is made, the master
        * node will notify anyone who is trying to subscribe to this topic name,
        * and they will in turn negotiate a peer-to-peer connection with this
        * node.  advertise() returns a Publisher object which allows you to
        * publish messages on that topic through a call to publish().  Once
        * all copies of the returned Publisher object are destroyed, the topic
        * will be automatically unadvertised.
        *
        * The second parameter to advertise() is the size of the message queue
        * used for publishing messages.  If messages are published more quickly
        * than we can send them, the number here specifies how many messages to
        * buffer up before throwing some away.
        */
            pub = it.advertise("camera/image_processed", 1);
        /**
        * In this application all user callbacks will be called from within the ros::spin() call.
        * ros::spin() will not return until the node has been shutdown, either through a call
        * to ros::shutdown() or a Ctrl-C.
        */
            ros::spin();
        //ROS_INFO is the replacement for printf/cout.
        ROS_INFO("tutorialROSOpenCV::main.cpp::No error.");
     
    }
    ```

    Save and Exit.

2.	Before we make the program, we have to edit the `CMakeLists.txt` file to ensure it will build and make an executable file of the program above. Gain root access, and type:
	For Rosbuild
	
    ```sh
    roscd tutorialROSOpenCV/
    ```

	For catkin
	```sh
    roscd tut_ros_opencv
    ```
	
    Then we will edit the CMakeLists file. Type:

	```sh
    subl CMakeLists.txt
    ```

    At the end of the file add the following line:

    ```sh
    rosbuild_add_executable(tutorialROSOpenCV src/main.cpp)
    ```

    For Catkin, uncomment:

    ```yaml
    include_directories(
      ${catkin_INCLUDE_DIRS}
      ${OpenCV_INCLUDE_DIRS}
    )
    ```

    and add:

    ```yaml
    add_executable(tut_ros_opencv_node src/main.cpp)
    target_link_libraries(tut_ros_opencv_node ${catkin_LIBRARIES} ${OpenCV_LIBRARIES} )
    add_dependencies(tut_ros_opencv_node tut_ros_opencv_generate_messages_cpp)
    ```

    Save and Exit.

3.	Now we can compile/make the package. Type:
	For Rosbuild:
    ```sh
	rosmake tutorialROSOpenCV
    ```

	For catkin:
	```sh
    catkin_make
    ```

    You should notice the following:

    ```sh
    [ rosmake ] Results:
    [ rosmake ] Built 50 packages with 0 failures.
    [ rosmake ] Summary output to directory
    ```

4.	Make sure that `roscore` is already running. If not, in the terminal type:

    ```sh
    roscore & 
    ```

    To run the project, type:
    For rosbuild:
    ```sh
    rosrun tutorialROSOpenCV tutorialROSOpenCV
    ```

    For catkin:
    ```sh
    rosrun tut_ros_opencv tut_ros_opencv
    ```

    You should see a window being created titled Image Processed containing the inverted image from the webcam


5.	In order to ensure that the processed image has been published as a rostopic, in a new terminal window type:

	```sh
    rostopic list
    ```

    You would see the following:

    ```sh
    /camera/camera_info
    /camera/image_processed
    /camera/image_processed/compressed
    /camera/image_processed/compressed/parameter_descriptions
    /camera/image_processed/compressed/parameter_updates
    /camera/image_processed/theora
    /camera/image_processed/theora/parameter_descriptions
    /camera/image_processed/theora/parameter_updates
    /camera/image_raw
    /camera/image_raw/compressed
    /camera/image_raw/compressed/parameter_descriptions
    /camera/image_raw/compressed/parameter_updates
    /camera/image_raw/theora
    /camera/image_raw/theora/parameter_descriptions
    /camera/image_raw/theora/parameter_updates
    /rosout
    /rosout_agg
    ```

    To check the image data in rostopic /camera/image_processed, type:

	```sh
    rosrun image_view image_view image:=/camera/image_processed
    ```

    You should see a new window pop-up with a continuous streaming video capture output of the webcam with image inverted. Press <kbd>Ctrl</kbd>+<kbd>C</kbd> to exit.
