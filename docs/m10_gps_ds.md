# M10 GPS V1

![](./media/m10_gps.avif)
![](./media/m10_pinout.avif)
![](./media/m10_dimensions.avif)

> **Firmware Support for M10 GPS:** PX4 1.14, ArduPilot 4.3, INAV 5.0.0, Betaflight 4.3.0 or newer is required.

## Specification

<table data-full-width="false"><thead><tr><th width="255.87557603686633"></th><th width="269">Holybro M10 GPS</th><th width="268">Holybro M9N GPS</th></tr></thead><tbody><tr><td><strong>GNSS Receiver</strong></td><td>Ublox M10</td><td>Ublox M9N</td></tr><tr><td><strong>Number of Concurrent GNSS</strong></td><td>Up to 4 GNSS<br>- BeiDou<br>- Galileo<br>- GLONASS<br>- GPS<br>- QZSS</td><td>Up to 4 GNSS<br>- BeiDou<br>- Galileo<br>- GLONASS<br>- GPS<br>- QZSS</td></tr><tr><td><strong>Frequency Band</strong></td><td>- GPS L1<br>- Galileo E1<br>- GLONASS L1<br>- BeiDou B1<br>- SBAS L1<br>- QZSS L1</td><td>- GPS L1<br>- Galileo E1<br>- GLONASS L1<br>- BeiDou B1<br>- SBAS L1<br>- QZSS L1</td></tr><tr><td><strong>Compass</strong></td><td>IST8310</td><td>IST8310</td></tr><tr><td><strong>Output Protocol</strong></td><td>- UBX (U-blox)<br>- NMEA</td><td>- UBX (U-blox)<br>- NMEA</td></tr><tr><td><strong>Accuracy</strong></td><td>2.0m CEP</td><td>1.5m CEP</td></tr><tr><td><strong>Nav. Update Rate</strong> </td><td>Up to 25 Hz (single GNSS),<br>Up to 10 Hz (4 concurrent GNSS)</td><td>Up to 25 Hz (4 concerrent GNSS)</td></tr><tr><td><strong>GNSS Augmentation System</strong></td><td>EGNOS, GAGAN, MSAS and WAAS<br>QZSS: L1S</td><td>EGNOS, GAGAN, MSAS and WAAS<br>QZSS: L1S </td></tr><tr><td><strong>Default Baud Rate</strong></td><td>115200</td><td>115200</td></tr><tr><td><strong>Input Voltage</strong> </td><td>4.7-5.2V</td><td>4.7-5.2V</td></tr><tr><td><strong>Port Type</strong></td><td>JST-GH-10P</td><td>JST-GH-10P</td></tr><tr><td><strong>Antenna</strong></td><td>25 x 25 x 4 mm ceramic patch antenna</td><td>25 x 25 x 4 mm ceramic patch antenna</td></tr><tr><td><strong>Power consumption</strong></td><td>Less than 200mA @ 5V</td><td>Less than 200mA @ 5V</td></tr><tr><td>Water Resistance Rating</td><td>IP67 (V2 only)</td><td>IP67 (V2 only)</td></tr><tr><td><strong>Operating Temperature</strong></td><td>-40~80C</td><td>-40~80C</td></tr><tr><td><strong>Dimension (V1)</strong></td><td>φ50 x14.4 mm</td><td>φ50 x14.4 mm</td></tr><tr><td><strong>Dimension (V2)</strong></td><td><strong>φ51 x18.5 mm</strong></td><td><strong>φ51 x18.5 mm</strong></td></tr><tr><td><strong>Weight (V1)</strong></td><td>32g </td><td>32g </td></tr><tr><td><strong>Weight (V2)</strong></td><td>36.8g</td><td>36.8g</td></tr><tr><td><strong>Cable Length</strong></td><td>26cm (42cm cable purchase separately)</td><td>26cm (42cm cable purchase separately)</td></tr><tr><td><strong>Other</strong></td><td>- Tri-color LED<br>- Onboard Buzzer<br>- Safety Switch<br>- LNA MAX2659ELT+ RF Amplifier<br>- Rechargeable Farah capacitance<br>- Low noise 3.3V regulator</td><td>- Tri-color LED<br>- Onboard Buzzer<br>- Safety Switch<br>- LNA MAX2659ELT+ RF Amplifier<br>- Rechargeable Farah capacitance<br>- Low noise 3.3V regulator</td></tr></tbody></table>

* **M8N:** Concurrent reception of up to 3 GNSS (GPS, Galileo, GLONASS, BeiDou)

## LED Indications

- **Fix (3D Fix)**
  - Off - No 3D Fixed
  - Blink/Solid On - 3D fixed
- **Switch**
  - Slow blinking - system is ready. press the safety switch to enable output to the motors.
  - Intermittent fast blinking - safety switch has been pressed, motors and servos are able to move once the vehicle is armed.
  - Solid – Vehicle is armed
- **Status LED**
  - **[Solid Blue]** Armed, No GPS Lock: Indicates vehicle has been armed and has no position lock from a GPS unit. When vehicle is armed, PX4 will unlock control of the motors, allowing you to fly your drone. As always, exercise caution when arming, as large propellers can be dangerous at high revolutions. Vehicle cannot perform guided missions in this mode.
  - **[Pulsing Blue]** Disarmed, No GPS Lock: Similar to above, but your vehicle is disarmed. This means you will not be able to control motors, but all other subsystems are working.
  - **[Solid Green]** Armed, GPS Lock: Indicates vehicle has been armed and has a valid position lock from a GPS unit. When vehicle is armed, PX4 will unlock control of the motors, allowing you to fly your drone. As always, exercise caution when arming, as large propellers can be dangerous at high revolutions. In this mode, vehicle can perform guided missions.
  - **[Pulsing Green]** Disarmed, GPS Lock: Similar to above, but your vehicle is disarmed. This means you will not be able to control motors, but all other subsystems including GPS position lock are working.
  - **[Solid Purple]** Failsafe Mode: This mode will activate whenever vehicle encounters an issue during flight, such as losing manual control, a critically low battery, or an internal error. During failsafe mode, vehicle will attempt to return to its takeoff location, or may simply descend where it currently is.
  - **[Solid Amber]** Low Battery Warning: Indicates your vehicle's battery is running dangerously low. After a certain point, vehicle will go into failsafe mode. However, this mode should signal caution that it's time to end this flight.
  - **[Blinking Red]** Error / Setup Required: Indicates that your autopilot needs to be configured or calibrated before flying. Attach your autopilot to a Ground Control Station to verify what the problem is. If you have completed the setup process and autopilot still appears as red and flashing, there may be another error.