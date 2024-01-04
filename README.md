# Räumi
Räumi ist ein Lego Spike Roboter, der durch den Raum navigiert ohne gegen Wänder oder andere Hindernisse zu Fahren und dabei Objekte verschiedener Farbe aufsammeln und sortieren kann.
In dieser Dokumentation wird in einzelschritten festgehalten, wie die Teilaufgaben durch Hard- und Software erreicht werden

Räumi is a Lego Spike Robot, which can navigate through space without colliding with walls and other obstacles. Additionally it can collect items of different colors and sort put them in the fitting container. In this documentation we show you which tasks the robot has to complete and how they are implemented in soft- and hardware

Sara: General information:
- Task of the robot
- numbers and types of motors and sensors
- which lego parts do we use and how many of them?
## Navigating through the room
At the very beginning of our project we need a base with enoug space for the computer, the drive section, the collection arm and especially the object container. Therefore we build a base using the bricks you see in the picture below

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/06e295b1-b751-4774-b193-b87c21b7fc46" height=200 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/b15ababf-390f-424e-9844-68a580e95cd1" height=200 />

This construction provides enough stability and allows the robot to rotate on the floor. This is an important property when it comes to avoiding contact with obstacles. 

However, we need a drive section for the robot in order to be able to move throug space. Here we decided to go with two wheels, each with an own motor. We need two motors, because only then the robot is able to turn while staying in the same position. For stability reasons the wheels were placed at the back of the robot. the back of the robot is the side were we placed the computer. This design is inspired for example by conventional lawn mower robots. In the left picture your can see the bricks required for one wheel. The bricks for the other wheel are identical, but you have to keep in mind that it must be build according to mirror symmetry. The result for is shown in the right picture. 

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/a8123cec-c84d-4a9b-bf63-f1937dd7c328" height=200 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/f7331b5e-6736-4af9-9220-a30e0f809f92" height=200 />

Then the wheel get mounted to the base. Don't forget to connect the wheels with the computer. We connected the left wheel with exit A and the right wheel with exit B. If you do so you should get the following result:

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/39a5114c-422c-4ef7-9209-9083075f9947" height=200 />

Now the Hardware allows the robot to drive. But first, we need to implement the software.

## Forward Movement Code Description
To move the robot forward, we need two code blocks. The first block begins with an "Event" block and serves as the foundation for our entire subsequent code. This "Event" block determines what happens when the program starts. For forward movement, we initially define the motors responsible for propulsion (in our case, the motors connected to ports A and B), along with a loop that executes the custom "forward" block.

Now, let's create a custom code block named "Forward." The use of custom code blocks helps maintain code clarity. Within this block, we only need two "Movement" blocks. In the Lego Spike environment, individual motor control is not necessary for forward movement. The "Movement" blocks automatically control both motors.

First, we set the speed to 35% of the maximum speed. Subsequently, the second block is executed to initiate forward movement. This structuring is aimed at simplifying comprehension and facilitating code maintenance.

<img src = "https://github.com/julianfabinc/Raeumi/assets/153218995/26bd341c-52ec-4c7e-8aa7-9dd76748ff3f" height=200/>

This code causes the robot to keep driving straight ahead. In the following sections, this code is supplemented further and further so that the robot can navigate through the room.



## Avoid collisions with obstacles
Now the robot can drive straight forward or in curves and even turn while staying in the same position. However it does not know yet when to do what. Our goal is that the robot usually drives straight ahead and if it comes accross an obstacles it should stop and turn into another direction. In order to achieve that we need a ultrasound sensor. Your need the following bricks:

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/60d8a8e6-0501-45d7-852f-f1fc43565d9b" height=200 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/bd8cd66d-e2d4-48f7-8513-11cdbf8bbc60" height=200 />

The challange here is to detect the obstacles wo don't want to collide with, but not to stop if we come accross on of the objects we want to collect. Therefore the sensor ist placed in sufficiant height. Additionally the sonsor should not interfere with the collection arm, which is why it is not placed at the center but more on the left side of the robot. 
Now we only have to implement when to stop and what to do if we come across an obstacle

## Code description for collision avoidance
For collision avoidance, we first create another custom block named "reverse and turn." In the first line, we set the speed for the robot to move backward. The next line defines how far the robot should move backward. We have chosen a distance of 7 cm to ensure that the robot avoids colliding with an obstacle during the turn. The third line specifies how the robot should turn. We have decided that the robot should always turn to the right, selecting a random angle between 360 and 560 degrees. We opted for a random angle to allow the robot to cover as much area of the room as quickly as possible.

<img  src = "https://github.com/julianfabinc/Raeumi/assets/153218995/fd33fef6-f4a4-4107-b820-000748e18ebd" height = 200/>

Next, we will integrate the "reverse and turn" block into our infinite loop using an if statement. The condition for executing the "reverse_and_turn" block is based on the ultrasonic sensor connected to port D. A corresponding "sensor block" needs to be inserted into the if condition. We have set a distance of 12 cm or closer as the condition, as this distance ensures that the robot's arm does not collide with the obstacle.

<img src = "https://github.com/julianfabinc/Raeumi/assets/153218995/d8a26e42-f749-47d0-bf8b-cf608203f2b0" height = 200/>

The following image displays the complete Lego Spike code that we utilized for room navigation and collision avoidance.

<img src = "https://github.com/julianfabinc/Raeumi/assets/153218995/57689ea3-be88-4d1f-8960-9f7fd1332b48" height = 200/>

## collect objects
First of all we have to know what kind of objects we want to collect. At first, we wanted to have the opportunity to collect any object form. But therefore our collection arm would have to be very complex and would definetly need at least two or more ports on the computer to fullfill this task. The problem here is that we only have three ports left and we know we definetly need at least one for the object container and one for the color sensor. This means we need to constuct a collection device which works with only one motor. This makes it very hard to build something like a pair of pliers. So we decided to go with something like a fork to pick up objects. But this also means that we only can collect certain objects. 

So first of all lets take a look at how we want to identify the objects. Since we whant to sort the objects by color, we need the color sensor which we want to place at the center front. As objects usually lie on the ground, it makes sense to place the sensor as close as possible to the ground. This works really easy with our base, because we simply have to mount it at the desired position. However, with the current design, you need a good amount of luck that the objects come right in front of the sonsor. And if they don't the robot would just continue driving ahead and push the object with it without noticing it. Consequently it is desirable to identify the object at any position at the front of the robot. Since it is not possible to enlargen the sensor, we build a funnel in front of the color sensor, which places the objects right in front of it. So overall you need the following bricks for the color sensor and the funnel:

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/661e12bf-41c3-44ed-bfc9-31bccfd3965f" height=200 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/f15e32f2-fcca-4f1c-afe7-70339c15f0ee" height=200 />

Now we can identify the objetcts, but not yet collect them. So we need to build an arm which works simular to a fork. Hier Jonas schreiben (Ich hab für die Teile und so Screenshots von den Videos gemacht)

Jonas: Hardware arm + software

Of course we still need objects to be picked up. Since we want to sort by color, we need similar or identical objects of different color. Additionally the should allow the arm to pick them up. Since the objects are very light and don't have a lot of resistance, it seems to be the easiest way to build something on the objects which allows the arm to thread in. And since our robot cannot turn the objects around to the fitting position, it should be possible to thread in from any direction. So we constructed the objects as the following:


<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/74a605e0-2750-4dd9-8b61-1b2e8dd897d6" height=200 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/b05f3f48-4e2f-4401-8455-89294e0d1349" height=200 />


## sort Objects of different colors
Now that the robot can pick up the objects, it still needs to sort them by color. The color is detected by the color sensor and now it has to be moved to the right container. This can be achieved in two different ways: Either by moving the arm to right container or by moving the container in the position. We decided to move the container to the right position, because the collection arm already had a fitting height to pick up the objects. 

Since the objects are quite big, the container also has to be big so the obects can fit inside. Additionally there are several ways to move the container to the required position. One way would be to simply rotate the container 180°. The other, and probably better way is to move it from side to side. This has the advantage that it can be stabilised easier and it seems more natural. But in order to move the container from side to side we have to translate the circular movement of the motor to a straight movement. Therefore we build a mechanical linkage called "Schubkurbel", which basically is the same linkage as in a petrol engine. For this linkage we need a rail in which on part of the linkage can move from side to side. This is the part that will be connected to the object container. For this we need the bricks as followed

<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/6b1775d1-2492-4cac-98ea-1694c3178144" height=200 />
<img src = "https://github.com/julianfabinc/Raeumi/assets/153210113/6566fb98-6328-4c64-8d31-785375e90633" height=200 />

On top of this mechanical linkage we will put the container. As already mentioned, the container consists of two small containers, which each have to be big enough to provide space for at least on of the objects. From experimenting with the collection arm, we learned that a higher wall at the end of the container is usefull to prevent the object from overshooting the target. On the other side lower wall at the front side facilitates the acces to the container. Because the container turned out to be quit big, we tried to construct it in a way that keeps the container lightweight. This means that we tried to use more of a grid-like structure than actual walls. Furthermore it was challanging to build the container with many useful bricks already being used on other components. So do not be surprised that the container looks a bit unconventional at first.

<img src="https://github.com/julianfabinc/Raeumi/assets/153210113/7d9038ba-d979-42bc-90d0-a46faaa2b3d7" height="200">
<img src="https://github.com/julianfabinc/Raeumi/assets/153210113/eacfb576-ac2a-46e6-af83-861052aeeb6a" height="200">

As the container is quite big and only mouted on the narrow linkage, it requires further stabilization. With the computer being in the perfect height, it offer a good opportunity to provide stabilization for the container. We therefore built an addition rail on the computer, on which the application you can see in the lower part of the right picture above can slide along. With that the container is stable enoug to move from side to side and catch the objects put in by the collection arm

<img src="https://github.com/julianfabinc/Raeumi/assets/153210113/a8522f3b-b6c5-42c8-bd85-cb984d99de81" height="200">

With that, the robot has all the hardware it needs to fulfill its task. But there is still some work to do on the software.


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
