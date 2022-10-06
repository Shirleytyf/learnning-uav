# Learning crazyflie

#### Source

https://www.bitcraze.io/documentation/tutorials/getting-started-with-crazyflie-2-x/#inst-comp

#### bitcraze-vm

https://github.com/bitcraze/bitcraze-vm

#### System Overview

![image-20220404151152020](C:\Users\tanyuanfang\AppData\Roaming\Typora\typora-user-images\image-20220404151152020.png)

##### The Crazyflie family of devices

The Crazyflie family members are the **[Crazyflie 2.0](https://www.bitcraze.io/products/old-products/crazyflie-2-0/)** nano quadcopter, the **[Crazyflie 2.1](https://www.bitcraze.io/products/crazyflie-2-1/)** nano quadcopter, the **[Crazyflie Bolt](https://www.bitcraze.io/products/crazyflie-bolt/)** quadcopter **controller** and the **[Roadrunner](https://www.bitcraze.io/products/roadrunner/)** UWB positioning tag. They are all based on similar hardware but have a bit different flavors and properties. They run similar firmware and can be used with the other components in the Crazyflie ecosystem, such as clients and positioning systems.

##### Crazyradio and clients

The main client for controlling the Crazyflie device family is the **python client** that runs on a PC and communicates via the **[Crazyradio PA](https://www.bitcraze.io/products/crazyradio-pa/)** USB dongle. The client uses a **python library**, which also is the main connection point for programs and scripts that communicate with the devices.

cflib is an API written in Python that is used to communicate with the Crazyflie and Crazyflie 2.0 quadcopters. It is intended to be used by client software to communicate with and control a Crazyflie quadcopter. For instance the [Crazyflie PC client](https://www.github.com/bitcraze/crazyflie-clients-python) uses the cflib.

![image-20220404151705441](C:\Users\tanyuanfang\AppData\Roaming\Typora\typora-user-images\image-20220404151705441.png)

Swarms of Crazyflies can be controlled through the python library, the external **CrazySwarm** project or other software.

There are **mobile phone apps** for Android and IOS that connects via BLE, mainly for manual flight.

##### Positioning technologies

source:https://www.bitcraze.io/documentation/system/positioning/

Positioning support is needed for automated or autonomous flight. 

There are two in-house position systems in the Crazyflie ecosystem: 

- the **Lighthouse positioning system** that uses SteamVR Base Stations.

- the Ultra Wide Band based **Loco Positioning System(LPS)**. (https://www.bitcraze.io/documentation/tutorials/getting-started-with-flying-using-lps/)

- It is also possible to integrate with external positioning systems, for instance **Motion Capture systems**.(Supporting VICON、NOKOV、OptiTrack and Qualisys)

#### Crazyswarm

##### source

https://crazyswarm.readthedocs.io/en/latest/

Crazyswarm has the following software architecture.

![image-20220404153228142](C:\Users\tanyuanfang\AppData\Roaming\Typora\typora-user-images\image-20220404153228142.png)

- **crazyflie_tools** These are command line tools that can be used using **rosrun crazyflie_tools <name> <arguments>**. These tools include methods to list logging variables, parameters, and to reboot individual crazyflies.
- **crazyswarm_server** This application is the core of the Crazyswarm. It provides the ROS interface, communicates with the robots and the motion capture system.
- **pycrazyswarm** This is a simplified Python library to use the Crazyswarm. It has two backends: the **physical backend** (communicating with the crazyswarm_server) and the **simulation backend**. The simulator uses parts of the official firmware for software-in-the-loop simulation. For performance reasons, the simulation does not include the dynamics and rather visualizes the setpoints.
- **Helper libraries** We provide a unified interface for different motion capture systems (libMotionCapture), a way to track rigid bodies frame-by-frame even with unique marker configurations (libObjectTracker), and a library for the low-level communication with the Crazyflie robots (crazyflie_cpp).

## Programming the Crazyflie

source

https://www.bitcraze.io/documentation/tutorials/getting-started-with-development/

## 用户指南 cfclient GUI

source

https://www.bitcraze.io/documentation/repository/crazyflie-clients-python/master/userguides/userguide_client/#firmware-upgrade

It is currently possible to change the following parameters which are stored in a none volatile memory:

- **Pitch trim** Can be programmed permanently with the trim values found to work good in the flight tab.
- **Roll trim** Can be programmed permanently with the trim values found to work good in the flight tab.
- **Radio channel** Can be set to anything between 0 and 125, correspond to a frequency from 2400MHz to 2525MHz. In most countries channel 0 to 80 is OK to use but this should be checked with you local regulations. If using 2M datarate, the copter channels should be 2 apart (2MHz).
- **Radio bandwidth** This can set the radio bandwidth to 250k, 1M or 2M. A lower bandwidth has longer range but has higher chance of collision. When used inside sometimes it is better to use 1M or 2M as it decreases the risk of collision with WiFi.
- **Radio address** (advanced) will set the shock burst address used for communicating. Note that if you change this then you will have to set the address correctly in the connect dialog.

## Repository overview

source:

https://www.bitcraze.io/documentation/repository/
