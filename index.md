<a name="TOP"></a>
# Welcome to My Portfolio!

## About Me

I'm a Senior Software Engineer with demonstrated experience in the architecture, development, and testing of Perception and Localization systems for Autonomous and Advanced Drive Assistance Systems (ADAS). 

As a roboticist I wear many hats, namely with Embedded Systems, Electric Motors, and Circuit Design.

At heart, my dream is to make our lives safer and cleaner through staying on top of the latest developments in the Robotics and AI fields so that I can inspire and teach those in my network.

My end goal is to play a key part in contributing to the global mindset that targets sustainability and safety for our current and future generations.

All that has made me who I am as an Engineer is highlighted here.

#### For your ease of perusing, I've listed my projects as follows:

* [_Pytorch, Multi-Task Learning, Tracing, and Deployment in ROS2_](#MTL)

* [_Multiple Object Tracking Using YOLO_](#YoloMOT)

* [_Camera-LiDAR Sensor Fusion and State Estimation of LiDAR_](#Perception)

* [_Autonomous Vehicles Club (Smart Vehicles Club)_](#SVC)

* [_Adaptive Cruise Control using GPS/GNSS, 2D LiDAR, and Camera_](#Audibot_ACC)

* [_Lane keeping & Collision Avoidance - Robot Car_](#RCBOT)

* [_Innovative Billboards LLC, Internship_](#IBB)

- - - -
<a name="MTL"></a>

### Pytorch, Multi-Task Learning, Tracing, and Deployment in ROS2

[![hydranet_ROS2](https://res.cloudinary.com/marcomontalbano/image/upload/v1667016333/video_to_markdown/images/youtube--7NW-bPTts8U-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=7NW-bPTts8U "hydranet_ROS2")

The video above illustrates depth and semantic segmentation inferences from a hydranet model that is industrialized and ported to C++ to perform inferencing using the ROS2 middleware. The image stream is playback data from a recording taken while driving around the Oakland University Campus.

By the time I had picked this project up in April 2022, I had accumulated a good breadth of knowledge in the robotics industry in my academic years and that knowledge was heavily accelerated with my current career as a Software Engineer at Accenture. Though I lacked expertise on a huge piece of the self driving puzzle: **Deep Learning**.

Granted, it's quite easy to deploy an existing ROS package that some wonderful soul has created and enjoy the results, heck, that's all I knew how to do. 

Though eventually, you will run into the same roadblocks as I did:

1. How do I understand these crazy deep learning papers that are coming out?! I coudln't even get past the abstract without scratching my head.
2. I had no idea how to integrate a new state-of-the-art model in my system.
3. I didn't know how to correctly prepare my dataset and train the model to fit my use case.
4. The model may not be performant with my current system. How can I accelerate that performance or viably select a better alternative? Perhaps a traditional methodology was my best bet all along?

Knowing how to address these points is a big deal, it means that your foot is in the door and that you are enabled in the field of deep learning. 

My deep learning journey started in the summer of 2021 with two amazing (and free) resources: fastai's [Practical Deep Learning for Coders](https://course.fast.ai/) and Deep Lizard's [Deep Learning Fundamentals](https://youtube.com/playlist?list=PLZbbT5o_s2xq7LwI2y8_QtvuXZedL6tQU) and [Pytorch-Python Deep Learning Neural Network API](https://youtube.com/playlist?list=PLZbbT5o_s2xrfNyHZsM6ufI0iZENK9xgG). These courses taught me the fundamentals of machine leanrning and deep learning and I would happily recommend them to those who are eager to get the ball rolling and motivated to go at their own pace.

Having been equipped with the essential concepts of machine learning, I was ready to move on to my chosen specialized field of _Computer Vision_. Jeremy Cohen's [Think Autonomous](https://courses.thinkautonomous.ai/) was my immediate choice for that. I had come across Jeremy's blog a number of times and had gained so much insight from him that it was basically a no-brainer at that point, so I enrolled in his Hydranet course, which focused on studying and training the popular multi-task learner concepts that were implemented in this paper: https://arxiv.org/abs/1809.04766. 

My initial plan when I enrolled in Jeremy's course was to integrate the Hydranet into ROS2. That way I would pick up ROS2 and Deep Learning at the same time. So I had picked up ROS2 while taking that course.

While planning the integration out, I came across the concept of industrialization in machine learning, which focuses on elevating a trained model from _eager mode_ to _producton mode_. Pytorch provided **Pytorch JIT** and **Libtorch**, which respectively give tracing/scripting capabilities to the model and a C++ API that enable further optimization to the model. I decided to adopt that as part of the integration knowing that this would add an extra layer of effort that came with C++, but that's the language of robotics, and I wanted to do it right.

I traced the model and deployed it in a ros node that would prepare the image coming in from the camera, pass the image into the network for inferencing, and advertise the depth and segmentation outputs. 

As of now, the repository for that project is private as I am currently evaluating a use case for it. Though I did create a [template repository](https://github.com/slabban/ros2_pytorch_cuda) for using Libtorch in ROS2 and have included a dockerized CUDA environment for a simpler setup.


- - - -
<a name="YoloMOT"></a>

### Multiple Object Tracking with YOLOv3

[![YOLO MOT](https://res.cloudinary.com/marcomontalbano/image/upload/v1649134272/video_to_markdown/images/youtube--ru_O9tgi5M4-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=ru_O9tgi5M4 "YOLO MOT")

This project was a classical approach to Multi-Object Tracking (MOT) using the popular Extended Kalman Filter (EKF) and an Intersection Over Union (IoU) association algorithm within the Robot Operating System (ROS) Middleware.

My inspiration to take on this project came from this [article](https://thinkautonomous.medium.com/computer-vision-for-tracking-8220759eee85) that Jeremy Cohen had written. I had come across it over a year ago and thought to myself: "I know how to design a Kalman Filter and have worked on Multiple Object Tracking, I should give this a shot", and so I did!

The fun part is I was able to try my algorithm on both the YOLOv3 and YOLOv4 and compare the results as seen in the video above. Overall YOLOv4 performed better with association since it was able to consistently detect and classify objects, but YOLOv3 was able to perform the detections at a quicker rate, and hence, produce smoother estimates. Using my current system, I was getting an detection output rate of 17 HZ, and was able to push the estimate rate to 50 HZ (0.02 seconds) for YOLOv3. The YOLOV4 model architecture is more complex, which really impacted the detection rate, bringing it down to ~7.5 HZ, after some experimentation I found that a estimate rate of 25 HZ (0.04 seconds) to an OK number. But as you can see, the image quality being fed to the detector isn't all that great, so I'd be curious to compare the performance with a better quality input that has been intrinsically calibrated.

My algorithm, and most MOTs, can be broken down into 5 steps:
1. Detection
2. Association
3. Track Identity Creation
4. Estimation
5. Track Identity Destruction
   
My methodolgy has a few drawbacks that generally apply to these classical approaches, namely loss of tracking through ID swaps and object occlusion. Using the famous Hungarian Algorithm for association paired with the EKF is known as **SORT**, and may help reduce the frequency of ID swaps and improve the overall effciency, since that algorithm uses a linear assignment strategy; whereas my current approach associates using a 'first come first serve' method. But a better method is called **Deepsort**, which leverages feature maps from the RCNN for association. Deepsort elegantly solves the ID Swap and Occlusion problem, and is built on **SORT** and the classical approach that I took. You can get the full scoop on this [here](https://medium.com/augmented-startups/deepsort-deep-learning-applied-to-object-tracking-924f59f99104).

While my algorithm is not state of the art, I am extremely proud of this project. I've learnt so much from the open source community and would like to get to a point where I can give back with well documented and readable code. This is my first step in that direction [Github link here](https://github.com/slabban/yolo_tracking).

- - - -
<a name="Perception"></a>


### Camera-LiDAR Sensor Fusion and State Estimation of LiDAR


[![Camera-LiDAR fusion](https://res.cloudinary.com/marcomontalbano/image/upload/v1607930316/video_to_markdown/images/youtube--EbhIny5wWd8-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=EbhIny5wWd8 "Camera-LiDAR fusion")


Successful sensor fusion of the Mobileye Monocular Camera with the state estimated & processed data from the Cepton Vista 3D LiDAR, with a focus on the detection of cars. 
These algorithms were developed using a combination of _C++_ and _Python_ on the _Robot Operating System (ROS)_ and the results were visualized in _Rviz_ using the Lincoln MKZ [_DATASPEED_](https://www.dataspeedinc.com/adas-by-wire-system/ "_DATASPEED_") autonomous vehicle provided by [Dr. Micho Radovnikovich](https://www.linkedin.com/in/micho-radovnikovich-ph-d-186820b/ "Dr. Micho Radovnikovich").

A question that may come to mind is: what is sensor fusion and why is it important? To answer that, I would like to refresh on the meaning of the term _Perception_, as it is a commonly thrown around in autonomous sector. Perception is the ability to sense and interpret the surrounding environment in order to make, or prepare to make, controlled and effective decisions. With greater quality and variety of information percieved from the environment, comes greater ability to make informed and smart decisions on how to react in that environment. That variety comes from different types of sensors that provide a variety of information, and if those two sensors can communicate well, then they can work together to allow a higher level of _Perception_ or _Awareness_.


<img src="/images/classified_object_img.png?raw=true" />


Back to the subject at hand, the Monocular Camera is a powerful and affordable sensor that allows the developers to use Computer Vision to classify objects in the streamed images; this was accomplished using a [YOLOv3](https://github.com/slabban/darknet_ros "YOLOv3") framework that was adopted for the Robot Operating System (ROS).


<img src="/images/Lidar_ekf.png?raw=true" />


The 3D LiDAR is quite expensive relative to monocular cameras, but is an extremely powerful tool when it comes to detecting the position of objects in a 3D frame of reference as a raw pointcloud input, furthermore, using state estimation algorithms, the Estimated Kalman Filter in this case, it wis possible to estimate the future position and relative velocity of each detected object at five times the original frequency, where the relative velocity to the vehicle is vizualized using the red arrows as seen in the image above.


**The Fusion Strategy**


<img src="/images/IoU figure.png?raw=true" />


The key to bringing these two sensors together was simple yet effective mathematical principle termed the _Jaccard Index_, or _Intersection Over Union (IoU)_ . The implementation is best illustrated above, where one rectangle represents the bounding box of the classified object from the Monocular Camera and the other rectangle comes from the 3D bounding box of the LiDAR which was projected as 2D pixels using Transformation and Image Geometry packages/libraries that are available to ROS. Intersected boxes with an IoU value of 50% or above can be percieved as cars.  

For more detailed information on Intersection over Union, click this [link](https://www.pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/ "IoU").


<img src="/images/Camera_LiDAR_IoU.png?raw=true" />


The image above drives the sensor fusion home, where the red rectangles in the left side of the figure above are the objects that have passed the IoU test of 50%, which are then filtered and re-published as can be seen on the right side of the figure above. 



- - - -
<a name="SVC"></a>


### Autonomous Vehicles Club (Smart Vehicles Club)


[![GEM_rundown](https://res.cloudinary.com/marcomontalbano/image/upload/v1608106627/video_to_markdown/images/youtube--k2_-BM4CIBk-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=k2_-BM4CIBk "GEM_rundown")


Early into my masters program, I realized that I had a passion for autonomous systems and robotics, but I did not know the first thing about them, that all changed when I became an active member of the Smart Vehicle Club (Autonomous Vehicle Club) in 2019. 
Led by [John Brooks](https://www.linkedin.com/in/jbrooks47/ "John Brooks") that year, our team had accomplished the phenomenal goal of developing the Drive-By-Wire system of the Polaris GEM vehicle, as demonstrated in the video clip above. 


<img src="/images/PCB.png?raw=true" />


A large part of our experience at the club was electric circuit prototyping and Printed Circuit Board (PCB) Design. Part of our goal for that year was clean and well documented designs, which involved efficient and replicable circuits; and thus, we introduced the concept of the PCB as a logical solution.
The PCB seen in the image above is recognized as a _Digital Signal Processing Board_, which plays the important role of conditioning signals going to and from the microcontroller to ensure that the board is communicating with the system and vice versa. Examples of sub-circuits in this board are Digital to Analog Converters (DACs) and Voltage Dividers.


[![LIDAR Processing](https://res.cloudinary.com/marcomontalbano/image/upload/v1607592207/video_to_markdown/images/youtube--fvGX2Kw34n0-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=fvGX2Kw34n0 "LIDAR Processing")


The following year, I had become the new President of the club, and with that, I had the responsibility of carrying on the great work that was accomplished in the previous year, I made sure to start that off on a high note.

The video above illustrates the successful results after processing the raw point cloud data coming from the Cepton Vista LiDAR to detect the cars in front of me. The algorithms were developed using the _Point Cloud Library (PCL)_ in _C++_ and realized in the _Robot Operating System (ROS)_ The results were visualized in _Rviz_.

Point cloud processing for 3D LiDARs is a huge deal as these sensors are data heavy, and can be very taxing on our processors if handled poorly. Additionally, the raw points coming from the LiDAR need to be processed in order to tune the performance based on the application, such as SLAM or object segementation. 

The key steps are: Constraining the range of the point cloud, applying a Voxel Grid Filter to downsample the data, filtering out the normal vectors to exclude the ground, implementing Euclidean Clustering, and bounding the clustered objects. 


<img src="/images/Camera_Calibration.png?raw=true" />


Monocular and Stereo Cameras are prevalent in the world of Autonomous Vehicles due to the awesome ability to pair them with computer vision systems that open the doors to object classification and geometric estimation. Naturally, we saw fit to include cameras on our vehicle.

The picture above illustrates my successfull efforts to calibrate the intrinsic properties of the _Logitech C920 Pro Webcam_ using the popular checkerboard approach. Intrinsic calibration is extremely important, as it detemines and accounts for the distortion, focal length, and image center parameters that are unique for each camera model. This allowed us to perform accurate geometric operations such as lane detection and projection of LiDAR objects into the camera's frame of reference for sensor fusion.

[![SVC Simulation](https://res.cloudinary.com/marcomontalbano/image/upload/v1649037959/video_to_markdown/images/youtube--G2TDP7dRkh0-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/G2TDP7dRkh0 "SVC Simulation")

The culmination of my contribution to the team was our first **official driving agent**. The video above illustrates our vehicle performing lane following, obstacle detection, and lane maneuvering within the simulated Gazebo environment. Here I played lead roles in ROS integration, Perception, Localization, and Systems Architecure. Taking in the simulated raw data from the GPS, Lidar, Camera, and Vehicle Speed and setting up the complete pipeline comprising of my camera-lidar segmentation & fusion algorithm, vehicle heading state estimation, and [Ali Irshayyid's](https://www.linkedin.com/in/ali-irshayyid-967378127/) control algorithm to successfully complete test F7 of the IGVC competition. The cool part is, this driving agent *impelementation independent*, which means that the entire agent can be ported on to the physical vehicle and should perform closely to the simulation with some system tuning!

<img src="/images/SVC_Perception.png?raw=true" />

The picture above is a close view of the output from obstacle detection portion of my perception pipeline using my camera-LiDAR fusion strategy outlined [here](#Perception). Each object of interest is is uniquely classified and tracked by it's uniquely numbered 3D Box. This valuable information allowed us to extract the distance of each object from the vehicle and subsequently perfom the adequate maneuvers to pass the test.

My last contribution to the team was the containerization of driving agent for both the real and simulated system using Docker. This allowed us to contribute and deploy the system across multiple machines with no discrepancies!

With no exaggeration, my time at the Smart Vehicle Club was an experience that shaped my career and personal life for the better and landed me the job and passion that I have today and will carry for a long time.



- - - -
<a name="Audibot_ACC"></a>


### Adaptive Cruise Control using GPS/GNSS, 2D LIDAR, and Camera 

![Adaptive Cruise Control](https://media.giphy.com/media/ylOb7MNaYR277JFtJW/giphy.gif)


The project that sparked a passion! As part of the introduction to the _Robot Operating System (ROS)_ course at Oakland University, my group undertook the task of developing an Adaptive Cruise Control (ACC) system that used feedback of the seperation distance between the two Audibot vehicles from an array of GNSS/GPS, LiDAR, and Monocular Camera sensors that was fed to a PI Controller to safely slow down the following vehicle from 70 to 45 mph and effectively avoid collision with the oncoming blue Audibot, while maintaining a vehicle separation distance set by the driver.


<img src="/images/ACC_Audibot.png?raw=true" />


**GNSS/GPS-Based Cruise Control**: The system relied on the communication between the GPS modules that were placed on each vehicle, creating a Vehicle-to-Vehicle (V2V) communication. After extracting the Universal Transverse Mercator (UTM) coordinates of each vehicle, we used the Pythagorean theorem to calculate the relative distance between the vehicles and feed this distance as the input to our PI controller to adjust the red Audibot's speed.

**2D LiDAR-Based Cruise Control**: We simply extracted the positional data coming from the 2D LiDAR mounted on the red Audibot and used this distance in our PI controller to adjust the red Audibot's speed.


<img src="/images/ACC_juxtaposed_blob.png?raw=true" />


**Monocular Camera-Based Cruise Control**: We were able to take advantage of the _OpenCV_ library to perform _Simple Blob Detection_, on the oncoming vehicle. However, we were faced with the challenge of determining the seperation distance based on pixels.. our solution was elegant and simple, using linear interpolation, we were able to map the distances from the 2D LiDAR to the Camera's pixels, and as a result, were able to use the same PI controller that we used on the previous systems and generate the same results!



- - - -
<a name="RCBOT"></a>


### Lane keeping & Collision Avoidance - Robot Car


[![Mechatronic Car](https://res.cloudinary.com/marcomontalbano/image/upload/v1607640464/video_to_markdown/images/youtube--EgaXYLZe98o-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/EgaXYLZe98o "Mechatronic Car")


Does a Master's degree in Mechatronics even count if you don't team up with an awesome group and create a really cool robot? Yes it does, but our team did it anyway.

This little fella was created for our Microcomputer-Based Control Systems course at Oakland University, where we successfully designed, simulated, and programmed it to perform Lane keeping, Collision Avoidance, and Adaptive Cruise Control (ACC) via sensor fusion of Computer Vision Systems of the _Pixy2 Smart Vision Sensor_ and a _Sharp GP2Y0A21YK Infrared Sensor_ that were contolled by an _Arduino Uno_ ECU. 

My role on this project was broken down into 3 main roles:
1. Develop High level control implementation.
2. Enable Lane Tracking through experimenting with the _Pixy2_ and understanding the Application Programming Interface (API).
3. Develop the system dynamics of the vehicle on MATLAB/Simulink and implement PID control to the motor for smooth Adaptive Cruise Control performance.

![RC_BOT](https://media.giphy.com/media/o8D44rIr8aQjwA1qTs/giphy.gif)


In the above video, you can see me just starting to get the hang of the _Pixy2_ line detection API, here the position of the line in pixel is being used to control the steering of the RC Car via a built in servo motor, notice the slow repsonse from the steering system..


```javascript
// PID Controller function for Steering 
float PID_Controller_steer(float Kp, float Ki, float Kd, float r_value_steer, float y_value_steer) 
{ 
  float error_integ_steer; 
  float error_derv_steer; 
  float e_prev_steer; 
  float u_value_steer; 
  float deltaT = 0.01; 
  float error_steer = r_value_steer - y_value_steer; 
  error_integ_steer = error_integ_steer + error_steer*deltaT; 
  error_derv_steer = (error_steer - e_prev_steer)/deltaT; 
  e_prev_steer = error_steer; 
  u_value_steer = Kp*error_steer + Ki*error_integ_steer + Kd*error_derv_steer; 
  return(u_value_steer); 
}
```

The code block above represents the function that was written for the PID controller, this specific function controlled the duty cycle of the servo motor that would steer the vehicle based on the pixel coordinates of the line, this approach led to a faster, smoother, and more refined response in the steering of the vehicle.


<img src="/images/Adaptive Cruise Control Picture2.png?raw=true" />


On to the simulation portion of the project. With access to the powerful features of MATLAB/Simulink, I was able to create a system that used digitally filtered feedback from the Sharp IR Sensor to sense oncoming objects and deploy a PID control strategy that was facilitated by an Arduino microcontroller to slow down our mechatronic RC Car. Don't let the images fool you, while the system may look trivial, each of these blocks comprises of complex subsystems and subfunctions that were used to develop the plant dynamics, sensor input with a low-pass filtration, and PID controlled Pulse Width Modulation (PWM) to control the car's motor speed.


<img src="/images/filtered_ultrasonic.jpg?raw=true" />


An interesting avenue explored during the initial stages of this project was the use of Ultrasonic Sensors to perform Obstacle Avoidance, specifically the implementation of a [digital low-pass filter](https://youtu.be/KzdsOhwVtms?t=496 "Digital Filtration Methods"). Ultrasonic sensors are notorious for their high levels of noise, which can lead to unwanted spikes and false positive readings as seen in the red curve in the graph above. The accuracy and performance of this sensor was improved significantly through using a digital low-pass filter. The significant effects of this approach can be seen when comparing the filtered output in the blue curve with the unfiltered output in the red curve.



- - - -
<a name="IBB"></a>


### Innovative Billboards LLC, Internship


[![IBB_Quarter_Scale](https://res.cloudinary.com/marcomontalbano/image/upload/v1608022524/video_to_markdown/images/youtube--Y56XGTr2FhU-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=Y56XGTr2FhU&feature=youtu.be "IBB_Quarter_Scale")


This experience deserves a higher slot in my portfolio as it has been instrumental to my foundation as a professional and an engineer; however, due to a signed NDA, I will just use this section to reflect on my achievements as a Procurement & Controls Engineer Intern. 

**Procurement Engineer**

I initally began my journey at Innovative Billboards as a Procurement Engineer Intern, where I was tasked with locating and contacting vendors locally and overseas to form long term relationships and purchase a variety of mechanical and electrical products that were needed for the Billboard in a Box quarter scale prototype shown in the video above, ranging from steel tubes and acrylic panels all the way to a single phase step down transformer. 
I quickly established myself in this role due to my ability to communicate clearly and concisely to my colleagues and suppliers while quickly mastering each product's properties and standards to guide the project towards economoic and robust solutions; essentially, I was responsible for every purchase that made the prototype successful and played a primary role in managing the logistics of delivering the prototype to Innovative Billboards' local facility.


<img src="/images/ibb_motorwork.png?raw=true" />


Pressure forms diamonds, and we were under a lot of pressure, with two weeks to prepare for our initial investor meeting, we had to transform the structural skeleton of the billboard into the the electo-mechanical product seen in the video above. I took charge of routing and harnessing High-Voltage breaker box, Delta motor drives, ABB AC induction motors and a Low-Voltage box comprising of a Beckhoff Programmable Logic (PLC), Safety Lights, and Stop/Start Button to control the system of the billboard prototype, the picture above provides a little insight into that successful experience.


**Controls Engineer**

When I first joined Innovative Billboards, I had big aspirations to learn the trade of a controls engineer through surrounding myself with distinguished professors and consultants with over 20 years of experience in the field of controls, and when Summer 2020 came around, I had the golden opportunity to apply myself as a Controls Engineer Intern. 

Having gained substantial experience from my work on the prototype, and coupled with the vast knowledge on sensors and control system design gained throughout my Mechatronics degree, I undertook the heavy task of coordinating with numerous automation firms overseas to develop and draft an 80 page document on the entire control system of the Full Scale Billboard. Additionally, I had generated a detailed Instrument I/O list for the Billboard and communicated with vendors to select a tailored PLC solution for the system.

The next line of achievements was motor selection and simulation, taking a deep dive into Electric Motor literature and having worked with seasoned professionals [Bill Young](https://www.linkedin.com/in/bill-young-8a2aa91/ "Bill Young") and [Dr. Ka C. Cheok](https://oakland.edu/secs/directory/cheok "Dr. Ka C. Cheok"), I was able to simulate the Billboard's scrolling mechanism on MATLAB/Simulink using the _Linear-quadratic regulator (LQR)_ and PID control strategies. Plotting and comparing the speed-torque curves of the simulation with those of the manufacturer in order to select the most suitable motors and gear reduction that would reduce motor cost and [Inertia Mismatch](https://www.motioncontrolonline.org/content-detail.cfm/Motion-Control-News/Understanding-the-Mysteries-of-Inertia-Mismatch/content_id/404 "Inertia Mismatch"). 

I look back fondly on my memories working for Innovative Billboards LLC, and the great experiences long-lasting relationships that I have built.

[Return to TOP](#TOP)
