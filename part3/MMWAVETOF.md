*Quick links :*
[Home](/README.md) - [Node-RED Charts](DASHBOARD.md) - [**Send mmWave Range Data**](MMWAVETOF.md) - [mmWave Range Dashboard](TOFDASH.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md) - [Summary](SUMMARY.md)
***

# mmWave Sensors

## Lab Objectives

In this lab you will attach the mmWave BoosterPack to your TI SimpleLink LaunchPad and learn about mmWave Range sensors. You will learn:

- Add the mmWave BoosterPack to your TI SimpleLink LaunchPad
- View and configure the mmWave sensor
- Send mmWave range sensor data to Watson IoT Platform

### Introduction

Summarize and link to these articles
- http://www.ti.com/sensors/mmwave/what-is-mmwave.html
- http://www.ti.com/sensors/mmwave/overview.html

### Step 1 - Flashing the 'High Accuracy Demo' binary onto the IWR6843

*This step has been prior to the lab session*.  For referece, instructions for this can be found in the [TI mmWave Toolbox](http://dev.ti.com/tirex/explore/node?node=AJoMGA2ID9pCPWEKPi16wg__VLyFKFf__LATEST).

### Step 2 - Running the 'High Accuracy Visualiser' (GUI-Composer) mmWave Viewer.

![mmWave - board](/screenshots/iwr6843isk_iwr6843isk-e-003-annotate.jpg)

- Connect 5v power to the MMWAVEICBOOST board and USB to the XDS110 port.
- Open the visualiser using the pre-installed desktop shortcut.
- The application needs to communicate with 2 Serial Ports on the IWR6843.  One is used for configuration/application control and the other is used for streaming radar data.  First configure the serial ports, by clicking on the 'Options'->'Serial Ports' menu and select the 2 XDS110 serial ports connected to the IWR6843.

![mmWave - Visualiser Serial](/screenshots/MMWAVE-visualiserserial.png)

- Next press the **NRST/SW2** 'reset' button on the MMWAVEICBOOST and the visualiser should show 'Hardware Connected' at the bottom of the screen.

![mmWave - Visualiser Serial](/screenshots/MMWAVE-visualiserconnected.png)

- Click the 'LOAD CONFIG FROM PC AND START' and select the *high_accuracy_demo_68xx.cfg* as the configuration to load.

![mmWave - Visualiser Serial](/screenshots/MMWAVE-visualiserloadconfig.png)

- Next press the **NRST/SW2** 'reset' button on the MMWAVEICBOOST and the visualiser should start to show the mmWave range profile of a target sitting in front of the mmWave sensor.  Experiment with placing objects in front of this sensor.  

![mmWave - Visualiser Range](/screenshots/MMWAVE-visualiserrangeprofile.png)

- At this stage the mmWave sensor is configured and we now want to start sending data to the CC3235SF so that it can be sent to the cloud service.

- Close the High Accuracy Visualiser window and press the **SW1** button which will convert the output stream from binary to text which can easily be viewed and consumed by the CC3235SF MCU.

- Open a serial port on the CFG port (921600,n,8,1) and you should see this line buffered status reported every second from the mmWave board.

![Terminal - mmWave](/screenshots/TERM-mmwave.png)

### Step 4 - Connecting the LaunchPad and BoosterPack

The mmWave MMWAVEICBOOST has a BoosterPack connector which is compatible with the CC3235SF LaunchPad.  These boards can be connected together and the USB serial connection returned to the CC3235SF LaunchPad.

### Step 5 - Building the LaunchPad application

The code to handle the mmWave input stream is found in the *mmwave_uart.c* module.  This is a thread that reads line buffered data from the UART and then extracts data into variable before signalling to send a message to the cloud.

```c
/*
 *  ======== mmwaveUartThread ========
 */
static void *mmwaveUartThread(void *arg0)
{
    UART_Params uartParams;

    /* Create a UART with data processing off. */
    UART_Params_init(&uartParams);
    uartParams.readDataMode = UART_DATA_TEXT;
    uartParams.readReturnMode = UART_RETURN_NEWLINE;
    uartParams.baudRate = 921600;

    uart1 = UART_open(CONFIG_UART_1, &uartParams);

    if (uart1 == NULL) {
        // Error
        while (1);
    }

    while (1) {

        int nbytes = UART_read(uart1, lineBuffer, sizeof(lineBuffer));

        if (nbytes > 0) {

            // Extract Data from mmWave
            if (nbytes == 110) {
                sscanf(lineBuffer, "TimeStamp(s): %d, Frequency(Ghz): %d, Range(mm): %d, Temp_TX0(C): %d, Temp_RX0(C): %d",
                    &MMWAVE_uptime,
                    &MMWAVE_freq,
                    &MMWAVE_objdist,
                    &MMWAVE_temptx,
                    &MMWAVE_temprx);

                // Post to Cloud
                mmwaveHandler(0);
            }
```
The message handler function (also contained in mmwave_uart.c) then builds a json message to send.

```c
/*
 *  ======== MMWAVE_getJsonPayload ========
 */
void MMWAVE_getJsonPayload(char *string, int len)
{
    static int payloadCount = 0;

    sprintf(string, (const char *)"{\"d\":{"
        "\"mmwave_uptime\":%d"
        ",\"mmwave_freq\":%d"
        ",\"mmwave_objdist\":%d"
        ",\"mmwave_temptx\":%d"
        ",\"mmwave_temprx\":%d"
        ",\"name\":\"%s\""
        ",\"payloadCount\":%d"
        "}}"
        ,MMWAVE_uptime
        ,MMWAVE_freq
        ,MMWAVE_objdist
        ,MMWAVE_temptx
        ,MMWAVE_temprx
        ,"CC32XXLP+MMWAVEISK"
        ,payloadCount++
    );
}    
```

- All MMAVE code is enabled via build define *SENSORS_MMWAVE* which should be enabled.

![CCS Project - Enable mmwave](/screenshots/CCS-enablemmwave.png)

- Then build the project with the updated changes.

![CCS Project - Build Project](/screenshots/CCS-buildproject.png)

- Once project is built, make sure the LaunchPad is connected via USB and click the 'Bug' icon to 'Launch'.  This will switch the CCS 'perspective' to debug view and load the program onto the target LaunchPad. 

![CCS Project - Build Project](/screenshots/CCS-launchdebugger.png)

- The target will run to 'main' and halt.

![CCS Project - Build Project](/screenshots/CCS-programatmain.png)

- Next open a serial terminal (115200,n,8,1) to observe the console output from the LaunchPad board *XDS110 Application/User* Uart 

- Finally Click the 'Run/Resume(F8)' button to continue.

![CCS Project - Run/Resume](/screenshots/CCS-runresume.png)

- The serial terminal will show the board starting up, sensor initialisation and TLS connection to IBM MQTT Broker.  Each time mmwave sensor data is received it is forwarded to the IBM Watson service as shown.
- The enviromental data (temp/accelerometer/button) is also sent periodically as before.

![Terminal - Registered mmWave](/screenshots/TERM-registeredmmwave.png)


### Congratulations - The mmWave sensor is now sending status to the cloud!

Continue to the next step - [mmWave Range Dashboard](TOFDASH.md)

***
*Quick links :*
[Home](/README.md) - [Node-RED Charts](DASHBOARD.md) - [**Send mmWave ToF Data**](MMWAVETOF.md) - [mmWave Range Dashboard](TOFDASH.md) - [Store Data in Cloud Storage](CLOUDANT.md) - [Historical Charts](HISTORY.md) - [Summary](SUMMARY.md)
***
