# Räumi
Räumi ist ein Lego Spike Roboter, der durch den Raum navigiert ohne gegen Wänder oder andere Hindernisse zu Fahren und dabei Objekte verschiedener Farbe aufsammeln und sortieren kann.
In dieser Dokumentation wird in einzelschritten festgehalten, wie die Teilaufgaben durch Hard- und Software erreicht werden

Räumi is a Lego Spike Robot, which can navigate through space without colliding with walls and other obstacles. Additionally it can collect items of different colors and sort put them in the fitting container. In this documentation we show you which tasks the robot has to complete and how they are implemented in soft- and hardware

Sara: General information:
- Task of the robot
- numbers and types of motors and sensors
- which lego parts do we use and how many of them?
## Navigating though space
At the very beginning of our project we need a base with enoug space for the computer, the drive section, the collection arm and especially the object container. Therefore we build a base using the bricks you see in the picture below

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/06e295b1-b751-4774-b193-b87c21b7fc46" height=300 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/b15ababf-390f-424e-9844-68a580e95cd1" height=300 />

This construction provides enough stability and allows the robot to rotate on the floor. This is in important property when it comes to avoiding contact with obstacles. 

However, we need a drive section for the robot in order to be able to move throug space. Here we decided to go with two wheels, each with an own motor. We need two motors, because only then the robot is able to turn while staying in the same position. For stability reasons the wheels were placed at the back of the robot. the back of the robot is the side were we placed the computer. This design is inspired for example by conventional lawn mower robots. In the left picture your can see the bricks required for one wheel. The bricks for the other wheel are identical, but you have to keep in mind that it must be build according to mirror symmetry. The result for is shown in the right picture. 

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/a8123cec-c84d-4a9b-bf63-f1937dd7c328" height=300 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/f7331b5e-6736-4af9-9220-a30e0f809f92" height=300 />

Then the wheel get mounted to the base. Don't forget to connect the wheels with the computer. We connected the left wheel with exit A and the right wheel with exit B. If you do so you should get the following result:

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/39a5114c-422c-4ef7-9209-9083075f9947" height=300 />

Now the Hardware allows the robot to drive. But first, we need to implement the software.





Jonas: software
## Avoid collisions with obstacles
Now the robot can drive straight forward or in curves and even turn while staying in the same position. However it does not know yet when to do what. Our goal is that the robot usually drives straight ahead and if it comes accross an obstacles it should stop and turn into another direction. In order to achieve that we need a ultrasound sensor. Your need the following bricks:

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/60d8a8e6-0501-45d7-852f-f1fc43565d9b" height=300 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/bd8cd66d-e2d4-48f7-8513-11cdbf8bbc60" height=300 />

The challange here is to detect the obstacles wo don't want to collide with, but not to stop if we come accross on of the objects we want to collect. Therefore the sensor ist placed in sufficiant height. Additionally the sonsor should not interfere with the collection arm, which is why it is not placed at the center but more on the left side of the robot. 
Now we only have to implement when to stop and what to do if we come across an obstacle

Jonas: Software
Abstandsensor, was passiert wenn er auf ein Hinderniss trifft
## collect objects
Julian: Hardware filter + sensor + objects

Jonas: Hardware arm + software

Farbe des Objekts erkennen, Gabelarm, usw,
## sort Objects of different colors
Julian: Hardware

Jonas: Software

Farbsensor, Schubkurbel die den Container bewegt
## Results
Sara: what the robot can and cannot do

## Strengths and weaknesses
Sara: write this part, but we can brainstorm together

## (Delete this in the end) General tasks:
Julian: make and cut Videos and Photos

Sara: check grammar and spelling

Jonas: manage sources
