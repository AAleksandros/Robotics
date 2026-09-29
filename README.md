# MyRobot

Python control code for the 4-DOF Dynamixel (AX-12A) robot arm, plus CAD parts.

```
Python/MyRobot.py   robot class + example usage
CAD/                SolidWorks parts (.SLDPRT)
DynamixelSDK/       ROBOTIS Dynamixel SDK (vendored, v4.0.0)
```

## Setup

Requires Python 3 with `numpy` (Anaconda already has it).

```bash
git clone https://github.com/AAleksandros/Robotics.git
cd Robotics/DynamixelSDK/python
pip install .
```

Check it worked:

```bash
python -c "import dynamixel_sdk; print('ok')"
```

If that fails with `ModuleNotFoundError`, your `pip` and `python` belong to different installs
(common on macOS with Anaconda). Use `python -m pip install .` instead, and run the robot code
with that same `python`.

## Connecting the robot

Set the serial port in `Python/MyRobot.py` (`DEVICENAME`, default `"COM5"`):

| OS      | Port looks like           | Find it with                        |
|---------|---------------------------|-------------------------------------|
| Windows | `COM3`                    | Device Manager → Ports (COM & LPT)  |
| macOS   | `/dev/tty.usbserial-XXXX` | `ls /dev/tty.usbserial*`            |
| Linux   | `/dev/ttyUSB0`            | `ls /dev/ttyUSB*`                   |

On Linux, you may need `sudo usermod -aG dialout $USER`, then log out and in again.

Motors 1–4 are the joints and motor 5 is the gripper. The baud rate is 1,000,000 and the
code uses Dynamixel protocol 1.0.

## Running

```bash
cd Python
python MyRobot.py
```

Both examples at the bottom of `MyRobot.py` are wrapped in `'''` quotes, so by default the
script runs nothing. Remove the quotes around one example to run it:

- **Example 1** reads the current joint angles and moves to a single pose.
- **Example 2** loops through a sequence of poses.

The joint angles are in degrees. The joint limits and motor offsets (`joint_limits`,
`joint_offsets`) are set in `__init__`, so check them against your robot before running.
