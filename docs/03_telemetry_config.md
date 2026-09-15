# Telemetry Wiring and Configuration Guide

## Pixhawk-6C Port Allocation

- **TELEM1**: SiK telemetry radio (MAVLink) - use stock 6-pin to 6-pin cable
- **TELEM2**: Radiomaster RP3-H (CRSF) - use modified 6-pin-to-4-pin cable. See below.

`TELEM1` for Mavlink/GCS telemetry is the PX4 default. `TELEM2` must be configured for RP3-H over CRSF, which requires a minor customisation in hardware (custom cable) and software (enabling CRSF in PX4)

## Wire Up RP3-H to Pixhawk-6C
 
#### Make 6-pin-to-4-pin Cable for RP3-H

Use a fine-tipped tool (eg: X-acto knife) to remap a 6-pin JST-GH connector (Pixhawk side) to a 4-pin JST-GH connector (RP3-H side). Gently lift the plastic retention tabs on the JST-GH housings to de-pin and re-arrange the wires as follows:

Pixhawk 6C TELEM2 (6-Pin) | RP3-H Receiver (4-Pin) | Signal Type
:------------------------ | :--------------------- | :----------
**Pin 1 (VCC)**           | **Pin 3 (VCC)**        | Power supply
**Pin 2 (TX)**            | **Pin 2 (RX)**         | Data line (crossed)
**Pin 3 (RX)**            | **Pin 1 (TX)**         | Data line (crossed)
Pin 4 (CTS)               | *No connection*        | Not used
Pin 5 (RTS)               | *No connection*        | Not used
**Pin 6 (GND)**           | **Pin 4 (GND)**        | Ground reference

*Warning: Double-check VCC and GND pins before powering up. Reversed power polarity can damage the receiver.*

## Build PX4 Custom Firmware With CRSF Enabled

**Reference**: https://docs.px4.io/main/en/telemetry/crsf_telemetry

- Clone the PX4 autopilot repo and launch the PX4 board configuration tool
  ```bash
  git clone --recursive https://github.com/cvilas/PX4-Autopilot.git
  cd PX4-Autopilot
  make px4_fmu-v6c_default boardconfig
  ```
- In the PX4 board config tool:
  - Disable the default `rc_input` module
    - Navigate to the drivers submenu, then scroll down to highlight `rc_input`.
    - Use the enter key to remove the `*` from `rc_input` checkbox.
  - Enable the `crsf_rc` module
    - Scroll to highlight the `RC` submenu, then press enter to open it.
    - Scroll to highlight `crsf_rc` and press enter to enable it.
- Save and exit the PX4 board config tool.
- Build the firmware
  ```bash
  make px4_fmu-v6c_default
  ```
- Connect the Pixhawk-6C to the PC via USB
- Upload firmware as part of the build process
  ```bash
  make px4_fmu-v6c_default upload
  ```

## Bind the R/C Transmitter/Receiver Pair

- Plug the RP3-H into Pixhawk-6C and power it up via USB-C port
- Follow instructions in [RP3-H user manual](./rp3-h_um.pdf) and [TX12 quick start guide](./tx12mk2_qsg.pdf)

## Configure Telemetry Channels via QGroundControl

- Connect your Pixhawk 6C to the PC via USB
- Start QGroundControl and navigate to **Vehicle Setup (Gear Icon) ➔ Parameters**.
- Configure `TELEM1` for SiK Radio
  - Search for `MAV_0_CONFIG` and ensure it is set to `TELEM 1` (Value: `101`).
  - Search for `SER_TEL1_BAUD` and set it to the baud rate configured in the SiK radio. `57600` is common, but it is not mandatory for every SiK setup. 
- Configure `TELEM2` for CRSF (RP3-H). Change these options sequentially:
  - Search for `MAV_1_CONFIG` (which natively claims TELEM2 for standard telemetry) and change it to `Disabled`.
  - Search for `RC_CRSF_PRT_CFG` and switch its value to `TELEM 2` (Value: `102`).
  - Reboot the vehicle
  - Search for `RC_CRSF_TEL_EN` and set it to `Enabled`. This enables bidirectional CRSF telemetry to the transmitter.

*Note: Do not set a separate CRSF baud rate: the CRSF driver configures it*

## System Validation

- Connect Pixhawk-6C to the PC via USB-C and start QGroundControl
- Turn on **RadioMaster TX12** handset. Verify that the RP3-H receiver status LED indicates a successful bind.
- In QGroundControl, navigate to **Vehicle Setup ➔ Radio**. 
- Move transmitter gimbal sticks. The channel slider graphics should respond dynamically in real-time. Follow the automated calibration wizard instructions to map your travel limits.
- Unplug the Pixhawk-6C from the PC and power it from a separate USB-C 5V source
- Plug the SiK Radio ground module into the PC via USB and the air module to the Pixhawk-6C
- Confirm that QGroundControl successfully interfaces over the wireless link to the Pixhawk-6C and can continue to read RC controller gimbal motions 

## Firmware Upgrades

### SiK Telemetry Radio

- Connect the SiK radio ground module to the laptop via USB
- Open QGroundControl: **Configure ➔ Firmware ➔ select SiK radio in the drop down menu ➔ Flash (follow onscreen instructions)**
- Repeat the same step for the SiK radio air module

### Radiomaster TX12 Transmitter and RP3-H Receiver

- Download the firmware using [ExpressLRS-Configurator](https://github.com/ExpressLRS/ExpressLRS-Configurator/releases)
- Create firmware files for both TX and receiver modules. 
  - Flashing method: WiFi
  - Device options
    - Regulatory domain: 2.4 GHz LBT
    - Binding Phrase: Set a unique string to bind the two modules. eg: `X500TX12RP3H`
  - Build (download the generated `firmware.bin`)
- Put the device in WiFi updating mode
  - TX module: Use the ExpressLRS Lua Script. Select `WiFi Connectivity` -> `Enable WiFi`. 
  - Receiver: Either power up and wait until `AUTO_WIFI_ON_INTERVAL` time has elapsed, or on a bound receiver, turn on receiver WiFi through the transmitter by selecting `WiFi Connectivity` -> `Enable Rx WiFi`. When in WiFi AP mode, red LED should pulse fast. 
- Connect to the device hotspot: `ExpressLRS TX` for TX module and `ExpressLRS RX` for receiver. password: `expresslrs`
- Navigate browser to http://10.0.0.1/
- Upload the firmware file

**Reference**: https://www.expresslrs.org/software/updating/wifi-updating/
