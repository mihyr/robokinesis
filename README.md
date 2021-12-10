# Robokinesis 

A wearable device for controlling any ROS based Robot 

Overview: 

Robokinesis is a low-cost wearable device that has the potential to control or interact with any ROS-based mobile robots and manipulators. 

The idea: 

The core goal was to develop a ROS package that can be used on any sensor integrated hardware.  

The Robokinesis ROS package maps the raw sensor data to user-defined ROS topics onboard and streams it directly to the robot at the desired frequency, without any middle agent. 

Motivation: Modularity 

Any RTOS hardware, Any sensors, Any ROS based robot  

User-Defined number of sensor inputs, User-Defined number of mapped ROS topics 

Is this device one of its kind? 

No, it's not! It’s a budget alternative. High-end wearables for controlling ROS-based robots exist, especially used in Human-robot interaction research.  But its ROS packages and SDKs are tightly coupled with its hardware that the package can't be used on low-cost alternatives or in combination with other open-source ROS packages.  

Target Audience 

Robotics Students or enthusiasts who want to test or fast prototype a wearable, control their robot. 

Robotics Researchers who want to test ROS-based hardware in its initial phase of development. 

The modularity of this package and the fact that it maps to any desired topic opens an opportunity to a wide range of applications  

How does it work? 

Robokinesis package has 2 ROS nodes: 

Perceptron node: uses single layer multi-class perceptron to train a model that maps the input raw sensor data to distinguishable signals  

Core node: maps the distinguishable sensor data to ROS topics at user-defined range and frequency  

The Ros-Bridge-Suite package subscribes to converted ROS topics and streams to the remote robot over a WebSocket connection 

The diagram below shows the entire software architecture, along with hardware connections. 

Workflow 

Initialization:  

Define sensor inputs, desired topics, range, frequency, remote robot IP and port in the package's config.yaml  

Training & testing:  

Create a dataset of actions and its corresponding raw sensor data  

Train the model using the Perceptron node.  

Implementation:  

Connect the robot to the wearable's IP and port, and control it using the trained model  

Hardware Specs: 


Hardware considerations: 

Pi Zero W was chosen considering its size (user can wear it), inbuilt WiFi/Bluetooth (to communicate directly to the robot, eliminating the need to have a computer in between wearable and robot), and can run ROS onboard (all computation would be done on the wearable) 

For the demo, a turtlebot3 was controlled using the wearable. 

To maneuver the turtlebot, only 4 topics are required to be mapped, hence reducing the number of distinguishable signals required to 4. 

For 4 distinguishable signals, the IMU alone is enough. 

The hardware setup with sensors IMU and muscle sensor, can give up to 9+4 distinguishable signals, and hence can be mapped to 13 different ROS topics of user’s choice 

The fewer the number of topics required, the faster the publishing frequency will be. Hence, it’s a tradeoff for the given constraints of the hardware. 

Lessons Learned 

This project allowed developing skills required for developing ROS-based packages for constrained RTOS hardware, also giving exposure to challenges like latency, sensor heating (changes calibration), etc, and tuning code to minimize error and overcome the mentioned challenges. Robotics is now penetrating domestic/consumer markets, developing a low-cost wearable project for controlling robots 

The images below show the internal hardware figure (1), cased hardware in figure (2), and the third figure with EMG sensors. (The device can hold up to 4 EMG sensors as the ADC is 4 channels.) 

Links 


To know more about Implementation details and how to use the Robokinesis package visit: https://robokinesis.mihr.io/  