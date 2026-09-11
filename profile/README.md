# ROSMicroPy

[ROSMicroPy](https://github.com/ROSMicroPy/ROSMicroPy) brings MicroPython and micro-ROS together so ESP32-class devices can participate in a ROS 2 system while being programmed in Python. Start with the core project, then explore the examples, libraries, hardware support, and development tools in the [ROSMicroPy organization](https://github.com/ROSMicroPy/).

## Load your board now

**[Open the ROSMicroPy Web Loader →](https://rosmicropy.github.io/ROSMicroPy/)**

Install ROSMicroPy Core directly from the browser using the project's GitHub Pages installer.

1. Connect your board with a data-capable USB cable. Back up MicroPython files you want to keep and close any serial monitors connected to the board.
2. Open the loader in desktop Chrome, Edge, or another browser with Web Serial support.
3. Connect through the installer, choose your board's serial port, and follow the prompts to install the matching firmware.
4. Follow the [user guide](https://github.com/ROSMicroPy/ROSMicroPy/blob/main/readme_docs/user-guide.md) and [startup and bridge configuration](https://github.com/ROSMicroPy/ROSMicroPy/blob/main/readme_docs/configuration-and-startup.md) to connect the device through a micro-ROS agent to ROS 2.

The live loader currently offers **RMP Core Generic (ESP32)** and **RMP Core S3 (ESP32-S3)** development firmware. Its [firmware manifest](https://rosmicropy.github.io/ROSMicroPy/manifest.json) lists the available builds; other board configurations in the source repository are not necessarily available through the web installer.

## Core platform — start here

| Repository | Purpose | Where to begin |
| --- | --- | --- |
| [ROSMicroPy](https://github.com/ROSMicroPy/ROSMicroPy) | Main firmware, integrated Python ROS interface, board configurations, build tools, documentation, and web loader. | [Load a board](https://rosmicropy.github.io/ROSMicroPy/), then use the [rclpy guide](https://github.com/ROSMicroPy/ROSMicroPy/blob/main/readme_docs/rclpy-guide.md) and [publisher/subscriber examples](https://github.com/ROSMicroPy/ROSMicroPy/tree/main/examples/rclpy_pubsub). |

New applications should use the integrated `rclpy` interface. It implements a subset of desktop ROS 2's Python API; the older direct ROSMicroPy API is deprecated for application development.

## Robot and messaging examples

These standalone examples use the older direct ROSMicroPy API. They illustrate message flow and hardware integration, but should be reviewed and adapted before use with current firmware. Start new applications with the core repository's `rclpy` examples linked above.

| Repository | Purpose |
| --- | --- |
| [rmp_example-twisted](https://github.com/ROSMicroPy/rmp_example-twisted) | `Twist` message publisher and subscriber examples for the `turtle1/cmd_vel` topic. |
| [rmp_example-maqueen_base](https://github.com/ROSMicroPy/rmp_example-maqueen_base) | Maqueen robot base example: consumes joystick velocity and attachment commands to control the drive and servo through its hardware library. |
| [rmp_example-joystickBit_V2](https://github.com/ROSMicroPy/rmp_example-joystickBit_V2) | Joystick:bit V2 teleoperation example: publishes velocity and attachment commands for a robot such as the Maqueen base. |

## Reusable control, sensing, and web libraries

| Repository | Purpose | Integration notes |
| --- | --- | --- |
| [mpylib_MotorControl](https://github.com/ROSMicroPy/mpylib_MotorControl) | Generic MicroPython motor interfaces with STEP/DIR, PWM servo, and PWM/ESC drivers. | Includes a `mip` package manifest and a component contract; applications supply pins and configuration. |
| [mpylib_DistanceSensor](https://github.com/ROSMicroPy/mpylib_DistanceSensor) | Generic MicroPython distance-sensor interface with HC-SR04 ultrasonic and VL53L4CD time-of-flight drivers. | Includes a `mip` package manifest; the VL53L4CD implementation uses native MicroPython I2C. |
| [mpylib_micropyserver](https://github.com/ROSMicroPy/mpylib_micropyserver) | Lightweight HTTP server for MicroPython device endpoints and web interfaces. | Fork of MicroPyServer; also referenced by the SmartStepper application. |
| [mpylib_ExecutionEngine](https://github.com/ROSMicroPy/mpylib_ExecutionEngine) | Event-driven workflow engine with success/failure routing, sequential or parallel child tasks, and publish/subscribe events. | Source and usage examples are present, but no README. It imports `threading`, `typing`, and `uuid`; MicroPython compatibility needs evaluation. |

## Device applications and browser tools

| Repository | Purpose | Current scope |
| --- | --- | --- |
| [device-smartstepper](https://github.com/ROSMicroPy/device-smartstepper) | Stepper-control application combining MotorControl, an HTTP API, status reporting, and a JSON form layout. | Its README describes integration with MicroPyServer and a WebTester client. |
| [ROSMicroPy-WebTester](https://github.com/ROSMicroPy/ROSMicroPy-WebTester) | Intended browser testing/control companion referenced by SmartStepper. | Empty repository at the time of review; no implementation is available here yet. |

## Hardware driver forks

These repositories provide hardware-specific drivers or reference implementations. Their target runtimes differ, so organization membership alone does not imply compatibility with ROSMicroPy firmware.

| Repository | Hardware and role | Runtime / scope |
| --- | --- | --- |
| [mpylib_TMC5160](https://github.com/ROSMicroPy/mpylib_TMC5160) | Trinamic TMC5160 motion-controller library. | MicroPython driver fork. |
| [tmc5160](https://github.com/ROSMicroPy/tmc5160) | ShushEngine driver for the Trinamic TMC5160. | Python fork whose README targets Raspberry Pi. |
| [mks_servo42c](https://github.com/ROSMicroPy/mks_servo42c) | Driver for the MKS SERVO42C stepper driver board. | Python driver fork for board version 1.0. |
| [QMI8658](https://github.com/ROSMicroPy/QMI8658) | QMI8658C six-axis accelerometer and gyroscope helper library. | CircuitPython fork with Adafruit Bus Device and Register dependencies. |

## Vision and embedded AI

| Repository | Purpose | Relationship |
| --- | --- | --- |
| [GVAIV2_Build](https://github.com/ROSMicroPy/GVAIV2_Build) | Build workspace and hardware assets for Grove Vision AI V2 and related camera work. Includes a Docker toolchain, AT-command documentation, camera CAD, and a training-camera application. | Its [build container](https://github.com/ROSMicroPy/GVAIV2_Build/tree/main/SSCMA-Micro_BuildContainer) checks out pinned revisions of the organization's two vision forks below and builds ESP32-S3 or Grove Vision AI V2 firmware. |
| [SSCMA-Micro](https://github.com/ROSMicroPy/SSCMA-Micro) | Embedded C++ inference framework for SenseCraft Model Assistant, including image processing, model inference, and AT-command interaction. | Fork used by the vision build workspace. |
| [sscma-example-we2](https://github.com/ROSMicroPy/sscma-example-we2) | Model deployment examples and firmware support for Himax WiseEye2 / Grove Vision AI V2. | Fork used by the vision build workspace for the Grove V2 target. |

## ROS integration and type-generation development

| Repository | Purpose | Development notes |
| --- | --- | --- |
| [micro_ros_espidf_component](https://github.com/ROSMicroPy/micro_ros_espidf_component) | micro-ROS integration component and examples for Espressif ESP-IDF. | Organization fork for integration work. The core project's current [submodule configuration](https://github.com/ROSMicroPy/ROSMicroPy/blob/main/.gitmodules) points to the upstream micro-ROS repository. |
| [ROSMicroPy-TypeGen](https://github.com/ROSMicroPy/ROSMicroPy-TypeGen) | Proof of concept for parsing ROS `.msg` definitions into Python classes and data-transfer instructions. | Research/prototype code; its README explicitly says it is incomplete and does not support constants or arrays. For current firmware behavior, see the core project's [type-support documentation](https://github.com/ROSMicroPy/ROSMicroPy/blob/main/readme_docs/type-support-and-serialization.md). |

## Organization and project navigation

| Repository | Purpose | Current scope |
| --- | --- | --- |
| [.github](https://github.com/ROSMicroPy/.github) (this repository) | Organization profile and grouped catalog of ROSMicroPy and its supporting components. | This guide lives in `profile/README.md` so GitHub displays it on the organization homepage. |

## Catalog scope

Reviewed on **2026-09-10** against the [public organization repository inventory](https://api.github.com/orgs/ROSMicroPy/repos?per_page=100&type=all). All **20 public repositories** returned by GitHub are included above. Classifications are based on repository READMEs and, where documentation is missing, source files and file trees. Fork labels come from GitHub metadata. This is a navigation guide, not a claim that every component has been tested together; repository contents and installer builds may change.
