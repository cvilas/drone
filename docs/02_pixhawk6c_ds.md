# Pixhawk 6C

## Technical Specification

### Processors & Sensors

* FMU Processor: STM32H743&#x20;
  * 32 Bit Arm® Cortex®-M7, 480MHz, 2MB memory, 1MB SRAM&#x20;
* IO Processor: STM32F103
  * &#x20;32 Bit Arm® Cortex®-M3, 72MHz, 64KB SRAM&#x20;
* On-board sensors&#x20;
  * &#x20;Accel/Gyro: ICM-42688-P&#x20;
  * Accel/Gyro: BMI088 (BMI055 discontinued due to the end of production of the sensor)
  * Mag: IST8310&#x20;
  * Barometer: MS5611

### Electrical data

* Voltage Ratings:
  * Max input voltage: 6V
  * USB Power Input: 4.75\~5.25V
  * Servo Rail Input: 0\~36V
* Current Ratings:
  * Telem1 Max output current limiter: 1.5A
  * All other ports combined output current limiter: 1.5A

### Mechanical data

* Dimensions: 84.8 \* 44 \* 12.4 mm
* Weight (Aluminum Case): 59.3g
* Weight (Plastic Case): 34.6g

### Interfaces

* 16- PWM servo outputs (8 from IO, 8 from FMU) with hardware switchable 3.3V or 5V signal mode
* 3 general purpose serial ports
  * Telem1 - Full flow control, separate 1.5A current limit
  * Telem2 - Full flow control
  * Telem3
* 2 GPS ports
  * GPS1 - Full GPS port (GPS plus safety switch)
  * GPS2 - Basic GPS port
* 1 I2C port
  * Supports dedicated I2C calibration EEPROM located on the sensor module
* 2 CAN Buses
* 2 Debug port
  * FMU Debug
  * I/O Debug
* Dedicated R/C input for Spektrum / DSM and S.BUS, CPPM, analog / PWM RSSI
* Dedicated S.BUS output
* 2 Power input ports (Analog)

### Other Characteristics

* Operating temperature: -40 \~ 85°c

## Dimensions

![](./media/pixhawk_6c_dimensions.avif)

## Ports

* I/O PWM OUT = MAIN OUT
* FMU PWM OUT = AUX OUT

Note the pin order relative to retainer tab

![](./media/pixhawk_6c_port_pin_order.avif)

### **Power1 & 2**

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Pin</strong></td><td><strong>Signal</strong></td><td><strong>Voltage</strong></td></tr><tr><td>1(red)</td><td>VDD5V_BRICK1 (in)</td><td>+5V</td></tr><tr><td>2(black)</td><td>VDD5V_BRICK1 (in)</td><td>+5V</td></tr><tr><td>3(black)</td><td>CURRENT1</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>VOLTAGE1</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>GND</td><td>GND</td></tr><tr><td>6(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **Telem 1 Port**

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Pin</strong></td><td><strong>Signal</strong></td><td><strong>Voltage</strong></td></tr><tr><td>1(red)</td><td>VCC</td><td>+5V</td></tr><tr><td>2(black)</td><td>UART7_TX(out)</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>UART7_RX(in)</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>UART7_CTS(in)</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>UART7_RTS(out)</td><td>+3.3V</td></tr><tr><td>6(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **Telem 2 Port**

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Pin</strong></td><td><strong>Signal</strong></td><td><strong>Voltage</strong></td></tr><tr><td>1(red)</td><td>VCC</td><td>+5V</td></tr><tr><td>2(black)</td><td>UART5_TX(out)</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>UART5_RX(in)</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>UART5_CTS(in)</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>UART5_RTS(out)</td><td>+3.3V</td></tr><tr><td>6(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **Telem 3 Port**

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Pin</strong></td><td><strong>Signal</strong></td><td><strong>Voltage</strong></td></tr><tr><td>1(red)</td><td>VCC</td><td>+5V</td></tr><tr><td>2(black)</td><td>USART2_TX(out)</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>USART2_RX(in)</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>NOT CONNECTED*</td><td>-</td></tr><tr><td>5(black)</td><td>NOT CONNECTED*</td><td>-</td></tr><tr><td>6(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

**\* For Pixhawk 6C with SN number&#x20;***<mark style="color:blue;">**`XXXX 001 XXXXXX`**</mark>* **(SN can be found on the packaging), Telem3 port is connected as follow:**

* pin 4 -> I2C4\_SCL (3.3V)
* pin 5 -> I2C4\_SDA (3.3V)&#x20;

**Do not connect Non-I2C device (such as telemetry radio) to telem3 pin 4 & 5 if you have this version.**

### **GPS 1 Port**

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Pin</strong></td><td><strong>Signal</strong></td><td><strong>Voltage</strong></td></tr><tr><td>1(red)</td><td>VCC</td><td>+5V</td></tr><tr><td>2 black)</td><td>TX1(out)</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>RX1(in)</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>SCL1</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>SDA1</td><td>+3.3V</td></tr><tr><td>6(black)</td><td>SAFETY_SWITCH</td><td>+3.3V</td></tr><tr><td>7(black)</td><td>SAFETY_SWITCH_LED</td><td>+3.3V</td></tr><tr><td>8(black)</td><td>IO_VDD_3V3</td><td>+3.3V</td></tr><tr><td>9(black)</td><td>BUZZER-</td><td>0~5V</td></tr><tr><td>10(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **GPS2 Port**

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Pin</strong></td><td><strong>Signal</strong></td><td><strong>Voltage</strong></td></tr><tr><td>1(red)</td><td>VCC</td><td>+5V</td></tr><tr><td>2 black)</td><td>UART8_TX(out)</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>UART8_RX(in)</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>I2C2_SCL</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>I2C2_SDA</td><td>+3.3V</td></tr><tr><td>6(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **USB Port**

| **Pin**  | **Signal** | **Voltage** |
| -------- | ---------- | ----------- |
| 1(red)   | VBUS       | +5V         |
| 2(black) | DM         | +3.3V       |
| 3(black) | DP         | +3.3V       |
| 4(black) | GND        | GND         |

### **I2C Port**

| **Pin**  | **Signal**  | **Voltage** |
| -------- | ----------- | ----------- |
| 1(red)   | VCC         | +5V         |
| 2(black) | I2C2\_SCL\* | +3.3V       |
| 3(black) | I2C2\_SDA\* | +3.3V       |
| 4(black) | GND         | GND         |

**\* For Pixhawk 6C with SN number&#x20;***<mark style="color:blue;">**`XXXX XXX 20221100`**</mark>* **AND prior**<mark style="color:blue;">**,**</mark> **(SN can be found on the packaging), I2C port is connected as follow:**

* pin 2 -> I2C4\_SCL (3.3V)
* pin 3 -> I2C4\_SDA (3.3V)&#x20;

### **CAN1 & CAN2 Port**

| **Pin**  | **Signal** | **Voltage** |
| -------- | ---------- | ----------- |
| 1(red)   | VCC        | +5V         |
| 2(black) | CAN1\_H    | +3.3V       |
| 3(black) | CAN1\_L    | +3.3V       |
| 4(black) | GND        | GND         |

### **DSM RC Port** (JST-ZH 1.5mm)

| **Pin**   | **Signal**         | **Voltage** |
| --------- | ------------------ | ----------- |
| 1(yellow) | VDD\_3V3\_SPEKTRUM | +3.3V       |
| 2(black)  | GND                | GND         |
| 3(gray)   | DSM/SPEKTRUM IN    | +3.3V       |

### **PPM/SBUS RC port**

| **Pin**   | **Signal**         | **Voltage** |
| --------- | ------------------ | ----------- |
| 1(null)   | VDD\_5V\_PPM\_SBUS | +5V         |
| 2(yellow) | PPM\&SBUS\_IN      | +3.3V       |
| 3(null)   | RSSI\_IN           | +3.3V       |
| 4(red)    | (NOT CONNECTED)    | --          |
| 5(black)  | GND                | GND         |

### **SBus Out Port**

| **Pin**   | **Signal**      | **Voltage** |
| --------- | --------------- | ----------- |
| 1(red)    | (NOT CONNECTED) | --          |
| 2(yellow) | SBUS\_OUT       | +3.3V       |
| 3(black)  | GND             | GND         |

### **FMU PWM OUT (AUX OUT)**

<table data-search="false"><thead><tr><th>Pin</th><th>Signal</th><th>Voltage</th></tr></thead><tbody><tr><td>1 (Red)</td><td>VDD_Servo</td><td> </td></tr><tr><td>2 (Black)</td><td>FMU_CH1</td><td>+3.3V</td></tr><tr><td>3 (Black)</td><td>FMU_CH2</td><td>+3.3V</td></tr><tr><td>4 (Black)</td><td>FMU_CH3</td><td>+3.3V</td></tr><tr><td>5 (Black)</td><td>FMU_CH4</td><td>+3.3V</td></tr><tr><td>6 (Black)</td><td>FMU_CH5</td><td>+3.3V</td></tr><tr><td>7 (Black)</td><td>FMU_CH6</td><td>+3.3V</td></tr><tr><td>8 (Black)</td><td>FMU_CH7</td><td>+3.3V</td></tr><tr><td>9 (Black)</td><td>FMU_CH8</td><td>+3.3V</td></tr><tr><td>10(Black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **I/O PWM OUT (MAIN OUT)**

<table data-search="false"><thead><tr><th>Pin</th><th>Signal</th><th>Voltage</th></tr></thead><tbody><tr><td>1 (Red)</td><td>VDD_Servo</td><td> </td></tr><tr><td>2 (Black)</td><td>IO_CH1</td><td>+3.3V</td></tr><tr><td>3 (Black)</td><td>IO_CH2</td><td>+3.3V</td></tr><tr><td>4 (Black)</td><td>IO_CH3</td><td>+3.3V</td></tr><tr><td>5 (Black)</td><td>IO_CH4</td><td>+3.3V</td></tr><tr><td>6 (Black)</td><td>IO_CH5</td><td>+3.3V</td></tr><tr><td>7 (Black)</td><td>IO_CH6</td><td>+3.3V</td></tr><tr><td>8 (Black)</td><td>IO_CH7</td><td>+3.3V</td></tr><tr><td>9 (Black)</td><td>IO_CH8</td><td>+3.3V</td></tr><tr><td>10(Black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **FMU Debug Port** (JST SH 1mm Pitch)

<table data-search="false"><thead><tr><th>Pin</th><th>Signal</th><th>Voltage</th></tr></thead><tbody><tr><td>1(red)</td><td>FMU_VDD_3V3</td><td>+3.3V</td></tr><tr><td>2 black)</td><td>FMU_USART3_TX</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>FMU_USART3_RX</td><td>+3.3V</td></tr><tr><td>4(black)</td><td>FMU_SWD_IO</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>FMU_SWD_CK</td><td>+3.3V</td></tr><tr><td>6(black)</td><td>SPI6_SCK_EXTERNAL1</td><td>+3.3V</td></tr><tr><td>7(black)</td><td>NFC_GPIO</td><td>+3.3V</td></tr><tr><td>8(black)</td><td>PH11</td><td>+3.3V</td></tr><tr><td>9(black)</td><td>FMU_nRST</td><td>+3.3V</td></tr><tr><td>10(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

### **I/O Debug Port** (JST SH 1mm Pitch)

<table data-search="false"><thead><tr><th>Pin</th><th>Signal</th><th>Voltage</th></tr></thead><tbody><tr><td>1(red)</td><td>IO_VDD_3V3</td><td>+3.3V</td></tr><tr><td>2 black)</td><td>IO_USART1_TX</td><td>+3.3V</td></tr><tr><td>3(black)</td><td>(NOT CONNECTED)</td><td>--</td></tr><tr><td>4(black)</td><td>IO_SWD_IO</td><td>+3.3V</td></tr><tr><td>5(black)</td><td>IO_SWD_CK</td><td>+3.3V</td></tr><tr><td>6(black)</td><td>IO_SWO</td><td>+3.3V</td></tr><tr><td>7(black)</td><td>IO_SPARE_GPIO1</td><td>+3.3V</td></tr><tr><td>8(black)</td><td>IO_SPARE_GPIO2</td><td>+3.3V</td></tr><tr><td>9(black)</td><td>IO_nRST</td><td>+3.3V</td></tr><tr><td>10(black)</td><td>GND</td><td>GND</td></tr></tbody></table>

## Sample Wiring Diagram

![](./media/pixhawk_6c_sample_wiring_diagram.avif)
