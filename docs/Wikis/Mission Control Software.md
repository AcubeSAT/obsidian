# OBC/ADCS campaign ‐ Mission Control System Manual

### Table of contents
1. [Introduction](#introduction)
2. [Telemetry and Commanding](#telemetry-and-commanding)
3. [YAMCS-Board Communication](#yamcs-board-communication)
4. [Message Handling](#message-handling)
5. [Backup Scripts](#backup-scripts)

### List of Abbreviations

| Abbreviation | Full Name                                   |
| ------------ | ------------------------------------------- |
| ADCS         | Attitude Determination Control Subsystem    |
| CAN          | Controller Area Network                     |
| CUC          | CCSDS Unsegmented Time Code                 |
| MCU          | MicroController Unit                        |
| MRAM         | Magnetoresistive Random Access Memory       |
| NAND         | NOT AND                                     |
| OBC          | On Board Computer                           |
| OBDH         | On Board Data Handling                      |
| PUS          | Packet Utilization Standard                 |
| RX           | Receive                                     |
| TC           | Telecommand                                 |
| TCP          | Transmission Control Protocol               |
| TM           | Telemetry                                   |
| TX           | Transmit                                    |
| UART         | Universal Asynchronous Receiver-Transmitter |
| USB          | Universal Serial Bus                        |
| XTCE XML     | Telemetric and Command Exchange             |
| YAMCS        | Yet Another Mission Control System          |

## Introduction

Communication between the OBC-ADCS Board during the Environmental Testing will be established through a set of PUS service types as described in ECSS-E-ST-70-41C standard, based on the mission’s requirements.

YAMCS is the software package making this communication possible, allowing the retrieval and archiving of Telemetry transmitted from the board as well as the creation and transmission of Telecommands to the board. YAMCS includes a Web Interface which provides quick access and control over many of its features.

During the Testing data regarding the status of the Board and the OBC and ADCS parameters will be collected and visualized. As far as the storage of the data is concerned, YAMCS server provides the primary Archive. But as mentioned in the document a Backup Database outside the YAMCS server can also be created.

This document describes the contents of the yamcs-instance project regarding the available TMs and TCs. Furthermore, it provides guidance on the operation of YAMCS Web Interface as far as handling of TMs and TCs is concerned.

An important mention is that all TM and TC packets comply with the CCSDS Space Packet Protocol (CCSDS-132.0-B-2, CCSDS-232.0-B-3) and the ECSS-E-ST-70-41C standard and the structure of YAMCS follows the XTCE schema, with the exception of the constraints imposed by the YAMCS mission control software, to encode and decode packets.

## Telemetry and Commanding

Through YAMCS mission control Web Interface data concerning the status of the OBC and ADCS parameters can be visualized.
To simply start the main YAMCS instance, run the following command:

```bash
mvn yamcs:run
```

In case you want to enable hot-backups (meaning backing up data **while** YAMCS is running) , you need to start the instance by enabling JMX with the command:

```bash
mvn yamcs:run -Dyamcs.jvmArgs="-Dcom.sun.management.jmxremote.port=9999 -Dcom.sun.management.mxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false"
```

After running the main YAMCS instance, YAMCS Web Interface will be initialized at localhost:8090.

### Web Interface

The web page opened at localhost:8090 consists of a sidenav and a home dashboard. Through the contents of the sidenav menu data gets handled.

![Sidenav](sidenav.png)  

#### Links

Four Data Links exist in YAMCS instance, configured in the /src/main/yamcs/etc/yamcs.myproject.yaml file. Three Data Links for receiving Telemetry from three different locations:

- ADCS-UART, listening to port 10016
- OBC-UART, listening to port 10015
- CAN-bus, listening to port 10017

and one for transmitting Telecommands:

- tcp-out, listening to port 10025

All Data Links listen to different TCP sockets and require an established connection to exchange data with the Board.
The **color** of the circle in front of every DataLink refers to the **status** of the Data Link:

- Green: Connection has been established.
- Light Green: Packets are being exchanged.
- Red: An error in the connection exists.
- Grey: Link is disabled.

![Data-Links](links.png)

#### Telemetry

As far as Telemetry is concerned the Packets and Parameters sections provide useful information regarding the incoming packets.

##### Packets
In this section all TM packets can be visualized once received via the DataLinks. They are classified based on their reception time.

  ![Packets](packets.png)

##### Parameters
Contains a list of all parameters defined in the YAMCS project. The values of
parameters get updated based on received TMs. The parameters are grouped into
five sub-folders:

- **AcubeSAT**: All OBC and ADCS parameters that will be used during the Environmental Testing are stored in this sub-folder. Their values get updated with reception of value-reporting TMs such as:
	- TM\[3,10\]: Housekeeping Parameter Report
	- TM\[3,25\]: Housekeeping Parameter Report 
	- TM\[20,2\]: Parameter Value Report

An overview of all Campaign parameters and their IDs is shown is shown in the following Tables.

ADCS Parametrs:
  Parameter ID | Description
  --- | ---
  1013 | Magnetometer Raw Values x
  1014 | Magnetometer Raw Values y
  1015 | Magnetometer Raw Values z
  1016 | Magnetometer Frequency
  1017 | Magnetometer cycle count on x
  1018 | Magnetometer cycle count on y
  1019 | Magnetometer cycle count on z
  1020 | Magnetometer self-test register
  1043 | Gyro measurements x
  1044 | Gyro measurements y
  1045 | Gyro measurements z
  1089 | Gyroscope X temperature
  1090 | Gyroscope Y temperature
  1091 | Gyroscope Z temperature
  1092 | ADCS board Temperature 1
  1093 | ADCS board Temperature 2
  1158 | Magnetometer axis x sign
  1159 | Magnetometer axis y sign
  1160 | Magnetometer axis z sign
  1164 | Gyro axis x sign
  1165 | Gyro axis y sign
  1166 | Gyro axis z sign
  1189 | Gyro bias x
  1190 | Gyro bias y
  1191 | Gyro bias z
  1218 | ADCS MCU temperature
  1220 | ADCS MCU boot counter
  1221 | ADCS MCU On-Board Time
  1224 | ADCS MCU Systick

OBC Parameters:
  Parameter ID | Description
  --- | ---
  5000 | OBDH board Temperature 1
  5001 | OBDH board Temperature 2
  5002 | OBC MCU temperature
  5004 | OBC MCU boot counter
  5012 | OBC On-Board Time
  5014 | OBC NAND currently used memory partition
  5017 | OBC MCU Systick
  5018 | CAN bus 1 load
  5019 | CAN bus 2 load
  5020 | Which CAN bus active
  5023 | OBC NAND FLASH threshold
  5024 | OBC MRAM threshold
  5025 | OBC NAND FLASH ON
  5026 | OBC MRAM ON

- **pus**: Contains all the packet header parameters, both primary and secondary,such as *time,sequence count, message type* and *service type*. Their values get updated with the reception of **every TM**, since all incoming packets contain the headers.

- **pus‐not‐used** : Contains the parameters transmitted in service **ST[12]**. Their values get updated with reception **ΤΜ[12,8]**: *Report Parameter Monitoring Definitions* and **ΤΜ[12,9]**: *Parameter Monitoring Definition Report* (both will not be used during the Testing).

- **pus‐verification**: Contains the parameters transmitted in service **ST[01]**.Their values get updated with reception **TM[1,1]**: *Successful Acceptance Verification Report* and **TM[1,2]**: *Failed Acceptance Verification Report* (both will not be used during the Testing).

- **YAMCS**: Contains parameters regarding the state of the links and the functionality of the instance. These parameters will not be used.

All **data types** of the parameters can be found in the /src/main/yamcs/mdb/dt.xml
file in yamcs-instance project.

#### Commanding

Only a few ECSS Services will be needed for the Environmental Testing. Their definition and location in the Commanding Section's sub-folders is shown in Table IV.
Service | Location
---|---
ST[03]: Housekeeping | pus
ST[04]: Parameter statistics reporting | pus
ST[11]: Time-based scheduling | time-based-scheduling
ST[17]: Test | pus
ST[20]: Parameter management | pus, report-values, set-values
ST[128]: Log Messages | pus

Based on the desirable TC to be sent, the user should navigate to the respective subfolder to locate it and then send it.

The procedure for **sending a TC** is the following:

1. Locate the sub-folder of the TC based on the Table above.
2. 2. Select the values of the configurable Arguments.
3. Press Send.

![Commands](commands.png)

After sending a TC, a "Resend this Command" option appears, giving the user the ability to re-send the same TC without doing the whole procedure all over again and thus saves time.

Some ECSS TCs can have multiple parameters as arguments, for example those requesting the value of N parameters, where N is user defined each time. However, YAMCS does not support this functionality, so as a workaround these TCs have been configured to **always** send a predefined number of parameters, lets say X. If the operator needs to get exactly X parameters, they just fill their respective ids. If however they need only 3, they must input N=3 in the corresponding field, select the desired 3 parameters and fill the rest randomly, as OBC will not really care and simply discard them.

#### TM-TC Definitions

- **Housekeeping Structures**
  For the execution of the service **ST[03]**: _Housekeeping_, 4 Housekeeping Structures have been implemented, complying with the _On Board Software_ project. Each structure contains a group of parameters which were differentiated by their sampling frequency and subsystem. For the creation of the groups, regarding the number of parameters included in each one of them, memory limits were considered. These structures are **static and pre‐configured** based on the needs of the Campaign. In case new Housekeeping Structures need to be added, the pus.xml file must be modified The final Housekeeping Structures as well as their sampling frequency and structure identification number are shown in the Table bellow.

| Structure               | Structure ID | Sampling Frequency |
| ----------------------- | ------------ | ------------------ |
| Housekeeping0.01        | 0            | 0.01sec            |
| HousekeepingOBC         | 4            | 1sec               |
| HousekeepingADCS        | 2            | 1sec               |
| HousekeepingADCSnotUsed | 3            | 1sec               |

List Of Parameters included in each structure:

- **Housekeeping0.01**:

  1. MagnetometerRawΧ
  2. MagnetometerRawY
  3. MagnetometerRawZ
  4. GyroscopeX
  5. GyroscopeY
  6. GyroscopeZ

- **HousekeepingOBC**:

  1. OBDHBoardTemperature1
  2. OBDHBoardTemperature2
  3. OBCMCUTemperature
  4. OnBoardTime
  5. OBCNANDcurrentlyUsedPartition
  6. OBCSystick
  7. CANbus1Load
  8. CANbus2Load
  9. ActiveCAN
  10. NANDLCLThreshold
  11. MRAMLCLThreshold
  12. OBCNANDOn
  13. OBCMRAMOn

- **HousekeepingADCS**:

  1. MagnetometerFrequency
  2. MagnetometerCycleCountΧ
  3. MagnetometerCycleCountΥ
  4. MagnetometerCycleCountΖ
  5. MagnetometerSelfTest
  6. GyroscopeXTemperature
  7. GyroscopeΥTemperature
  8. GyroscopeΖTemperature
  9. ADCSBoardTemperature1
  10. ADCSBoardTemperature2
  11. ADCSMCUTemperature
  12. ADCSMCUBootCounter
  13. ADCSMCUOnBoardTime
  14. ADCSSystick

- **HousekeepingADCSnotUsed**:

  1. MagnetometerSignX
  2. MagnetometerSignΥ
  3. MagnetometerSignΖ
  4. GyroSignX
  5. GyroSignY
  6. GyroSignZ
  7. GyroBiasX
  8. GyroBiasY
  9. GyroBiasZ

- **Default TCs**
  As mentioned above not all TCs have configurable Arguments. Some pre-made TCs with default values have been created. The following tables show the TC options for service **ST[20]**. As shown in the bellow Table , specific groups of parameters have been created. Each **TC[20,1]** for requesting the report of the values of parameters contains a default number of related parameters.

Telecommand | Description (number of parameters included)
---|---
TC[20,1]: reportGyroParameterValues | Gyroscope Related Parameters (6)
TC[20,1]: reportMagnetometerParameterValues | Magnetometer Related Parameters (8)
TC[20,1]: reportMcuParameterValues |MCU Related Parameters (7)
TC[20,1]: reportCanParameterValues |CAN Related Parameters (3)
TC[20,1]: reportBoardParameterValues | Board Related Parameters (4)
TC[20,1]: reportMemoryParameterValues | Memory Related Parameters (5)
TC[20,1]: reportTimeParameterValues | Time Related Parameter (1)

List of Parameters included in each group:

- **Gyroscope Related Parameters**:
    1. GyroscopeX
    2. GyroscopeY
    3. GyroscopeZ
    4. GyroscopeXTemperature
    5. GyroscopeYTemperature
    6. GyroscopeZTemperature

- **Magnetometer Related Parameters**:
    1. MagnetometerRawΧ
    2. MagnetometerRawY
    3. MagnetometerRawZ
    4. MagnetometerFrequency
    5. MagnetometerCycleCountΧ
    6. MagnetometerCycleCountY
    7. MagnetometerCycleCountZ
    8. MagnetometerSelfTest

- **MCU Related Parameters**:
    1. OBCBootCounter
    2. OBCSystick
    3. OBCMCUTemperature
    4. ADCSMCUTemperature
    5. ADCSMCUOnBoardTime
    6. ADCSSystick
    7. ADCSMCUBootCounter

- **CAN Related Parameters**:
    1. CANbus1Load
    2. CANbus2Load
    3. ActiveCAN

- **Board Related Parameters**:

    1. OBDHBoardTemperature1
    2. OBDHBoardTemperature2
    3. ADCSBoardTemperature1
    4. ADCSBoardTemperature2

- **Memory Related Parameters**:

    1. NANDLCLThreshold
    2. MRAMLCLThreshold
    3. OBCNANDOn
    4. OBCMRAMOn
    5. OBCNANDcurrentlyUsedPartition

- **Time Related Parameter**:
    1. OBCOnBoardTime

#### Mission Database
The Mission Database Section of the sidenav contains a list of all the Parameters, Containers and Commands existing in the yamcs-instance project as well as their location. The way these Components (Parameters, Containers, Commands) are presented is:

        /location(.xml file)/component-name
All these files are included in src/main/main/yamcs/mdb folder.

### Preprocessor
MyPacketPreprocessor class does some processing to all incoming data from each Data Link. Since incoming data is structured as a stream through the TCP ports, the Preprocessor splits each stream into separate packets automatically. This class is responsible for any error detection (and correction) and some basic information extraction from each packet such as:
- Generation time
- Sequence count
- Packet length

Of course, there are other parameters extracted from each packet, but these are the most crucial, because if they are not parsed properly, they can cause warnings, in the best case scenario, and malfunctions or errors, in the worst case scenario.
1. OBC encodes the packet's generation time using a custom CUC format. It is a 32 bit integer, representing the total tenths of a second since 1/1/2022. In YAMCS, we have implemented a CUC to UNIX time conversion function, since YAMCS internally uses the UNIX type representation.
2. Initially, YAMCS used UDP sockets to "listen" for new packets, but they are not as secure (in terms of packet transmission) as TCP. Also, TCP is restricted in terms of maximum packet length (1500) , so if a packet has length larger than that, the data link is dropped. The try-catch clauses should in theory catch these kind of exceptions and restore normal communication after a while. The reason it does not happen instantly is because TCP ports remain closed after the connection is dropped, sometimes even for a couple of minutes. This is by design and although unfortunate, TCP connections have been tested and displayed no packet loss, contrary to UDP.
3.  Sequence count is an id associated to each packet sent by the board, beginning with number 1. YAMCS expects the first packet to have a sequence count of 1. If a jump in sequence count is detected (sequence count > 1), a warning will be displayed in the terminal. This should not cause any problems in the whole process , with only one exception.

Be sure to check the terminal output frequently to detect any possible errors or warnings, especially if you are experiencing trouble in receiving or sending packets. For example, if you are sure the TM packets sent to YAMCS have a specific length but YAMCS does not recognise it, double check the corresponding field in the packet headers, in eccs-services **composeMessage** method of **MessageParser.cpp**

### Time Manipulation
YAMCS uses a conventional relational database to store all data communicated with the MCU. Both generation time and sequence count are used as primary composite key of the TM table in the database archive. That means they have to uniquely identify a packet; if YAMCS receives a new packet with the same **(generation time, sequence count)** tuple more than once, it will discard the previous entry stored in the database. This can happen, although it is quite unlikely, since after the MCU restarts, all parameters associated with time-keeping reset to zero (1/1/2020) and so do those regarding the sequence count of the packets. This in turn means an overwrite can occur, so as a
prevention measure, we can:
1. Set each packet's generation time as the current time, by replacing
    ```java
    packet.setGenerationTime(CUCtoUnix(time));
    ```
    with
    ```java
    packet.setGenerationTime(TimeEncoding.getWallclockTime());
    ```
    This means that we loose all information regarding on board time, but we ensure no packets are lost in the process.
2. Synchronize the on-board clock each time the MCU resets, using TC's to set the appropriate parameters.
3. Parse time as a parameter and disregard the one in the packet headers, if this
functionality is implemented by OBC.

## YAMCS-Board Communication

The devboard can be connected with a PC using a USB interface. In order for YAMCS to receive the messages from the USB port, **MessageHandler.py** script has been created. It forwards the messages from the USB port to the TCP port of YAMCS and vice-versa. For the campaign, there will be 3 serial connections to and from the PC. YAMCS is currently configured to have 3 data links; OBC, ADCS and CAN BUS There are two methods to connect the devboard with a USB port:
1. Using a USB cable connected to the debug port of the devboard. This is the default configuration and the usb port is listed as /dev/ttyACM0.
2. Using a UART to USB adapter. Both RX and TX ports of the configured UART interface of the devboard are connected to TX and RX ports of the adapter respectively. The board will be listed as /dev/ttyUSB0.
If more devboards are connected to the PC using either method, they will be listed as another /dev/ttyUSBX or /dev/ttyACMX device. In order to view all connected devices you can run:
```bash
ls /dev/ttyUSB*
## or
ls /dev/ttyACM*
```

**TIP**: When connecting multiple devices, run this command each time a new connection
is made in order to keep track of which serial port corresponds to which board. Those
changess are documented in the next section.

## Message Handling

Messages are handled with threads. Two types of threads are implemented, one listens to YAMCS and forwards the message to a serial port and the other does the exact opposite. Each serial and TCP port can be read by exactly **one** thread and written by **one** thread only (not nescessarily the same).

You can define the serial port and the TCP port using the **MessageHandler** class constructor. Please refer to the class documentation in the script. After all threads are finalized, simply run:
```bash
python3 MessageHandler.py
## or if you experience package problems
sudo -E python3 MessageHandler.py
```
All TMs sent by the boards and TCs sent by Yamcs will be printed in the terminal. If there is a need to separate the boards' output into different terminals, create a copy of the script for every board, keeping only one MCU listener thread and execute all scripts. Be careful though that YAMCS can send commands only to one board at a time; you can include only one YAMCS listener thread in total.

If you attempt to start a new YAMCS listener thread and another one already exists you will either get a "connection refused error" on either of the two threads. The same thing will happen if you try to create a new MCU listener thread for a port that is already being read by another thread (or another application such as Minicom); you will get a "device unavailable" error

## Backup Scripts

YAMCS has implemented a local database system, storing all TMs, TCs, parameters, alarms , events etc. We should be able to backup all this information, in case something goes wrong. This is achieved using a Google Drive command line interface called gdrive, which can be used to upload a folder and all it's contents to a specified google drive location.The backups are differential, meaning only the edited/new files are uploaded, and are created at a configurable, in the script, time interval. We cannot use AcubeSat's Google Drive space, since it is shared and the script cannot get access to it. That's we have created a new account under the name of yamcs.backup.acubesat@gmail.com. This account has already been used for testing, so in order for the setup to be successful, a **NEW** folder should be created and used as a backup storage location. The steps required are:
1. Read [readme.md](https://gitlab.com/acubesat/ops/yamcs-instance/-/blob/main/backup-scripts/readme.md) in yamcs-instance/backup-scripts.
2. Login to the account using the login credentials stored at [Nextcloud](https://cloud.spacedot.gr/index.php/apps/files/?dir=/AcubeSAT/Subsystems/OPS%20-%20Spacecraft%20Operations/YAMCS&fileid=391449).
3. Create a new folder and copy the id from the URL bar. For example, if the URL is
https://drive.google.com/drive/u/0/folders/1fTiQ-3cMKZrV3bJw_W1CM9BPzldjQNkl
then the id will be 1fTiQ-3cMKZrV3bJw_W1CM9BPzldjQNkl . Set it as the value of
the respective variable in yamcs-instance/backup-scripts/backup.sh.
4. Run `./gdrive about` to complete the setup.
5. **Make sure you start yamcs using this command, or else the process will fail**
```bash
mvn yamcs:run -Dyamcs.jvmArgs="-Dcom.sun.management.jmxremote.port=9999 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false"
```
6. Simply run `sh backup.sh` to start the backup process. Backups will be created
at a specified time interval and are differential, meaning only the new files are
uploaded.