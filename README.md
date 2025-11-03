# Head-Gesture Wheelchair Control Prototype

This repository contains the two core scripts used for a research prototype that enables powered wheelchair control through head-tilt gestures. An IMU worn on the user’s head detects pitch and roll motion, which is processed on an ESP32 and transmitted over Bluetooth to a PC. MATLAB receives the gesture signal and outputs joystick-equivalent voltages through an NI-DAQ device to drive a powered wheelchair interface.

The aim of this system is to provide an alternative control method for users who cannot operate traditional joystick systems. This repo is being shared strictly for academic transparency and reference as part of the associated thesis submission.

There are only two files here, each performing one half of the control pipeline:

* `ESP32_code.ino` — reads IMU data, identifies tilt gestures, and broadcasts a control code via BLE
* `MATLAB_DAQ_Interface.m` — receives the BLE gesture code and sends voltage commands to the wheelchair through NI-DAQ

This is a proof-of-concept implementation meant for lab testing and evaluation. It is **not** intended for clinical use, unsupervised use, or deployment in real mobility devices without further safety systems, validation, and regulatory compliance.

### Hardware this was developed/tested with:
- ESP32-C6 microcontroller
- MPU6050 IMU
- PC with Bluetooth support
- NI USB-6008 DAQ (or equivalent NI device)
- Powered wheelchair with analog joystick interface (test bench setup, bench-mode only)

### Basic usage flow:
1. Upload the ESP32 firmware using Arduino IDE
2. Power the IMU/ESP module
3. Run the MATLAB script
4. After connection, type `start` in MATLAB to enable control
5. Head tilts translate to wheelchair commands (forward, reverse, left, right, neutral)

The system stays neutral by default and returns to neutral on errors, loss of BLE signal, or script failure, as a basic safety measure.

### Important note
This software is provided only as part of a research project. It should not be used on an actual mobility device by end-users without supervision, review, and more advanced safety systems. It is not medical-grade software and has not undergone formal certification or safety clearance.

Use at your own risk and only in controlled testing conditions.

