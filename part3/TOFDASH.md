*Quick links :*
[Home](/README.md) - [Node-RED Charts](DASHBOARD.md) - [Send mmWave ToF Data](MMWAVETOF.md) - [**mmWave Range Dashboard**](TOFDASH.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md) - [Summary](SUMMARY.md)
***

# Plot mmWave Distance on a Node-RED Dashboard

## Lab Objectives

In this lab you will plot the mmWave sensor data on a Node-RED Dashboard.  You will learn:

- How to display distance sensor data in a Node-RED Dashboard
- Node-RED Dashboard user interface nodes

### Introduction

IoT sensors that can measure distance with good accuracy are useful in numerous Industrial IoT, manufacturing, commercial use cases.  The TI SimpleLink millimeter wave BoosterPack calculates distance by measuring the time of flight of a wave and its reflection.  This section plots distance using a variety of Node-RED Dashboard user interface nodes.

### Step 1 - Import the Node-RED mmWave Dashboard Flow

- Open the “Get the Code” github URL listed below, mark or Ctrl-A to select all of the text, and copy the text for the flow to your Clipboard. Recall from a previous section, click on the Node-RED Menu, then Import, then Clipboard. Paste the text of the flow into the Import nodes dialog and press the red Import button.

<p align="center">
  <strong>Get the Code: <a href="/flows/NRD-mmWave-SensorData.json">Node-RED mmWave TOF Dashboard Flow</strong></a>
</p>


### Step 2 - Graph mmWave IoT Sensor data using Node-RED

- The mmWave Range flow displays the IoT Sensor Device data on a Node-RED Dashboard.  It uses the Node-RED Chart node to display a single bar representing the height.  The flow also implements a gauge. There is a nice node-red-contrib-ui-level widget that shows tick marks as both vertical and horizontal elements. Various mmWave sensor data is displayed as text values.

![Node-RED mmWave Range Flow](/screenshots/NRD-TI-mmWave-Dashboard-flow.png)

### Step 3 - mmWave Range Dashboard

- Turn to the Node-RED Dashboard browser tab, click on the menu tab in the upper left corner, and select the mmWave ToF tab.
- On the mmWave dashboard, you will see a bar chart, a Level and a Gauge.

![Node-RED mmWave Range Flow](/screenshots/NRD-TI-mmWave-Dashboard.png)


### Congratulations - The mmWave Dashboard is configured
Continue to the next step - [Store Distance Data](CLOUDANT.md)

***
*Quick links :*
[Home](/README.md) - [Node-RED Charts](DASHBOARD.md) - [Send mmWave Range Data](MMWAVETOF.md) - [**mmWave Range Dashboard**](TOFDASH.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md) - [Summary](SUMMARY.md)
***
