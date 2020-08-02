## Adaptive Systems

### Infosys Consulting Romania

## 1. Hardware

 Two Alphabot robotic development platforms
 Four 16850 Li-Ion Batteries
 Two charging/discharging protection circuits for the batteries (FDC-2S- 2 )
 Two Raspberry Pi Model 3B (or 3B+) SBCs

 Two Raspberry Pi (B) Rev. 2.0 cameras
 One RGB sensor (TCS34725)
 One 8.4V Li-Ion charger for starting the robots
 A map with a black lined grid and four colored shapes used as finish points
 Four mini shapes used for color recognition as starting target

 Two HC-SR04 ultrasonic sensors

## 2. Project overview

## 2.1. Introduction

The Adaptive Systems Experience is represented by two Alphabot robotic
development platforms which cooperate in reaching a common goal by sending
each other critical messages such as positioning, current path, visited places.

AlphaBot is a platform compatible with Raspberry Pi and Arduino. It consists of the
AlphaBot mainboard, the mobile chassis, and everything required to get it moving.
It can perceive its environment and perform relative response. It involves the
following technologies: Tracking line, obstacle avoidance, mobile phone/PC video
monitoring, WIFI/Bluetooth/ZigBee/Infrared remote control and the likes.

### 2.2. Real life application

This project is meant to innovate way in which self-driving cars are communicating
in order to find the optimal path and also not to collide with each other. Beside
this, another real life application of the project could be in automating warehouses
by making them more organized and efficient, using image recognition and
algorithms for finding the most efficient road when the packages are moved around
and stored.

## 3. Technology details

```

 Raspberry Pi:
o Scripts built using Python 3 with OpenCV and MQTT packages
```

o Start the control application and select starting positions for the
Alphabots and then press Connect. A dialog will pop up and ask if
calibration should be done -> press Yes.
o The Alphabots should be placed with the IR sensors perpendicular to
a black line and while the calibration process is running, the robots
should be moved forward and backwards so that the sensors could
store the minimum and maximum values that they should be able to
recognize. These values will be stored in a file and used for all the
following runs until a new calibration is made.
 Insert a starting shape into the RGB sensor and then the robots should start
moving and searching for the finish with the corresponding color to the one
that they’ve received.
 Each robot chooses the closest corner to him and finds the optimal path to
it using Dijkstra’s Algorithm. Each intersection of the map represents a node
in a graph on which the algorithm is applied. At short time intervals, the
agents send each other messages, using MQTT package, such as position on
the map, the chosen path, the colors found so far at the finish points. Using
these information, they are able to avoid each other, changing their paths
accordingly.
 The color recognition is made using HSV color scheme so that changes in
lightning conditions will not affect the functionality of the agents.

 When an Alphabot encounters an obstacle, it will change its path (using
Dijkstra’s Algorithm) and will tell the other agent where the map is blocked
in order to avoid that route.


## 7. Difficulties encountered

```
 The Li-Ion batteries were draining under the safe voltage of 3.0V so
they were not capable of holding the charge anymore. The solution to
this problem was to add a protection circuit that would prevent this
from happening and cut the power when the voltage passes a certain
limit.
 The IR Line Tracking Sensors were reading bad values so a calibration
algorithm was added in the beginning
 When the ultrasonic sensor was connected to its original port on the
Alphabot board it interfered with the IR Line Tracking Sensor, both
using the same GPIO ports so this was fixed by connecting it to the
servomotor ports. Also, sometimes the readings were erroneous or
the sensor would become stuck so the fix for this was adding a
software timeout so that the sensor would not infinitely wait for a
response.
 An image recognition algorithm using OpenCV and Tensorflow was
implemented for finding the finishes but the hardware capabilities of
the Raspberry Pi allowed a performance of only 1 FPS using a live feed.
The approach was changed and the current implementation uses an
algorithm based on color recognition which is a lot faster and easier to
use.
```

## 8. Gallery


