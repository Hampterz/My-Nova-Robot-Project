# Nova SM3 Interactive Manual Servo Calibration Tool

This utility replaces the original automated calibration routine with a safe, highly accurate, interactive Serial Monitor tool.

## Why Manual Calibration is Needed

Automated calibration routines sweep all 12 high-torque servos simultaneously based on rigid default values. Because manufacturing variances, 3D printing tolerances, 25T servo horn spline alignment, and physical assembly angles differ on every build, automated sweeps regularly:
- Command joints to completely wrong physical positions.
- Slam leg linkages into mechanical end-stops and 3D-printed frame panels.
- Stall servos under extreme mechanical strain, risking stripped gears and driver burnout.
- Cannot accommodate flipped servo orientations or custom horn positions.

This manual tool solves these problems by providing **isolated single-leg activation** and **tick-by-tick PWM micro-adjustments** directly from the Serial Monitor.

## How to Use (Serial Monitor at 19200 baud)

1. Upload `Nova-SM3-calibrate.ino` to the Teensy 4.0.
2. Open the Serial Monitor set to **19200 baud** with "Newline" line ending.
3. Power on servo rail via battery buck converter.
4. Use the commands below to calibrate each leg individually.

## Command Reference

| Command | Action |
|---|---|
| `leg1` | Activates Right Front leg (Servos 0, 1, 2) and turns off all other servos |
| `leg2` | Activates Left Front leg (Servos 3, 4, 5) and turns off all other servos |
| `leg3` | Activates Right Rear leg (Servos 6, 7, 8) and turns off all other servos |
| `leg4` | Activates Left Rear leg (Servos 9, 10, 11) and turns off all other servos |
| `<joint> <pwm>` | Jogs joint (0=Coxa, 1=Femur, 2=Tibia) to exact PWM value (e.g. `1 350`) |
| `<joint> min` | Safely tests configured minimum limit |
| `<joint> max` | Safely tests configured maximum limit |
| `<joint> home` | Returns joint to current home position |
| `done` | Prints complete 12-servo calibration table ready to paste into `NovaServos.h` |
