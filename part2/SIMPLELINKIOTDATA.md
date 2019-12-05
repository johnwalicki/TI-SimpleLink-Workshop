*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [Device Types and Devices](SIMPLELINKDEVICE.md) - [Send SimpleLink Data](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [Node-RED MQTT](MQTTCONFIG.md) - [**Sensor Data**](SIMPLELINKIOTDATA.md)
***

# Receive Device Environmental Sensor Data in Node-RED

## Lab Objectives

In this lab you will build a flow that receives Device environmental temperature and motion sensor data.  You will learn:

- How to create a new Node-RED flow and configure MQTT Nodes
- How to output the Device environmental temperature and motion data.
- How to work with JSON data and observe the sensor results in the Debug sidebar.

### Introduction

In just a few nodes, Node-RED can receive the data that was transmitted from the device over MQTT to Watson IoT Platform.  This simple exercise will be the foundation for the next several sections that plot the data in a dashboard, trigger Real Time threshold alerts, store the data in Cloud Storage and allow for data analytics and anomaly detection.

### Step 1 - Extract the Temperature and Accelerometer data from the JSON Object

- Recall that the environmental sensor data was transmitted in a JSON object

 ```
 { "d": {"temp":26.63,"accel_x":-27,"accel_y":136,"accel_z":4172}}
 ```

- Node-RED passes data from node to node in a *msg.payload* JSON object.
- The **Change** node can be used to extract a particular value so that it can be directly output or manipulated (for instance in a Dashboard chart which we will take advantage of in the next section).
- From the Function category of the left Node-RED palette, select a **Change** node and drag it onto your Node-RED flow
- Double-click on the Change node. An **Edit change node** sidebar will open
- Configure the "to" AZ dropdown to msg. and set it to *payload.d.temp*
- Click on the red **Done** button
- Wire the node to the MQTT in node by clicking and dragging the connector on the right of the MQTT in node to the connector on the left of the change node
 ![Receive Sensor Data](/screenshots/mqtt-ReceiveSensorData-Change-Node.png)

## Step 2 - Node-RED Debug Nodes

- Debug nodes can be used to print out JSON object values and help you validate your program.
- From the Output category of the left Node-RED palette, drag two **debug nodes** onto your Node-RED flow.
- Double-click on one of them. An **Edit debug node** sidebar will open.
- Configure the Output to print the *complete msg object*.
- Click on the red **Done** button.
- Wire the 2 nodes as shown
 ![Receive Sensor Data](/screenshots/mqtt-ReceiveSensorData-Debug-Node.png)

### Step 3 - Wire the Node-RED nodes together

- Click on the red **Deploy** button in the upper right corner.
  - The **mqtt in** node should show status **Connected**
  - Observe the LaunchPad sensor data in the **debug** tab of the Node-RED right sidebar.  You can expand the twisties to expose the JSON object information. Hover over a debug message in the right sidebar and the node that generated the message will be outlined in orange.
  ![Receive Sensor Data](/screenshots/mqtt-ReceiveSensorData-Deploy.png)

**Congratulations** - Your Node-RED flow is receiving sensor data from the SimpleLink board.

Continue to the next section - [Node-RED Charts](/part3/DASHBOARD.md)
***
*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [Device Types and Devices](SIMPLELINKDEVICE.md) - [Send SimpleLink Data](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [Node-RED MQTT](MQTTCONFIG.md) - [**Sensor Data**](SIMPLELINKIOTDATA.md)
***
