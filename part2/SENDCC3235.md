*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [Device Types and Devices](SIMPLELINKDEVICE.md) - [**Send SimpleLink Data**](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [Node-RED MQTT](MQTTCONFIG.md) - [Sensor Data](SIMPLELINKIOTDATA.md)
***

# Send Device Environmental Sensor Data to Node-RED

## Lab Objectives

In this lab you will configure the LaunchPad application to send data to the IBM Watson Platform using registered device credentials.  Once data is inside the Watson IoT platform there are many cloud services that can be used to process and handle the data.  Quickstart is very useful for testing the initial connection, viewing data and evaluating base services, but devices should be registered for production systems.

### Introduction

There are just a few steps to reconfigure the LaunchPad application from the Quickstart (unregistered) service to the Watson (registered) platform. 

### Updating the credentials

- You will need the device credentials created in the previous section.
- Edit watson_iot_config.h

- Firstly, enable 'registered mode' by enabling the define of *WATSON_IOT_SERVICE_REGISTERED*
![CCS Project - Enable Registered](/screenshots/CCS-registereduncomment.png)

- Set the organisation *WATSON_IOT_ORGANISATION*
![CCS Project - Set Org](/screenshots/CCS-registeredorg.png)

- Set the device type *WATSON_IOT_DEVICETYPE* and id *WATSON_IOT_DEVICEID*
![CCS Project - Set Type and Id](/screenshots/CCS-registeredtypedeviceid.png)

- Next, set the authentication token *WATSON_IOT_TOKEN_PASSWORD*
![CCS Project - Set Token](/screenshots/CCS-registeredtoken.png)

### Rebuild the application

- Then build the project with the updated changes

![CCS Project - Build](/screenshots/CCS-buildproject.png)

- Reload and Rerun the application.

- The serial terminal will show the board starting up, sensor initialisation and TLS connection to IBM MQTT Broker.  Note the new clientid containing the 'org','type' and 'deviceid'. 

![Terminal - Registered](/screenshots/TERM-registered.png)- 


<!--
- How to use Code Composer Studio

### Introduction

In just a few nodes, Node-RED can send the TI SimpleLink LaunchPad environmental sensor data from the edge over MQTT to Watson IoT Platform.  

### Step 1 - Code Composer Studio

- .
- Click on the Done button

### Step 2 - Configure the Watson IoT Credential

- .
- Click on the **Done** button

### Step 3 - Compile

-  .
- Click on the **Deploy** button

### Step 4 - Flash

- .
-->


**Congratulations** - Your TI SimpleLink MCU is sending sensor data to Watson IoT Platform.

Continue to the next step - [Node-RED Setup](NODERED.md)

***
*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [Device Types and Devices](SIMPLELINKDEVICE.md) - [**Send SimpleLink Data**](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [Node-RED MQTT](MQTTCONFIG.md) - [Sensor Data](SIMPLELINKIOTDATA.md)
***
