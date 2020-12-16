<a name="TOP"></a>
# Welcome to My Portfolio!

## About Me

I'm a Mechatronics Engineer with demonstrated experience regarding the development of data processing, state estimation, and control algorithms for GPS/GNSS, LIDAR, Radar, Camera, and a variety of sensors that are used in current Autonomous and Advanced Drive Assistance Systems (ADAS). In addition, I have a secondary focus on Electric Motor and PCB design. 
Accompanied with an undergraduate degree in Mechanical Engineering, my skills shine when bridging the multi-disciplinary gap between hardware and software through strong teamwork and effective communication and presentation skills.

At heart, my dream is to make the indivdual life safer and more efficient through vehicle autonomy and robotic applications with the end goal of creating a global mindset that targets sustainability and safety for our current and future generations.

All that has made me who I am as an Engineer is highlighted here.

#### For your ease of perusing, I've listed my projects as follows:


* [_Camera-LIDAR Sensor Fusion and State Estimation of LiDAR_](#Perception)

* [_Point Cloud Processing on Cepton Vista 3D LIDAR_](#lidar)

* [_Adaptive Cruise Control using GPS/GNSS, 2D LIDAR, and Camera_](#Audibot_ACC)

* [_Lane keeping & Obstacle Avoidance using the PixyCam and an Infrared Sensor_](#RCBOT)

* [_Innovative Billboards LLC, Internship_](#IBB)



- - - -
<a name="Perception"></a>


### Camera-LiDAR Sensor Fusion and State Estimation of LiDAR


[![Camera-LiDAR fusion](https://res.cloudinary.com/marcomontalbano/image/upload/v1607930316/video_to_markdown/images/youtube--EbhIny5wWd8-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=EbhIny5wWd8 "Camera-LiDAR fusion")


My latest work and magnum opus! The succesfull sensor fusion of the Monocular Camera with the State Estimated & processed data from the Cepton Vista 3D LiDAR, with a focus on the detection of cars. The algorithms were developed using a combination of _C++_ and _Python_ on the _Robot Operating System (ROS)_ and the results were visualized in _Rviz_ using the Lincoln MKZ [_DATASPEED_](https://www.dataspeedinc.com/adas-by-wire-system/ "_DATASPEED_") autonomous vehicle.

A question that may come to mind is: what is sensor fusion and why is it important? To answer that, I would like to refresh on the meaning of the term _Perception_, as it is a commonly thrown around in autonomous sector. Perception is the ability to sense and interpret the surrounding environment in order to make, or wait to make, controlled and effective decisions. With greater quality and variety of information percieved from the environment, comes greater ability to make informed and smart decisions on how to react in that environment. That variety comes from different types of sensors that provide a variety of information, and if those two sensors can communicate well, then they can work together to allow a higher level of _Perception_ or _Awareness_.


<img src="/images/classified_object_img.png?raw=true" />


Back to the subject at hand, the Monocular Camera is a powerful and affordable sensor that allows the developers to use Computer Vision to classify objects in the streamed images; this was accomplished using a [YOLOv3](https://github.com/slabban/darknet_ros "YOLOv3") framework that was adopted for the Robot Operating System (ROS).

However, the Monocular Camera is poor in performance when it comes to deducing distances to objects, which leads into the next sensor..


<img src="/images/Lidar_ekf.png?raw=true" />


The 3D LiDAR has a higher price, but is an extremely powerful tool when it comes to detecting the position of objects in a 3D frame of reference, furthermore, using state estimation algorithms, specifically the Estimated Kalman Filter, it was possible to estimate the future position and relative velocity of each detected object at five times the original frequency, where the relative velocity to the vehicle was vizualized using the red arrows as seen in the image above.

However, this current make/model does have any object classification capabilities.

**The Fusion Strategy**


<img src="/images/IoU figure.png?raw=true" />


The key to bringing these two sensors together was simple yet effective mathmatical principle termed the _Jaccard Index_, or _Intersection Over Union (IoU)_ . The implementation is best illustrated above, where one rectangle represents the bounding box of the classified object from the Monocular Camera and the other rectangle comes from the 3D bounding box of the LiDAR which was projected as 2D pixels using Transformation and Image Geometry packages/libraries that are available to ROS. Intersected boxes with an IoU value of 50% or above can be percieved as cars.  

For more detailed information on Intersection over Union, click this [link](https://www.pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/ "IoU").


<img src="/images/Camera_LiDAR_IoU.png?raw=true" />


The image above drives the sensor fusion home, where the red rectangles in the left side of the figure above are the objects that have passed the IoU test of 50%, which are then filtered and re-published as can be seen on the right side of the figure above. 



- - - -
<a name="lidar"></a>


### Point Cloud Processing on Cepton Vista 3D LiDAR

[![LIDAR Processing](https://res.cloudinary.com/marcomontalbano/image/upload/v1607592207/video_to_markdown/images/youtube--fvGX2Kw34n0-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=fvGX2Kw34n0 "LIDAR Processing")


The video above illustrates the successful results after processing the raw point cloud data coming from the Cepton Vista LIDAR to detect the cars in front of me. The algorithms were developed using _C++_ and  on the _Robot Operating System (ROS)_  and the results were visualized in _Rviz_.

Point cloud processing for 3D LiDARs is a huge deal as these sensors are data heavy, and can be very taxing on our processors if handled poorly. Additionally, the raw points coming from the LiDAR need to be processed in order to tune the performance based on the application, such as SLAM or Object Detection. 

The key steps are: Constraining the range of the point cloud, applying a Voxel Grid Filter to downsample the data, filtering out the normal vectors to exclude the ground, implementing Euclidean Clustering, and bounding the clustered objects. 



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


### Lane keeping & Obstacle Avoidance using the PixyCam and an Infrared Sensor


[![Mechatronic Car](https://res.cloudinary.com/marcomontalbano/image/upload/v1607640464/video_to_markdown/images/youtube--EgaXYLZe98o-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/EgaXYLZe98o "Mechatronic Car")


Does a Master's degree in Mechatronics even count if you don't team up with an awesome group and create a really cool robot? Actually, it probably still does, but our team did it anyway.

This little fella was created for our Microcomputer-Based Control Systems course at Oakland University, where we successfully designed, simulated, and programmed it to perform Lane keeping, Obstacle Avoidance, and Adaptive Cruise Control (ACC) via sensor fusion of Computer Vision Systems of the _Pixy2 Smart Vision Sensor_ and an _Sharp GP2Y0A21YK Infrared Sensor_ and contolled by an _Arduino Uno_. 

My role on this project was broken down into two main roles:
1. Develop High level control implementation.
2. Enable Lane Tracking through experimenting with the _Pixy2_ and understanding the Application Programming Interface (API)
3. Develop the system dynamics of the vehicle on MATLAB and implement PID control to the motor to perform Adaptive Cruise Control

![RC_BOT](https://media.giphy.com/media/o8D44rIr8aQjwA1qTs/giphy.gif)


In the above video, you can see me just starting to get the hang of the _Pixy2_ line detection API, here the position of the line in pixel is being used to control the steering of the RC Car via a built in servo motor, notice the slow reposnse of the steering system..


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

The code block above represents the function that was written for the PID controller, this specific function controlled the duty cycle of the servo motor that would steer of the vehicle based on the , this approach led to a faster, smoother, and more refined response in the steering of the vehicle.


<img src="/images/Adaptive Cruise Control Picture2.png?raw=true" />


On to the simulation portion of the project. With access the powerful features of _MATLAB_ and _Simulink_, I was able to create a system that used digitally filtered feedback from the Sharp IR Sensor to sense oncoming objects and deploy a PID control strategy that was facilitated by an Arduino microcontroller to slow down our mechatronic RC Car. Don't let the images fool you, while the system may look trivial, each of these blocks comprises of complex subsystems and subfunctions that were used to develop the plant dynamics, sensor input with a low-pass filtration, and PID controlled Pulse Width Modulation (PWM) to control the car's motor speed.


<img src="/images/filtered_ultrasonic.jpg?raw=true" />


An interesting avenue explored during the initial stages of this project was the use of Ultrasonic Sensors to perform obstacle avoidance, specifically the implementation of a [digital low-pass filter](https://youtu.be/KzdsOhwVtms?t=496 "Digital Filtration Methods"). Ultrasonic sensors are notorious for their high levels of noise, which can lead to unwanted spikes and false positive readings as seen in the red curve in the graph above. This accuracy and performance of this sensor was improved significantly through using a digtal low-pass filter, as shown in the blue curve.



- - - -
<a name="IBB"></a>


### Innovative Billboards LLC, Internship


[![IBB_Quarter_Scale](https://res.cloudinary.com/marcomontalbano/image/upload/v1608022524/video_to_markdown/images/youtube--Y56XGTr2FhU-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=Y56XGTr2FhU&feature=youtu.be "IBB_Quarter_Scale")


This experience deserves a higher slot in my portfolio as it has been instrumental to my foundation as a professional and an engineer; however, due to a signed NDA, I will just use this section to reflect on my achievements as a Procurement & Controls Engineer Intern. 

**Procurement Engineer**

I initally began my journey at Innovative Billboards as a Procurment Engineer Intern, where I was tasked with locating and contacting vendors locally and overseas to form long term relationships and purchase a variety of mechanical and electrical products that were needed for the Billboard in a Box quarter scale prototype shown in the video above, ranging from steel tubes and acrylic panels all the way to a single phase step down transformer. 
I quickly established myself in this role due to my ability to communicate clearly and concisely to my colleagues and suppliers while quickly mastering each product's properties and standards to guide the project towards economoic and robust solutions; essentially, I was responsible for every purchase that made the prototype successful and played a primary role in managing the logistics of delivering the prototype to Innovative Billboards' local facility.


<img src="/images/ibb_motorwork.png?raw=true" />


Pressure forms diamonds, and we were under a lot of pressure, with two weeks to prepare for our initial investor meeting, we had to transform the structural skeleton of the billboard into the the electo-mechanical product seen in the video above. I took charge of routing and harnessing High-Voltage breaker box, Delta motor drives, ABB AC induction motors and a Low-Voltage box comprising of a Beckhoff Programmable Logic (PLC), Safety Lights, and Stop/Start Button to control the system of the billboard prototype, the picture above provides a little insight into that successful experience.


**Controls Engineer**

When I first joined Innovative Billboards, I had big aspirations to become learn the trade of a controls engineer through surrounding myself with distinguished professors and consultants with over 20 years of experience in the field of controls, and when Summer 2020 came around, I had the golden opportunity to apply myself as a Controls Engineer Intern. 
https://www.linkedin.com/in/bill-young-8a2aa91/
Having gained substantial experience from my work on the prototype, and coupled with the vast knowledge on sensors and control system design gained throughout my Mechatronics degree, I took the heavy task of coordinating with numerous automation firms overseas to develop and draft an 80 page document on the entire control system of the Full Scale Billboard. Additionally, I had generated a detailed Instrument I/O list for the Billboard and chose a tailored PLC solution for the system.

The next line of achievements was motor selection and simulation, taking a deep dive into Electric Motor literature and having worked with seasoned [Bill Young](https://www.linkedin.com/in/bill-young-8a2aa91/ "Bill Young") and [Dr. Ka C. Cheok](https://oakland.edu/secs/directory/cheok "Dr. Ka C. Cheok"), I was able to simulate the Billboard's scrolling mechanism on MATLAB/Simulink using the _Linear-quadratic regulator (LQR)_ and PID control strategies. Plotting and comparing the speed-torque curves of the simulation and the manufacturer in order to select the most suitable motors and gear reduction that would reduce motor cost and [Inertia Mismatch](https://www.motioncontrolonline.org/content-detail.cfm/Motion-Control-News/Understanding-the-Mysteries-of-Inertia-Mismatch/content_id/404 "Inertia Mismatch"). 

I look back fondly on my memories working for Innovative Billboards LLC, and the great experiences long-lasting relationships that I have built.

[Return to TOP](#TOP)
