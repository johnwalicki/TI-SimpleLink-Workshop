*Quick links :*
[Home](/README.md) - [Node-RED Charts](DASHBOARD.md) - [Send mmWave ToF Data](MMWAVETOF.md) - [**Time of Flight Dashboard**](TOFDASH.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md) - [Summary](SUMMARY.md)
***

# Plot mmWave Distance on a Node-RED Dashboard

## Lab Objectives

In this lab you will plot the mmWave sensor data on a Node-RED Dashboard.  You will learn:

- How to display distance sensor data in a Node-RED Dashboard

### Introduction

The previous section stored the Device environment sensor data into a Cloudant DB.  This section will read the historical sensor data from a Cloud storage database and create a graph of prior readings.

### Step 1 - Import the Node-RED mmWave Dashboard Flow

- Open the “Get the Code” github URL listed below, mark or Ctrl-A to select all of the text, and copy the text for the flow to your Clipboard. Recall from a previous section, click on the Node-RED Menu, then Import, then Clipboard. Paste the text of the flow into the Import nodes dialog and press the red Import button.

<p align="center">
  <strong>Get the Code: <a href="/flows/NRD-mmWave-SensorData.json">Node-RED mmWave TOF Dashboard Flow</strong></a>
</p>


### Step 2 - Graph mmWave IoT Sensor data using Node-RED

- The mmWave Time of Flight flow displays the IoT Sensor Device data on a Node-RED Dashboard.

![Node-RED mmWave ToF Flow](/screenshots/NRD-TI-mmWave-Dashboard-flow.png)

### Step 3 - Time of Flight Dashboard

- Turn to the Node-RED Dashboard browser tab, click on the menu tab in the upper left corner, and select the mmWave ToF tab.
- On the mmWave ToF dashboard, you will see a bar chart, a Level and a Gauge.

![Node-RED mmWave ToF Flow](/screenshots/NRD-TI-mmWave-Dashboard.png)

### Congratulations - The mmWave Dashboard is configured
Continue to the next step - [Store Distance Data](CLOUDANT.md)

***
*Quick links :*
[Home](/README.md) - [Node-RED Charts](DASHBOARD.md) - [Send mmWave ToF Data](MMWAVETOF.md) - [**Time of Flight Dashboard**](TOFDASH.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md) - [Summary](SUMMARY.md)
***
