***
*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [**Device Types and Devices**](SIMPLELINKDEVICE.md) - [Send SimpleLink Data](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [Node-RED MQTT](MQTTCONFIG.md) - [Sensor Data](SIMPLELINKIOTDATA.md)
***

# Registering a new device to the Watson IoT Platform

## Lab Objectives

This Lab will show you how to register your TI SimpleLink CC3235SF LaunchPad with the IBM Watson Internet of Things Platform.  In the lab you will learn:

- How to define a device type and register a device in the Watson IoT Platform

### Introduction

Before you can connect a device to the Watson IoT Platform you need to define how the device will connect to the platform and also register the device to generate an access token for the device.  This will be used to verify the device identity.

You need to decide how you want to group devices, by function, by hardware type, etc.  Each device registered on the platform must be registered against a device type.  There are no restrictions about how devices are grouped and the device types, for this workshop we will create a device type representing the TI SimpleLink devices.

### Step 1 - Add a new device type for SimpleLink device

- Navigate into the **Devices** section (1) of the console
![Create SimpleLink Device](/screenshots/IoTP-Devices.png)

- Select the **Device Types** section (2).  Press the **+ Add Device Type** (3) button
![Create SimpleLink Device](/screenshots/IoTP-DeviceType.png)

- Enter the following:
  - Type : Ensure **Device** is selected (NOT Gateway)
  - Name : Enter **ti-simplelink** (4)
- Press the **Next** button (5)
![Create SimpleLink Device](/screenshots/IoTP-DeviceType-Create.png)

- Press the **Finish** button (6)
![Create SimpleLink Device](/screenshots/IoTP-DeviceType-Done.png)

### Step 2 - Register a new *mylaunchpad1* device in the IoT Platform

You now have the opportunity to register a device.
- Press **Register Devices** (7)
![Create SimpleLink Device](/screenshots/IoTP-DeviceRegister.png)

- The *ti-simplelink* device type should be pre-selected.  You now need to enter a unique device ID.  You can choose how you want to identify devices.  For the workshop, use a simple format, such as **mylaunchpad1**. (8)
- Press **Next** button (9)
![Create SimpleLink Device](/screenshots/IoTP-DeviceName.png)

- Press **Next** button (10)
![Create SimpleLink Device](/screenshots/IoTP-DeviceInfo.png)
- You will be prompted to provide a token (11)

- Each time you connect the device the token will need to be presented to the server. Once the device is registered there is no way to recover a token. You will need to delete and reregister the device if the token is lost or forgotten.

- Enter a **token** for your device (11) then press **Next** (12).
![Create SimpleLink Device](/screenshots/IoTP-DeviceToken.png)

- You will see a summary of the device.  Press **Finish** to complete the device registration.
![Create SimpleLink Device](/screenshots/IoTP-DeviceSummary.png)

- You are now shown a **Device Credentials** page - this is the last chance you get to see the token.  Once you leave this page the token can not be recovered. Write down the Org, Device Type, Device ID and Authentication Token. You might even consider taking a screen shot.
![Create SimpleLink Device](/screenshots/IoTP-DeviceCreds.png)

**Congratulations** : You have created a device and in the next section you will send data securely to Watson IoT Platform using TLS encrypted MQTT packets and server certificates.

Continue to the next step - [Send SimpleLink Data](SENDCC3235.md)
***
*Quick links :*
[Home](/README.md) - [IoT Platform Starter](CREATEIOTP.md) - [**Device Types and Devices**](SIMPLELINKDEVICE.md) - [Send SimpleLink Data](SENDCC3235.md) - [Node-RED Setup](NODERED.md) - [Node-RED MQTT](MQTTCONFIG.md) - [Sensor Data](SIMPLELINKIOTDATA.md)
***
