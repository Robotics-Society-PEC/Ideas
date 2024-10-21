# Controlling RC Car Over WiFi Using ESP32 and PlatformIO

## Overview

If you've had the opportunity to build an RC car in a workshop, you might have noticed that it's usually controlled via Bluetooth with a mobile application or with a transmitter.

## Problems

There are certain problems with these two approaches:

1. **Only works with Android:** The mobile application approach typically only works with Android phones and not with iOS. Moreover, these applications often do not provide speed control and do not use a standard protocol. This becomes an issue if, in the future, you want to control the robot autonomously through your computer.

2. **Requires a Receiver:** When using a transmitter, you also need a receiver to receive the signals, and then you have to process them. This adds additional cost and doesn't make much sense for such low-range applications.

> **Note:**
> Check out this [library](#) that I made for reading different communication protocols used by these receivers. It is a basic protocol parser that reads the headers and performs parity checks, ultimately providing the final decoded values.

## Solution

The solution is to use WiFi as a communication protocol, specifically utilizing UDP to receive control packets. UDP provides low-latency communication suitable for control signals.

By receiving control packets over UDP, we can parse them using our custom parser, allowing for efficient and flexible control of the RC car. This method eliminates the need for specialized receivers and enables control from various devices, including computers and iOS devices.

For generating the control packets, we can use an **ELRS (ExpressLRS)-based transmitter**. ELRS is an open-source, high-performance radio control link. A Pull Request in the ExpressLRS repository details how to implement UDP packet transmission using an ELRS transmitter:

- [ExpressLRS Pull Request #2444](https://github.com/ExpressLRS/ExpressLRS/pull/2444)

This PR explains how to send control data over UDP using an ELRS-based transmitter, enabling you to control the RC car over WiFi without the need for additional receivers or relying on Android-only applications.

## Implementation Steps on ESP32
To control your RC car over WiFi using an ESP32, you can follow these steps:

**1. Set Up WiFi Connection:** Configure the ESP32 to connect to your local WiFi network. This connection will allow the ESP32 to receive control signals over the network.

**2. Implement UDP Communication:** Utilize the UDP protocol to receive control packets. UDP is ideal for real-time applications like controlling an RC car due to its low-latency communication.

**3. Receive Control Packets:** Set up the ESP32 to listen for incoming UDP packets on a specific port. Ensure that your transmitter is sending packets to the correct IP address and port of the ESP32.

**4. Develop a Data Parser:** Implement a parser that can decode the received UDP packets. The parser should interpret the data format used by your ELRS-based transmitter and extract control commands such as throttle, steering, and other functions.