# Mission Control for Rocket with ArduPilot

Now that you've made the rocket work with ArduPilot, it's time to focus on the ground station. While ArduPilot's ground stations like Mission Planner are great for drones and planes, they lack certain features for rockets, particularly in-depth telemetry display and tracking. To make this work for rockets, you'll need to modify the source code of the Mission Planner ground station, which is written in C++. Additionally, we'll cover setting up a high-performance radio link using ExpressLRS (ELRS), selecting an antenna, and using an antenna tracker for better range and coverage.

## 1. Modifying Mission Planner for Rockets

Mission Planner is a ground station software primarily built for managing drones and planes. Since it doesn't have specific features for rocket missions, such as vertical trajectory visualization or in-depth telemetry related to altitude, thrust, or apogee detection, you'll need to modify its source code to suit your rocket's needs.

### Steps to Modify Mission Planner:

1. **Set Up Development Environment**:

   - Mission Planner is written in C#. To start, clone the Mission Planner source code from the GitHub repository.
   - Follow the guide to set up the development environment:
     - [Mission Planner Development Documentation](https://ardupilot.org/dev/docs/building-mission-planner.html)

2. **Key Areas to Modify**:

   - **Trajectory Tracking**: Modify the 3D trajectory visualization to better represent vertical rocket flights.
   - **Custom Telemetry**: Add fields for high-altitude telemetry, apogee detection, and thrust data visualization.
   - **Launch and Ascent Mode**: Create a custom user interface and telemetry mode specific to rocket launches, focusing on vertical flight and sensor data during boost and coast phases.

3. **Compiling and Testing**:
   - After making the necessary changes, compile the source code and test the updated Mission Planner with simulated rocket missions using **SITL (Software in the Loop)** in ArduPilot.

## 2. Using ExpressLRS (ELRS) for Rocket-to-Ground Station Communication

To reliably send telemetry and receive commands from the rocket to the ground station, a high-performance radio link is essential. **ExpressLRS (ELRS)** is an open-source, long-range radio control system that supports **MAVLink** out of the box, making it an ideal choice for your mission control system.

### Setting Up ELRS for MAVLink:

- ELRS can handle both control signals and telemetry data, including MAVLink messages.
- Use an ELRS receiver on the rocket and a compatible ELRS transmitter on the ground station for long-range communication.

### ELRS Documentation:

- [ExpressLRS Official Documentation](https://www.expresslrs.org/)
- [Using ELRS with MAVLink](https://www.expresslrs.org/software/mavlink/?h=mavlink)

## 3. Selecting an Antenna and Antenna Tracker

For long-range missions like rockets, selecting the right antenna and antenna tracking system is critical to maintain a strong link between the rocket and the ground station, especially at high altitudes.

### Choosing an Antenna:

1. **Patch Antenna**: Ideal for long-range communication but requires precise pointing. A patch antenna is great for directional communication.

   - **Advantages**: High gain, directional focus for long distances.
   - **Disadvantages**: Needs to be accurately pointed at the rocket throughout the flight.

2. **Yagi Antenna**: A high-gain directional antenna often used in high-power radio setups. It's suitable for maintaining long-range links over tens of kilometers.
   - **Advantages**: High gain, ideal for long-range missions.
   - **Disadvantages**: Requires precise pointing and a stable mount.

### Antenna Tracker:

An **Antenna Tracker** helps you maintain a solid link with the rocket by automatically pointing the antenna at the rocket in real-time as it ascends and descends. It significantly improves range and signal strength over the entire flight.

1. **ArduPilot Antenna Tracker**: ArduPilot supports antenna trackers, which work by following MAVLink telemetry data and adjusting the antenna direction accordingly.

   - [ArduPilot Antenna Tracker Documentation](https://ardupilot.org/antennatracker/index.html)

2. **Custom Antenna Tracker**: If using an external tracker, ensure it can interface with MAVLink or similar telemetry data to adjust direction automatically.

### Suggested Antenna Tracker Systems:

- **MFD Antenna Tracker**: A reliable option with MAVLink support for long-range tracking.
- **3D Robotics Antenna Tracker**: Another option with full integration into the ArduPilot ecosystem.

---

## Summary

- Modify the **Mission Planner** ground station software to better suit rocket missions by adding features like vertical trajectory tracking, rocket-specific telemetry fields, and launch phase modes.
- Set up **ExpressLRS (ELRS)** for high-performance radio communication between the rocket and ground station, supporting MAVLink for telemetry and commands.
- Choose the right **antenna** (like a patch or Yagi) for long-range communication, and use an **antenna tracker** to maintain signal strength and coverage throughout the rocket's flight.
