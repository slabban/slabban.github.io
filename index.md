<a name="TOP"></a>
# Welcome to My Portfolio!

## About Me

I'm a Mechatronics Engineer with demonstrated experience regarding the development of data processing, state estimation, and control algorithms for GPS/GNSS, LIDAR, Radar, Camera, and a variety of sensors that are used in current Autonomous and Advanced Drive Assistance Systems. In addition, I have a secondary focus on Electric Motor and PCB design. 
Accompanied with an undergraduate degree in Mechanical Engineering, my skills shine when bridging the multi-disciplinary gap between hardware and software through strong teamwork and effective communication and presentation skills.

At heart, my dream is to make the indivdual life safer and more efficient through vehicle autonomy and robotic applications with the end goal of creating a global mindset that targets sustainability and safety for our current and future generations.

All that has made me who I am as an Engineer is highlighted here.

#### For your ease of perusing, I've listed my projects as follows:


* [_Camera-LIDAR Sensor Fusion and State Estimation of LIDAR_](#Perception)

* [_Adaptive Cruise Control using GPS/GNSS, 2D LIDAR, and Camera_](#Audibot_ACC)

* [_Lane keeping & Obstacle Avoidance using the PixyCam and an Infrared Sensor_](#RCBOT)

* [_Innovative Billboards Quarter Scale Prototype_](#IBB)



- - - -
<a name="Perception"></a>


### Camera-LIDAR Sensor Fusion and State Estimation of LIDAR

[![Camera-LiDAR fusion](https://res.cloudinary.com/marcomontalbano/image/upload/v1607930316/video_to_markdown/images/youtube--EbhIny5wWd8-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=EbhIny5wWd8 "Camera-LiDAR fusion")

My latest work and magnum opus. The succesfull sensor fusion of the Monocular Camera with the State Estimated & processed data from the Cepton Vista 3D LiDAR!

A question that may come to mind is: what is sensor fusion and why is it important? To answer that, I would like to refresh on the meaning of the term Perception, as it is a commonly thrown around in autonomous sector. Perception is the ability to sense and interpret the surrounding environment in order to make, or wait to make, controlled and effective decisions, and the more information there is about the environment


<img src="/images/gazebo_simulation.png?raw=true" />



- - - -

### Point Cloud Processing on Cepton Vista 3D LIDAR

[![LIDAR Processing](https://res.cloudinary.com/marcomontalbano/image/upload/v1607592207/video_to_markdown/images/youtube--fvGX2Kw34n0-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=fvGX2Kw34n0 "LIDAR Processing")

The video above illustrates the successful results after processing the raw point cloud data coming from the Cepton Vista LIDAR to detect the cars in front of me. The algorithms were developed in C++ on ROS (Robot Operating System) and the results were visualized in Rviz.

Point cloud processing for 3D LIDARs is a huge deal as these sensors are data heavy, and can be very taxing on our processors if handled poorly. Additionally, the raw points coming from the LIDAR need to be processed in order to tune the performance based on the application, such as SLAM or Object Detection. 

The key steps are: Constraining the range of the point cloud, applying a Voxel Grid Filter to downsample the data, filtering out the normal vectors to exclude the ground, implementing Euclidean Clustering, and bounding the clustered objects. 

- - - -
<a name="Audibot_ACC"></a>


### Adaptive Cruise Control using GPS/GNSS, 2D LIDAR, and Camera 

![Adaptive Cruise Control](https://media.giphy.com/media/ylOb7MNaYR277JFtJW/giphy.gif)


The project that sparked a passion! As part of the introduction to ROS (Robot Operating System) course at Oakland University, my group undertook the task of developing an Adaptive Cruise Control system that used individual feedback of the seperation distance between the two Audibot vehicles from an array of GNSS/GPS, LIDAR, and Monocular Camera sensors that was fed to a PI Controller to safely slow down the following vehicle from 70 to 45 mph and effectively avoid collision with the oncoming blue Audibot, while maintaining a vehicle separation distance set by the driver.


<img src="/images/ACC_Audibot.png?raw=true" />


**GNSS/GPS-Based Cruise Control**: the system relied on the communication between the GPS modules that were placed on each vehicle, creating a Vehicle-to-Vehicle (V2V) communication. After extracting the Universal Transverse Mercator (UTM) coordinates of each vehicle, we used the Pythagorean theorem to calculate the relative distance between the vehicles and fed this distance as the input to our PI controller to adjust the red Audibot's speed.

**2D LiDAR-Based Cruise Control**: We simply extracted the positional data coming from the 2D LiDAR mounted on the red Audibot and used this distance in out PI controller to adjust the red Audibot's speed.

<img src="/images/ACC_juxtaposed_blob.png?raw=true" />


**Monocular Camera-Based Cruise Control**: We were able to take advantage of the _OpenCV_ library to perform _Simple Blob Detection_, as seen above, on the oncoming faced with the challenge of mapping the pixels to meters; however, we were faced with the challenge of determining distance based on pixels.. our solution was elegant and simple, using linear interpolation, we were able to map the distances from the 2D LiDAR to the Camera's pixels, and as a result, were able to use the same PI controller that we used on the previous systems and generate the same results!



- - - -
<a name="RCBOT"></a>


### Lane keeping & Obstacle Avoidance using the PixyCam and an Infrared Sensor



[![Mechatronic Car](https://res.cloudinary.com/marcomontalbano/image/upload/v1607640464/video_to_markdown/images/youtube--EgaXYLZe98o-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/EgaXYLZe98o "Mechatronic Car")



- - - -
<a name="IBB"></a>


### Innovative Billboards Quarter Scale Prototype




[Return to TOP](#TOP)
