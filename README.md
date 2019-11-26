# TI SimpleLink Watson IoT Workshop
Texas Instruments SimpleLink and IBM Watson IoT Hands-On Workshop

## Texas Instruments SimpleLink and IBM Watson IoT Hands-On Workshop

Learn how to connect your next IoT Edge design to the Cloud using IBM Watson IoT Platform and the TI SimpleLink CC3235SF LaunchPad.  The CC3235SF features a ARM Cortex® -M4 MCU and wireless connectivity. In this workshop we will attach an BoosterPack sensor expansion board to showcase cloud connectivity features.  We will create a program in the TI Code Composer Studio.  The program will send sensor data to the IBM Watson IoT Platform, where Node-RED running in a Node web application in IBM Cloud will display a Dashboard.  The data will be saved to a Cloudant time series database.

**Presenters:**
- [**Roger Monk**](https://github.com/rdmonk) - TI System Applications Engineer
- [**John Walicki**](https://github.com/johnwalicki) - IBM Developer Advocate, CTO IoT / Edge Advocacy

This hands-on workshop will show you how to integrate sensors, wireless connectivity, a low-power microcontroller and sensor libraries into your next IoT Edge design. You’ll then learn to connect the TI SimpleLink LaunchPad to IBM Cloud and Watson IoT Platform to create a new application in minutes using Node-RED.

The hands-on training is a working session – please bring your laptop. Note: Administrator rights is needed for software and driver installation. TI will provide the required TI SimpleLink development boards and software. SPACE IS LIMITED FOR THIS SESSION – FIRST COME, FIRST SEATED.

**The TI SimpleLink boards must be returned after the session.**

## Learning Objectives:
In this workshop, you will learn how to:

### Part 1

- Learn about the [TI SimpleLink CC3235SF](http://www.ti.com/product/CC3235SF)
- Learn about the [TI SimpleLink WiFi CC3235SF dual band LaunchPad](http://www.ti.com/tool/LAUNCHXL-CC3235SF) development kit
- Learn about the [TI BoosterPack Boards](http://www.ti.com/design-resources/embedded-development/hardware-kits-boards.html)
- Install [Code Composer Studio IDE](http://www.ti.com/design-resources/embedded-development/ccs-development-tools.html) on your laptop
- Compile and run Environmental Sensor programs to observe temperature, humidity, acceleration and gyroscope information
- Send TI SimpleLink CC3235SF LaunchPad data to [Watson IoT Quickstart](https://quickstart.internetofthings.ibmcloud.com/#/)

### Part 2

- Create an IoT Starter Kit application running in IBM Cloud
- Launch the Watson IoT Starter application
- Open the Watson IoT Platform so that you can send/receive data from the SimpleLink device
- Create a SimpleLink device type and device
- Using Code Composer Studio, Compile and Flash a MCU program that sends MQTT data to Watson IoT Platform
- Configure the Node-RED visual programming editor
- Secure your Node-RED Editor in IBM Cloud
- Install additional Node-RED nodes
- Create a new Node-RED flow and configure IoT MQTT
- Output the TI SimpleLink CC3235SF LaunchPad temperature and humidity data
- Work with JSON data and observe the sensor results in the Debug sidebar

### Part 3

- Create a Node-RED Dashboard
- Experiment with Chart types
- Plot Real Time sensor data
- Attach the mmWave BoosterPack to your LaunchPad and compile a MCU binary
- Send Time of Flight (ToF) distance sensor data to Watson IoT
- Plot ToF distance sensor data
- Create a Node-RED flow that uses the Cloudant node
- Format a time series database record
- View Cloudant databases
- Read datasets from a Cloudant database
- Create a chart of historical data

## Prerequisites
This tutorial can be completed using an IBM Cloud Lite account.

* Create an [IBM Cloud account](https://ibm.biz/BdzgST)
* Log into [IBM Cloud](https://cloud.ibm.com/login)

## Part 1

### Section 1 - Unbox the TI SimpleLink CC3235SF LaunchPad development board

This section shows you how to unpack the TI SimpleLink CC3235SF LaunchPad development board and connect the Sensor expansion board.

- Instructions : [Unpack the TI SimpleLink CC3235SF LaunchPad and BoosterPacks](part1/UNBOX.md)

### Section 2 -  connect to the LaunchPad

This section shows you how to program the TI SimpleLink CC3235SF LaunchPad, connect to the WiFi and create the Watson IoT Cloud project

- Instructions : Install [Code Composer Studio IDE](part1/CCSIDE.md)

### Section 3 - Run the Environmental Sensor programs

This section shows you how to run the Environmental Sensor programs to observe temperature, humidity, acceleration and gyroscope information

- Instructions : [Environmental Sensor Data](part1/SENSORDATA.md)

### Section 4 - Send TI SimpleLink LaunchPad data to Watson IoT Quickstart

This section shows you how to send TI SimpleLink LaunchPad data to [Watson IoT Quickstart](https://quickstart.internetofthings.ibmcloud.com/#/)

- Instructions : [Send Sensor Data to Quickstart](part1/QUICKSTART.md)

## Part 2

### Section 6 - Create an Internet of Things Platform Starter application

- Instructions : [Create an Internet of Things Platform Starter application](part2/CREATEIOTP.md)

### Section 7 - Create a Watson IoT Platform Device Type and Device

- Instructions : [Create a Watson IoT Platform Device Type and Device](part2/SIMPLELINKDEVICE.md)

### Section 8 - Send Sensor Data from the SimpleLink LaunchPad to Node-RED Cloud

- Instructions : [Send Sensor Data from the LaunchPad to IBM Cloud](part2/SENDCC3235.md)

### Section 9 - Node-RED Set up and Configuration in IBM Cloud

- Instructions : [Node-RED Set up and Configuration in IBM Cloud](part2/NODERED.md)

### Section 10 - Configure MQTT Node to Receive Sensor data

- Instructions : [Configure the Node-RED MQTT input node to receive sensor data](part2/MQTTCONFIG.md)

### Section 11 - Receive SimpleLink LaunchPad Environmental Sensor Data in Node-RED

- Instructions : [Receive SimpleLink LaunchPad Environmental Sensor Data in Node-RED](part2/SIMPLELINKIOTDATA.md)

## Part 3

### Section 12 - Node-RED Dashboard Charts - Plot Environmental Sensor Data

- Instructions : [Node-RED Dashboard Charts - Plot Environmental Sensor Data](part3/DASHBOARD.md)

### Section 13 - mmWave BoosterPack - Time of Flight Sensor Data

- Instructions : [Add the mmWave BoosterPack to your LaunchPad and compile a MCU binary](part3/MMWAVETOF.md)

### Section 14 - Node-RED Dashboard - Plot ToF Distance Sensor Data

- Instructions : [Plot Time of Flight Sensor Data on a Node-RED Dashboard](TOFDASH.md)

### Section 15 - Store Data in Cloud Storage for Historical Data Analytics

- Instructions : [Store Data in Cloud Storage for Historical Data Analytics](part3/CLOUDANT.md)

### Section 14 - Node-RED Charts of Historical Sensor Data

- Instructions : [Node-RED Charts of Historical Sensor Data](part3/HISTORY.md)

## Workshop summary

This section summarizes what the workshop covered and also provides some useful links for further exploration of Edge, IoT and Data Science

- [Summary and links](part3/SUMMARY.md)

*Quick links :*
[Home](README.md) - [IoT Platform Starter](part2/CREATEIOTP.md) - [Device Types and Devices](part2/SIMPLELINKDEVICE.md) - [Node-RED Setup](NODERED.md) - [Sensor Data](SIMPLELINKIOTDATA.md) - [Node-RED Charts](DASHBOARD.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md)
***
