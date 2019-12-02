*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [Device Types and Devices](SIMPLELINKDEVICE.md) - [Send SimpleLink Data](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [**Node-RED MQTT**](MQTTCONFIG.md) - [Sensor Data](SIMPLELINKIOTDATA.md)
***

# Receive Device Environmental Sensor Data in Node-RED

## Lab Objectives

In this lab you will build a flow that receives Device environmental temperature and humidity sensor data.  You will learn:

- How to create a new Node-RED flow and configure MQTT Nodes
- How to output the Device environmental temperature and humidity data.
- How to work with JSON data and observe the sensor results in the Debug sidebar.

## Introduction

In just a few nodes, Node-RED can receive the data that was transmitted from the device over MQTT to Watson IoT Platform.  This simple exercise will be the foundation for the next several sections that plot the data in a dashboard, trigger Real Time threshold alerts, store the data in Cloud Storage and allow for data analytics and anomaly detection.

## MQTT Application connections

In a prior section you connected the SimpleLink application to the Watson IoT platform using an MQTT client.  In this section you will connect a Node-RED application to the Watson IoT platform.

The Watson IoT platform uses the open source MQTT protocol to allow devices and applications to connect to the IoT platform.  It adds some additional security and restrictions upon what is defined by the MQTT standard.  

### Watson IoT Connection types

In a prior section you defined a device type and created a device ID in the Watson IoT platform to represent your SimpleLink board. The connection was created as a device. In this section you will connect the Node-RED application as an **Application connection**.

Here are some Watson IoT connection fixed format types :

- Device : **d:*orgId*:*deviceType*:*deviceId***
  - Device connections can only produce events and consume commands as the registered device.
- Gateway : **g:*orgId*:*typeId*:*deviceId***
  - Gateways are a special type of device connection with additional privileges that can act on behalf of other devices if they are authorized.
- Application : **a:*orgId*:*appId***
  - Application connections can consume events from all devices, publish events on behalf of a devices and send commands to devices. Application connections have greater access than a device connection.
- Scalable application : **A:*orgId*:*appId***
  - Scalable applications can load balance event messages across multiple instances of an application.


### Topics

The Watson IoT platform restricts the topic space used by MQTT.  If you attempt to send an invalid topic to Watson IoT Platform, your connection will be terminated.  The valid topics are specified in the [Watson IoT platform documentation.](https://www.ibm.com/support/knowledgecenter/SSQP8H/iot/platform/applications/mqtt.html)  This tutorial only uses two types of topic formats:

- Subscribing to device events : **iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string***
- Publishing device commands : **iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string***

where *device_type*, *device_id*, *event_id*, *command_id* and *format_string* are set accordingly.

When subscribing to topics the wildcard character **+** can be used to subscribe to all events from any device type, device, event type or format.

### Authentication

In an earlier section, you needed to register your device and set an authentication token.  With an Application connection you need to use an API key and API token to authenticate.

When the Watson IoT platform is bound to a Cloud Foundry application on the IBM Cloud, a API key and token are automatically generated and can be found in the **Runtime** environment variable section of the application view on the IBM Cloud web user interface

![env vars](/screenshots/app_IoTCredentials.png)

You can use the automatically generated values or create your own from the App section of the Watson IoT Platform web console.

![IoT App key](/screenshots/generateKey.png)

If you generate your own key you must take a note of the token because, like the device token, once the screen showing the token is closed it is not recoverable.

The API Key is used as the username when connecting and the API Token is the password.

### Custom Certificates

If you have a custom server certificate configured on the Watson IoT platform then you must use the SNI (Server Name Indication) extension to the TLS protocol to specify the server name in the connection parameters or the IoT platorm will not use your custom certificate.

## Create the Node-RED flow to receive device events

### Step 1 - Configure an MQTT in Node

- From the Input category of the left Node-RED palette, select an **mqtt in node** and drag it onto your Node-RED flow.
- Double-click on the MQTT node. An **Edit mqtt in node** sidebar will open.
- Click the pencil icon next to the Server property to configure the MQTT server properties.
  ![new mqtt connection](/screenshots/mqtt-NewBroker.png)
  - The **Add new mqtt-broker config node** sidebar will open
    ![add mqtt broker config](/screenshots/mqtt-AddBrokerConfig.png)
  - On the **Connection** tab
  - Enter the server name in the **Server** field (*orgId*.messaging.internetofthings.ibmcloud.com)
  - Enter 8883 as the **Port**
  - Enter the **Client ID** (a:*orgId*:*appId*).  The appID can be any unique string
  - Enable secure (SSL/TLS) connection then select the pencil next to the TLS configuration to open the **Edit tls-config node** sidebar
    - Enable the Verify server certificate **checkbox**
    - Enter the **Server Name** (*orgId*.messaging.internetofthings.ibmcloud.com).  This sets the SNI extension on the TLS connection
    - Click on the **Add** button to close the **Edit tls-config node** ![TLS Config](/screenshots/TLSconfig.png)
  - You have finished on the **Connection** tab
  - Switch to the **Security** tab and enter the Username and Password - get these from the application **Runtime** environment variables tab of your IBM Cloud application. The API Key is used as the Username when connecting and the API Token is the Password.
    ![mqtt Broker Security](/screenshots/mqtt-BrokerSecurity.png)
  - Click on the **Update** button to return to the **Edit mqtt in node** sidepanel
- Set the **Topic** field to **iot-2/type/+/id/+/evt/+/fmt/json**  The wildcard **+** is used to select all events from all devices and all events.  The topic requires that the event contains JSON data.
- Select the **Output** as **a parsed JSON object**
  ![MQTT in node config](/screenshots/mqtt-InNodeConfig.png)
- Click **Done** to close the mqtt in node config sidepanel

### Step 2 - Extract the Temperature from the JSON Object

- Recall that the environmental sensor data was transmitted in a JSON object

 ```
 { "d": {"temp":X, "humidity":Y }}
 ```

- Node-RED passes data from node to node in a *msg.payload* JSON object.
- The **Change** node can be used to extract a particular value so that it can be directly output or manipulated (for instance in a Dashboard chart which we will take advantage of in the next section).
- From the Function category of the left Node-RED palette, select a **Change** node and drag it onto your Node-RED flow
- Double-click on the Change node. An **Edit change node** sidebar will open
- Configure the "to" AZ dropdown to msg. and set it to *payload.d.temp*
- Click on the red **Done** button
- Wire the node to the MQTT in node by clicking and dragging the connector on the right of the MQTT in node to the connector on the left of the change node
 ![Receive Sensor Data](/screenshots/mqtt-ReceiveSensorData-Change-Node.png)

## Step 3 - Node-RED Debug Nodes

- Debug nodes can be used to print out JSON object values and help you validate your program.
- From the Output category of the left Node-RED palette, drag two **debug nodes** onto your Node-RED flow.
- Double-click on one of them. An **Edit debug node** sidebar will open.
- Configure the Output to print the *complete msg object*.
- Click on the red **Done** button.
- Wire the 2 nodes as shown
 ![Receive Sensor Data](/screenshots/mqtt-ReceiveSensorData-Debug-Node.png)

### Step 4 - Wire the Node-RED nodes together

- Click on the red **Deploy** button in the upper right corner.
  - The **mqtt in** node should show status **Connected**
  - Observe the LaunchPad sensor data in the **debug** tab of the Node-RED right sidebar.  You can expand the twisties to expose the JSON object information. Hover over a debug message in the right sidebar and the node that generated the message will be outlined in orange.
  ![Receive Sensor Data](/screenshots/mqtt-ReceiveSensorData-Deploy.png)

***
*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [Device Types and Devices](SIMPLELINKDEVICE.md) - [Node-RED Setup](NODERED.md) - [**Node-RED MQTT**](MQTTCONFIG.md) - [Send SimpleLink Data](SENDCC3235.md) - [Sensor Data](SIMPLELINKIOTDATA.md)
***
