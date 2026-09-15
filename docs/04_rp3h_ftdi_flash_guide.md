# RP3-H FTDI Firmware Upgrade Guide

This guide outlines how to upgrade firmware on the **RadioMaster RP3-H Receiver** via USB-to-UART FTDI adapter. 

## Step 1: Wire Up

Connect the receiver pins to FTDI adapter as follows:

| RP3-H Receiver Pin | FTDI / USB-TTL Adapter Pin |
| :--- | :--- |
| **TX** | **RX** |
| **RX** | **TX** |
| **5V** | **5V** |
| **GND** | **GND** |

> ⚠️ Ensure physical voltage selector jumper on FTDI adapter is set to **5V**.


## Step 2: Boot into Hardware Bootloader Mode

- Press and hold boot button on the RP3-H receiver while plugging the FTDI adapter into the PC's USB port
- Status LED on the receiver should show solid red to indicate bootloader mode. 
- Release the button

## Step 3: Flash Firmware via ExpressLRS Configurator

- Launch the _ExpressLRS Configurator_ application
- Set the following options:
   * Release: _Match the version on the transmitter_
   * Device Category: `RadioMaster 2.4 GHz`
   * Device: `RadioMaster RP3-H Diversity 2400 RX`
   * Flashing Method: `UART`
- Select the port corresponding to the plugged-in FTDI adapter
- Configure personalized operational variables:
   * Set _Binding Phrase_: `X500TX12RP3H` (match the transmitter setting)
   * Set _Regulatory Domain_ settings: LBT
- Click the _Flash_ button


## Step 4: Verify

* On success, the receiver will automatically reboot. The status LED will shift to a slow, regular flash sequence, indicating it is searching for its bound transmitter.
* Unplug the FTDI adapter, remove the jumper wires, and reconnect RP3-H back into the `TELEM2` port of the flight controller.
