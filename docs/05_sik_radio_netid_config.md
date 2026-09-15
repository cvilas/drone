# Assigning a SiK radio pair a unique network ID

This procedure assigns the air and ground radios the same non-default SiK
`NETID`. It is intended for a Pixhawk 6C running PX4, QGroundControl (QGC), and
a Linux ground-station computer.

> ⚠️ `NETID` separates nearby SiK networks, but it is not a secure
> binding or an encryption key. Any compatible radio with the same RF settings
> and `NETID` can join the network. Use it to avoid accidental cross-connection,
> not to protect sensitive traffic.

> ⚠️ Do not change air data rate, UART baud rate, `ECC`, etc just to bind the pair. 
> These settings must match at both ends and affect compatibility and link performance.
> Specifically, air data rate should be greater than UART baud rate to avoid buffer 
> overflows. Default air data rate of 64kbps offers good compromise between range and 
> reliability.

`NETID` is set by SiK register `S3` and valid range of `1 - 255`. The factory default is often `25`; the example below uses `142`.

## Before starting

1. Remove the propellers or otherwise make the vehicle safe on the bench.
2. Connect the air radio to the Pixhawk 6C `TELEM1` port.
3. Power the Pixhawk and air radio, then connect the ground radio to the Linux
   computer by USB.
4. Confirm the pair currently links and QGC can connect to the vehicle.
5. Fully close QGC so that it releases the ground radio's serial port.

This method uses the working radio link to configure both radios from the ground
radio. No USB-to-UART adapter is required.

## Configure both radios

### 1. Find the ground radio serial port

Prefer the stable device name shown by:

```bash
ls -l /dev/serial/by-id/
```

It normally points to a device such as `/dev/ttyUSB0` or `/dev/ttyACM0`. If the
port is not accessible, add your user to the serial-port group (commonly
`dialout`), log out, and log back in:

```bash
sudo usermod -aG dialout "$USER"
```

### 2. Open a serial terminal

Install `picocom` if necessary, then open the radio at its current serial rate.
`57600` is the normal default:

```bash
picocom --baud 57600 /dev/serial/by-id/YOUR_RADIO_DEVICE
```

MAVLink traffic may appear as unreadable characters. That is expected.

### 3. Enter SiK command mode

1. Do not type anything for at least one second.
2. Type `+++` without pressing Enter.
3. Do not type anything for at least one more second.
4. Wait for the radio to reply `OK`.

If `OK` does not appear, close QGC again, check the port and baud rate, and
repeat the guard-time sequence carefully.

### 4. Inspect both radios

Press Enter after each command:

```text
ATI5
RTI5
```

`ATI5` displays the local (ground) radio settings. `RTI5` displays the remote
(air) radio settings over the current link. Check that both reports contain an
`S3: NETID=...` line. Also confirm that the firmware versions and all required
link settings match before making changes.

### 5. Set and save the new NETID

Replace `142` with the value selected for this pair:

```text
ATS3=142
RTS3=142
ATS3?
RTS3?
RT&W
AT&W
```

The two query commands must both return the selected value. `RT&W` saves the
air radio first, and `AT&W` saves the ground radio. Do not power either radio
off until both write commands have completed.

Exit `picocom` with `Ctrl+A`, then `Ctrl+X`. Power-cycle both radios so the new
network ID takes effect.

## Verify PX4 and QGroundControl

1. Start QGC after both radios have restarted.
2. Confirm that QGC connects to the vehicle through the ground radio.
3. In **Vehicle Setup > Parameters**, verify:
   - `MAV_0_CONFIG` is `TELEM 1`.
   - `SER_TEL1_BAUD` matches the SiK `SERIAL_SPEED`. For the usual SiK
     `S1: SERIAL_SPEED=57`, select `57600 8N1` in PX4.
4. Reboot the Pixhawk if either PX4 parameter was changed.
5. Disconnect and reconnect ground-radio USB, then confirm QGC reconnects.

LED meanings vary by radio vendor, so use a successful QGC vehicle connection
as the final test rather than relying only on LED color or blink pattern.

## Confirm separation from another pair

For a bench test, power down your newly configured air radio and power a
different air radio that still uses another `NETID`. Your configured ground
radio must not establish a vehicle connection through that radio. Restore the
normal air radio and confirm QGC reconnects.

## Recovery when the pair no longer links

If `RTI5` or `RTS3` fails, the radios are not currently compatible over the air.
Configure each radio locally instead:

- Configure the ground radio through its USB serial port with `ATS3=<value>`,
  `AT&W`, and a power cycle.
- Connect the air radio with a USB-to-UART cable that matches the radio
  manufacturer's connector pinout and voltage requirements. Configure the same
  value locally with `ATS3=<value>`, `AT&W`, and a power cycle.

Do not guess the air-radio power or UART pinout. Reversed power, a 5 V UART
signal on a 3.3 V input, or incorrectly crossed TX/RX wiring can damage it.

## References

- [PX4 SiK Radio documentation](https://docs.px4.io/main/en/telemetry/sik_radio.html)
- [SiK advanced configuration and AT commands](https://ardupilot.org/copter/docs/common-3dr-radio-advanced-configuration-and-technical-information.html)
- [QGroundControl firmware loading](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/firmware.html)