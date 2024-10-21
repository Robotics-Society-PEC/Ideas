# Autonomous RC Plane

In this guide, we’ll walk through setting up an **Autonomous RC Plane** using **ArduPilot**, combined with an **antenna tracker** for long-range communication. This system allows you to control and monitor your RC plane over great distances with real-time telemetry data and video feed, using an antenna tracker to maintain a strong link between the ground station and the plane.

## 1. Setting Up ArduPilot on Your RC Plane

ArduPilot is anutopilot platform that can manage the control, stabilization, and telemetry of your RC plane autonomously. Here's how to get started:

### 1.1 Install ArduPilot on Flight Controller

You need to install ArduPilot on a flight controller such as **Pixhawk** or **Matek**. The flight controller handles all aspects of controlling the plane, from stabilization to navigation.

- **ArduPilot Setup Instructions**: Follow the instructions on the official documentation to install ArduPilot firmware on your flight controller.
  - [ArduPilot Setup Documentation](https://ardupilot.org/plane/docs/common-loading-firmware-onto-pixhawk.html)

### 1.2 Configuring ArduPilot for RC Plane

Once ArduPilot is installed, configure it for fixed-wing flight. This involves calibrating the plane's control surfaces, configuring fail-safes, setting up GPS, and configuring telemetry.

- **Fixed-Wing Setup Documentation**: Follow the instructions to configure ArduPilot for your RC plane.
  - [ArduPilot Plane Configuration](https://ardupilot.org/plane/docs/first-flight-landing-page.html)

## 2. Adding Telemetry for Long-Range Communication

To control and monitor your plane over long distances, you'll need to set up a reliable telemetry link between the plane and your ground station.

### 2.1 Telemetry Radios

Use **900 MHz telemetry radios** (or a frequency allowed in your region) to send data from the plane to the ground station. This data includes GPS coordinates, attitude, speed, altitude, and more.

- **Telemetry Radio Setup**: Install telemetry radios on both the RC plane and the ground station.
  - [ArduPilot Telemetry Setup](https://ardupilot.org/copter/docs/common-3dr-radio-advanced-configuration-and-technical-information.html)

## 3. Using Antenna Tracker for Maintaining Communication

An antenna tracker helps maintain a stable communication link between the plane and the ground station by automatically pointing a directional antenna toward the plane as it moves.

### 3.1 Setting Up Antenna Tracker

ArduPilot supports **Antenna Tracker**, which can follow the plane's telemetry data (received via MAVLink) and point a directional antenna to ensure strong signal strength during flight.

### 3.2 Connecting Antenna Tracker with Ground Station

1. **Install Antenna Tracker Firmware**: Install the ArduPilot Antenna Tracker firmware onto a compatible controller such as **Pixhawk** or **APM**.

   - [Antenna Tracker Firmware Setup](https://ardupilot.org/antennatracker/)

2. **Connect Telemetry Radio**: Connect a telemetry radio to the antenna tracker. The tracker uses real-time telemetry data to follow the position of the RC plane.

3. **Calibrate the Antenna Tracker**: After installation, calibrate the tracker to ensure it can accurately track the plane. The calibration includes setting the pan and tilt limits and calibrating the GPS.

### 3.3 Antenna Types for Long-Range Communication

Choosing the right antenna is crucial for long-range communication. Here are two common options:

- **Patch Antenna**: A high-gain, directional antenna that works well for long distances but needs to be accurately pointed at the plane.
- **Yagi Antenna**: Offers even more gain than a patch antenna, making it ideal for extreme long-range communication.

### 3.4 Antenna Tracker Mount and Setup

- Mount the antenna on a stable surface (e.g., tripod) and ensure it has a clear line of sight to the plane.
- Use the **MAVLink protocol** to link the tracker to the ground station and the plane’s telemetry stream. This allows the tracker to follow the plane's movement in real-time.

- **Antenna Tracker Setup and Calibration**: [Antenna Tracker Documentation](https://ardupilot.org/antennatracker/)

## 4. Mission Planner: Ground Station Software

You’ll use **Mission Planner**, a ground station software, to control the RC plane and monitor its telemetry data in real-time. Mission Planner also supports antenna trackers, so you can manage the tracker from
