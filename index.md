
# Welcome to My Portfolio!
All that has made me who I am as Engineer is highlighted here.

#### For your ease of perusing, I've listed my projects as follows:
[Camera-LIDAR Fusion and State Estimation of LIDAR](#Camera-LIDAR "Goto Camera-LIDAR Fusion and State Estimation of LIDAR")
* _Camera-LIDAR Fusion and State Estimation of LIDAR_
* _Point Cloud Processing on Cepton LIDAR_
* _Adaptive Cruise Control using GPS/GNSS, 2D LIDAR, and Camera_
* _Lane keeping & Obstacle Avoidance using the PixyCam and an Infrared Sensor_
* _Innovative Billboards Quarter Scale Prototype_


### Camera-LIDAR Fusion and State Estimation of LIDAR


<img src="/images/gazebo_simulation.png?raw=true" />



- - - -

### Point Cloud Processing on Cepton Vista 3D LIDAR

[![LIDAR Processing](https://res.cloudinary.com/marcomontalbano/image/upload/v1607592207/video_to_markdown/images/youtube--fvGX2Kw34n0-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=fvGX2Kw34n0 "LIDAR Processing")

The video above illustrates the successful results after processing the raw point cloud data coming from the Cepton Vista LIDAR to detect the cars in front of me. The algorithms were developed in C++ on ROS (Robot Operating System) and the results were visualized in Rviz.

Point cloud processing for 3D LIDARs is a huge deal as these sensors are data intensive, and can be very taxing on our processors if handled poorly. Additionally, the raw points coming from the LIDAR need to be processed in order to tune the performance based on the application, such as SLAM or Object Detection. 

The key steps are: Constraining the range of the point cloud, applying a Voxel Grid Filter to downsample the data, filtering out the normal vectors to exclude the ground, implementing Euclidean Clustering, and bounding the clustered objects. 

- - - -

### Adaptive Cruise Control using GPS/GNSS, 2D LIDAR, and Camera

[![Adaptive Cruise Control](https://res.cloudinary.com/marcomontalbano/image/upload/v1607909247/video_to_markdown/images/youtube--p0SfGsaEiwc-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/p0SfGsaEiwc "Adaptive Cruise Control")

The project that sparked a passion! As part of the introduction to ROS (Robot Operating System) course at Oakland University, my group undertook the task of developing an Adaptive Cruise Control system that used individual feedback of the seperation distance between the two Audibot vehicles from an array of GNSS/GPS, LIDAR, and Monocular Camera sensors that was fed to a PI Controller to safely slow down the following vehicle from 70 to 45 mph and effectively avoid collision with the oncoming blue Audibot, while maintaining a vehicle separation distance set by the driver.

<img src="/images/ACC_Audibot.png?raw=true" />

**GNSS/GPS-Based Cruise Control**: the system relied on the communication between the GPS modules that were placed on each vehicle, creating a Vehicle-to-Vehicle (V2V) communication. After extracting the Universal Transverse Mercator (UTM) coordinates of each vehicle, we used the Pythagorean theorem to calculate the relative distance between the vehicles and fed this distance as the input to our PI controller to adjust the red Audibot's speed.

**2D LiDAR-Based Cruise Control**: We simply extracted the positional data coming from the 2D LiDAR mounted on the red Audibot and used this distance in out PI controller to adjust the red Audibot's speed.

<img src="/images/ACC_juxtaposed_blob.png?raw=true" />

**Monocular Camera-Based Cruise Control**: We were able to take advantage of the _OpenCV_ library to perform _Simple Blob Detection_, as seen above, on the oncoming faced with the challenge of mapping the pixels to meters; however, we were faced with the challenge of determining distance based on pixels.. our solution was elegant and simple, using linear interpolation, we were able to map the distances from the 2D LiDAR to the Camera's pixels, and as a result, were able to use the same PI controller that we used on the previous systems and generate the same results!



- - - -

### Lane keeping & Obstacle Avoidance using the PixyCam and an Infrared Sensor



[![Mechatronic Car](https://res.cloudinary.com/marcomontalbano/image/upload/v1607640464/video_to_markdown/images/youtube--EgaXYLZe98o-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/EgaXYLZe98o "Mechatronic Car")

- - - -

Here 

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/slabban/slabban.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
