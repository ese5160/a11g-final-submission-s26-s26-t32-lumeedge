[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Y5lYn2wb)

# a11g-final-submission

**Team Number: 32**

**Team Name: LumeEdge**

| Team Member Name | Email Address | GitHub Username |
| ---------------- | ------------- | --------------- |
| Yuao Guo         | guo01@seas.upenn.edu     | Og-118    |
| Yiwei Tang         | tgg123@seas.upenn.edu     | tggyyds    |

**GitHub Repository URL: [https://github.com/ese5160/a11g-final-submission-s26-s26-t32-lumeedge](https://github.com/ese5160/a11g-final-submission-s26-s26-t32-lumeedge)**

**GitHub WebPage URL: [https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge](https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge)**

## 1. Video Presentation

[https://youtu.be/i7tSZm3Seq0](https://youtu.be/i7tSZm3Seq0)

and on github webpage:

[https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge](https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge)

## 2. Project Summary

Please see github webpage:

[https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge](https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge)

## 3. Hardware & Software Requirements

### 3.1. Hardware Requirements Specification (HRS)

The following requirements define the electrical and physical constraints of the LumeEdge system. They are prioritized to ensure the device meets the **ESE 516** graduate-level complexity standards while remaining strictly testable.

#### 3.1.1 Power System Requirements

| ID               | Requirement Description                                                                                                                   | Priority            |Validation |
| :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------- | :------------------ |------|
| **HRS-01** | The device shall be powered by a single-cell Lithium-Ion battery with a nominal voltage of 3.7V.                                         | **Mandatory** | Passed. It can run in battery mode |
| **HRS-02** | The power system shall include an charge management controller to facilitate battery charging via USB-C.                                  | **Mandatory** | Passed. It can charge the battery |
| **HRS-03** | The system shall generate a regulated 3.3V rail ($\pm$5%) using a Buck Boost Converter topology to power the MCU and sensors efficiently. | **Mandatory** | Passed. We measure it with multimeter |
| **HRS-04** | The device should auto switch to external                                                                                                 | *Recommended*     | Passed. It will use USB-C if connected |

#### 3.1.2 Computing & Communication Requirements

| ID               | Requirement Description                                                                                                      | Priority            |Validation |
| :--------------- | :--------------------------------------------------------------------------------------------------------------------------- | :------------------ |------|
| **HRS-05** | The primary microcontroller shall be the SIWG917Y121MGABA SoC.                                                               | **Mandatory** | Passed. |
| **HRS-06** | The microcontroller shall utilize Wi-Fi to maintain connectivity with the Cloud LLM gateway.                                 | **Mandatory** | Passed. Wifi works normally and can communicate with gateway. |
| **HRS-07** | The system shall utilize a dedicated$I^2C$ bus operating at a minimum of 100 kHz (Standard Mode) for sensor communication. | **Mandatory** |Passed. I2C is in standard mode. |

#### 3.1.3 Sensing & Actuation Requirements

| ID               | Requirement Description                                                                                                                                     | Priority            |Validation |
| :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------ |-----------|
| **HRS-08** | The system shall include a Ambient Light Sensor to measure illuminance values.                                                                              | **Mandatory** | Passed. It has one. |
| **HRS-09** | The system shall include a Environmental Sensor to measure Temperature ($\pm 1.0^{\circ}C$) and Relative Humidity ($\pm 3\%$).                          | **Mandatory** | Passed. It has one. Accuracy is +- 0.2C and +- 2%RH in datasheet. |
| **HRS-10** | The device shall control the LED actuator brightness using Pulse Width Modulation (PWM) with a frequency of no less than 480 Hz to prevent visible flicker. | **Mandatory** | Passed. Frequency is 5KHz. |
| **HRS-11** | The system should have a screen to display system status.                                                                                                   | *Recommended*     | Passed. It has one. |
| **HRS-12** | The actuator shall have a driver to control a motor.                                                                                                        | **Mandatory** | Passed. It has one. |

#### 3.1.4 Physical & Budgetary Requirements

| ID               | Requirement Description                                                                                                                | Priority        | Validation |
| :--------------- | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------- | --------|
| **HRS-13** | The total Bill of Materials (BOM) cost for the sensing and actuation subsystem should not exceed $30.00 USD.                           | *Recommended* | Passed. |
| **HRS-14** | The PCB should be designed with mounting holes compatible with a standard electrical wall box enclosure.                               | *Recommended* | Passed.  |
| **HRS-15** | All major components (MCU, Regulators, Sensors) should be Surface Mount Devices (SMD) to reflect professional manufacturing standards. | *Recommended* | Passed.  |

### 3.2. Software Requirements Specification (SRS)

#### 3.2.1 System Initialization & Configuration

| ID               | Requirement Description                                                                                                                        | Priority            |Validation |
| :--------------- | :--------------------------------------------------------------------------------------------------------------------------------------------- | :------------------ |--------|
| **SRS-01** | The system**shall** provide a mechanism (e.g., SoftAP or BLE provisioning) to accept and save local Wi-Fi SSID and Password credentials. | **Mandatory** | Not Passed. We use locally auto switching mechanisms instead. |

#### 3.2.2. Sensor Data Acquisition

| ID               | Requirement Description                                                                                           | Priority            |Validation |
| :--------------- | :---------------------------------------------------------------------------------------------------------------- | :------------------ |-----|
| **SRS-02** | The firmware shall poll the Light Sensor every 1 seconds (configurable) to obtain the current Lux value. | **Mandatory** | Passed. About every 75ms.|
| **SRS-03** | The firmware shall poll the SHT40 sensor every 5 seconds to obtain Temperature and Humidity data.                | **Mandatory** | Passed. About every 550ms. |

#### 3.2.3 Cloud & LLM Integration

| ID               | Requirement Description                                                                                                                             | Priority            |Validation |
| :--------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------ |---------|
| **SRS-04** | The device shall establish a secure (TLS/SSL) connection to the Cloud Gateway (e.g., AWS IoT or Azure IoT).                                         | **Mandatory** |Passed. We use azure. |
| **SRS-05** | The system shall format sensor telemetry into a JSON payload containing `{"lux": value, "temp": value, "user_intent": string}` for transmission.  | **Mandatory** |Passed.|
| **SRS-06** | The system shall parse incoming JSON commands from the Cloud LLM containing target brightness levels (0-100%) and motor speed (if supported). | **Mandatory** |Passed.|
| **SRS-07** | If the Wi-Fi connection is lost, the device shall maintain the last known actuator state until connectivity is restored.                            | **Mandatory** |  Half Passed. the device maintain the last known actuator state, but reboot is needed to reconnect. |

#### 3.2.4 Actuation & Control Logic

| ID               | Requirement Description                                                                                                                    | Priority            |Validation |
| :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------- | :------------------ |----------|
| **SRS-08** | The firmware shall generate a hardware PWM signal on the GPIO connected to the MOSFET gate.                                                | **Mandatory** |Passed. |
| **SRS-09** | The control loop shall implement a "Soft-Ramp" feature, changing brightness by no more than 10% per 100ms, to prevent jarring transitions. | **Mandatory** |Passed. max rate is 1%/1s|
| **SRS-10** | The system should implement a PID control algorithm to maintain target brightness if external lighting conditions change rapidly.          | *Recommended*     |Passed. P = 0.001, I=D=0|

## 4. Project Photos & Screenshots

Please see github webpage:

[https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge](https://ese5160.github.io/a11g-final-submission-s26-s26-t32-lumeedge)

## 5. Codebase

Do *not* commit any of your source code to this repository. Rather, provide links to the other GitHub repository you've already been using with your firmware.

- A link to your final embedded C firmware codebases: [https://github.com/ese5160/final-project-firmware-s26-t32-lumeedge/tree/main/final/wifi_http_otaf_soc](https://github.com/ese5160/final-project-firmware-s26-t32-lumeedge/tree/main/final/wifi_http_otaf_soc)

- A link to your Node-RED dashboard code: [https://github.com/ese5160/final-project-firmware-s26-t32-lumeedge/tree/main/Node-RED](https://github.com/ese5160/final-project-firmware-s26-t32-lumeedge/tree/main/Node-RED)

- Links to any other software required for the functionality of your device