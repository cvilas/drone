# Roadmap

## Drone build

- [ ] Build the dev kit
  - [x] Pixhawk: Flash custom PX4 firmware with CRSF support
  - [x] RP3-H: Make cable harness to plug into `TELEM2`
  - [x] RP3-H: Upgrade firmware on RP3-H and TX12 and set unique binding code
  - [x] TX12: Configure to receive telemetry info (RSSI, battery level) on the screen
  - [x] SiK: Upgrade firmware on air and ground units
  - [x] Mount FC, RP3-H, SiK on frame
  - [x] Charge battery
  - [x] Mount battery
- [ ] Configure PX4: https://docs.px4.io/main/en/frames_multicopter/holybro_x500v2_pixhawk6c
  - [ ] Install px4 stable version 1.17, not master
  - [ ] Follow [PX4 Utimate Tuning Guide](https://youtube.com/playlist?list=PLFPBjpbd5xKRECBsvI3MbmsS8NQJ8l8L9&si=fXR6GNuO4HAsD2xE)
    - [x] Set airframe
    - [x] Set actuator mappings
    - [x] Calibrate sensors
    - [x] Calibrate radio
    - [ ] Setup switches
      - [x] Flight Modes (position, altitude, stabilised)
      - [ ] Kill switch
      - [ ] Arm switch
    - [ ] ESC
    - [ ] Battery
    - [ ] Safety
    - [ ] Document all settings
  - [ ] Enable safety switch on GPS dome
  - [ ] Document safety switch LED indications
  - [ ] Document GPS dome LED status indications
  - [ ] Move UX (LED indications, sounds) to a new document
  - [ ] Power up test (no props)
- [ ] First flight with RCC
  - [ ] basic flying: https://docs.px4.io/main/en/flying/basic_flying_mc
  - [ ] ??
  - [ ] Auto tune
- [ ] Flight with QGC
  - [ ] ??
- Yak shaving
  - [ ] Configure unique binding between SiK air and ground modules
  - [ ] Configure SiK for high baud rate that is reliable
  - [ ] How to use ELRS for telemetry into QGC (alternative to SiK. Rationale: robust to RF noise)

## Software development

- Deep dive into SIH & Hawkeye: https://docs.px4.io/main/en/sim_sih/
- ???

### Familiarisation

- [ ] Read PX4 logs
- [ ] Define a mavlink message
- [ ] Develop a pub/sub loop using mavsdk
- [ ] Make a trivial modification to PX4 firmware. Build artifacts, deploy on autopilot
- [ ] Ways to integrate PX4-Autopilot, MAVSDK and MAVLINK into monorepo or superbuild
- [ ] How does `make` and `cmake` interact within PX4-Autopilot? They seem to be doing similar yet different things.
