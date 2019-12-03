*Quick links :*
[Home](/README.md) - [Unbox your SimpleLink CC3235SF LaunchPad](UNBOX.md) - [Code Composer Studio](CCSIDE.md) - [Sensor Data](SENSORDATA.md) - [**Send Data to QuickStart**](QUICKSTART.md)
***
## Watson IoT Quickstart

Quickstart is a way of getting a single device sending data to Watson IoT Platform that you can visualize in your browser.

See how easy it is to connect your device to Watson IoT Platform and view live sensor data.

Quickstart allows you to experiment without having to register.

### Section 5 - Send TI SimpleLink LaunchPad data to Watson IoT Quickstart

- Open Code Composer Studio using the default workspace and select the **watson_sensors_mmwave_CC3235SF_LAUNCHXL_tirtos_ccs** project.

- First configure the build options for this project to enable the on-board temperature (TMP117) and accelerometer (BMA2X2) sensors.

![CCS Project - Select Sensors](/screenshots/CCS-sensorsbuildconfig.png)

- Next edit the network_if.h header file to configure the SSID and PASSWORD of the external Wi-Fi Access Point.

![CCS Project - Configure Wi-Fi AP Credentials](/screenshots/CCS-networkif.png)

- Then build the project with the updated changes.

![CCS Project - Build Project](/screenshots/CCS-buildproject.png)

- Once project is built, make sure the LaunchPad is connected via USB and click the 'Bug' icon to 'Launch'.  This will switch the CCS 'perspective' to debug view and load the program onto the target LaunchPad. 

![CCS Project - Build Project](/screenshots/CCS-launchdebugger.png)

- The target will run to 'main' and halt.

![CCS Project - Build Project](/screenshots/CCS-programatmain.png)

- Next open a serial terminal (115200,n,8,1) to observe the console output from the LaunchPad board *XDS110 Application/User* Uart 

- Finally Click the 'Run/Resume(F8)' button to continue.

![CCS Project - Run/Resume](/screenshots/CCS-runresume.png)

- The serial terminal will show the board starting up, sensor initialisation and TLS connection to IBM MQTT Broker. 

![Terminal - Quickstart](/screenshots/TERM-quickstart.png)

- Observe the JSON formatted message that is published.  The application will send sensor data periodically, or when the SW2 (LEFT) button is pressed.

![Terminal - Quickstart](/screenshots/TERM-quickstart-json.png)

- Note the 'client id' of the board (based on a generic mylaunchpad name + MAC address) shown in the console view.  The 'device id' is the highlighted part of the client id.

![Terminal - Quickstart](/screenshots/TERM-quickstart-id.png)

- Connect to [Watson IoT Quickstart](https://quickstart.internetofthings.ibmcloud.com/#/) and enter the device id and observe data from the board.  Press the SW2 button a few times and observe the button state toggling!

![Terminal - Quickstart](/screenshots/QS-buttontoggle.png)

**Congratulations** - Your TI SimpleLink MCU is sending sensor data to Quickstart Watson IoT Platform.

Continue to the next step - [Create an Internet of Things Platform Starter application](/part2/CREATEIOTP.md)
***

*Quick links :*
[Home](/README.md) - [Unbox your SimpleLink CC3235SF LaunchPad](UNBOX.md) - [Code Composer Studio](CCSIDE.md) - [Sensor Data](SENSORDATA.md) - [**Send Data to QuickStart**](QUICKSTART.md)
***
