# AIR2216II / T1045II Motor Datasheet

Datasheet transcribed from [x500_motor_spec](./media/x500_v2_powertrain_ds.avif).

## Motor: AIR2216II

### Product drawing

| Dimension | Value |
|---|---:|
| Overall motor length | 42.5 +0.2/-0.2 mm |
| Motor body length | 31 +0.2/-0.2 mm |
| Front offset | 9.5 mm |
| Shaft-side offset | 6.5 mm |
| Shaft | M6 |
| Motor body diameter | 27.7 mm |
| Shaft diameter shown | 3 mm |
| Mounting holes | 4 x M3 |
| Mounting pattern dimensions shown | 16 mm and 19 mm |
| Cable length | 150 +/-3 mm |

### Specifications

| Parameter | Value |
|---|---:|
| KV | 920 |
| Rated voltage (LiPo) | 4S (4.2 V per cell) / 16 V |
| Idle current at 10 V | 0.8 A |
| Internal resistance | 115 +/-10 mOhm |
| Peak current, 180 s | 17 A |
| Weight, including cable | 64 +/-2 g |
| Maximum power, 180 s | 272 W |
| Package weight | Not specified |

## ESC: BLHeli S 20A

| Parameter | Value |
|---|---:|
| Size (L x W x H) | 26 x 14 x 5 mm |
| Rated voltage (LiPo) | 3-4S |
| Continuous current | 20 A |
| BEC | Not specified |
| Peak current, 10 s | 30 A |
| Weight, including cable | 21 g |
| Banana plug | 2.0 mm |
| Throttle signal frequency | 50-600 Hz |

## Propeller: T1045II

| Parameter | Value |
|---|---:|
| Type | Plastic polymer propeller |
| Size | 10 x 4.5 in (260 x 30 mm) |
| Weight, single propeller | 12.5 g |
| Material | Nylon + glass fiber |
| Surface treatment | Matte technology |
| Working temperature | -10 to 40 deg C |
| Storage temperature | 10 to 35 deg C |
| Storage humidity | 65 +/-20% RH |
| Optimum RPM | 6000-7000 RPM |
| Thrust limitation | 1.2 kg |

## AIR2216II Test Report

Test configuration: AIR2216II-KV920 motor with a T1045II propeller at 16 V. The source image lists the operating temperature as 80 deg C.

| Throttle | Voltage (V) | Thrust (g) | Torque (N*m) | Current (A) | RPM | Power (W) | Efficiency (g/W) |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 30% | 16 | 210 | 0.03 | 1.44 | 4042 | 23 | 9.12 |
| 35% | 16 | 259 | 0.04 | 1.87 | 4469 | 30 | 8.67 |
| 40% | 16 | 309 | 0.05 | 2.29 | 4855 | 37 | 8.45 |
| 45% | 16 | 373 | 0.05 | 2.86 | 5301 | 46 | 8.15 |
| 50% | 16 | 447 | 0.06 | 3.60 | 5780 | 58 | 7.76 |
| 55% | 16 | 536 | 0.08 | 4.53 | 6298 | 72 | 7.39 |
| 60% | 16 | 628 | 0.09 | 5.61 | 6800 | 90 | 7.01 |
| 65% | 16 | 729 | 0.10 | 6.78 | 7281 | 108 | 6.73 |
| 70% | 16 | 814 | 0.11 | 7.92 | 7679 | 126 | 6.44 |
| 75% | 16 | 906 | 0.12 | 9.20 | 8096 | 147 | 6.18 |
| 80% | 16 | 993 | 0.14 | 10.59 | 8468 | 169 | 5.88 |
| 85% | 16 | 1087 | 0.15 | 12.11 | 8867 | 193 | 5.65 |
| 90% | 16 | 1191 | 0.16 | 13.81 | 9257 | 219 | 5.43 |
| 95% | 16 | 1289 | 0.18 | 15.68 | 9675 | 249 | 5.18 |
| 100% | 16 | 1332 | 0.18 | 16.37 | 9857 | 260 | 5.13 |

> Note: The source states that motor temperature is the motor surface temperature after 10 minutes at 100% throttle. Bench-test data is for reference only; comparison with other motor types is not recommended.