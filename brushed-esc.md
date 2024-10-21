# Brushed ESC (Electronic Speed Controller)

Motor driver control using an ESP32 is great, but wouldn’t it be even better if you had an ESC that you could directly connect to a PWM receiver and have it work out of the box? This guide will walk you through designing a brushed ESC that can accept PWM signals to control the speed of a DC motor. We'll dive into control structures, PID loop tuning, cascaded PID loops, how to measure motor speed using a shunt resistor, integrating these techniques into a closed-loop system for optimal motor control, and how to create a GUI for configuring the ESC.

## 1. Basic Control Structure

In a brushed ESC, the primary goal is to control the speed of a DC motor based on a PWM input signal. The PWM signal is typically generated from a remote control, microcontroller, or other devices. The ESC interprets this signal and adjusts the motor speed accordingly.

The basic structure involves:
- **PWM Signal Input**: Accept the PWM signal as a reference for motor speed.
- **Motor Driver (H-Bridge)**: Control the voltage applied to the motor using an H-Bridge to control motor speed and direction.
- **Feedback**: Use a sensor (e.g., current sensing via a shunt resistor) to measure the motor's actual speed.
- **PID Control**: Implement a PID controller to adjust the motor's input to match the desired speed based on feedback.

## 2. PID Loop

The **Proportional-Integral-Derivative (PID)** loop is the heart of the control system. It continuously adjusts the motor's speed to minimize the difference between the desired speed (set by the PWM signal) and the actual motor speed.

- **Proportional (P)**: Corrects the error based on the magnitude of the difference.
- **Integral (I)**: Corrects for past errors by accumulating over time.
- **Derivative (D)**: Predicts future errors based on the rate of change.

The basic PID loop adjusts the motor’s speed to track the desired value by dynamically changing the PWM duty cycle.

### MATLAB Reference for PID Controller:
To learn more about implementing a PID controller, check out the following MATLAB resource:
- [MATLAB - PID Controller Overview](https://in.mathworks.com/help/control/ug/proportional-integral-derivative-pid-controllers.html)

## 3. Cascade PID Loop

A **Cascade PID Loop** is a more advanced control method where two PID controllers work together in a nested configuration. It is especially useful in applications where two control variables are interrelated, such as controlling both speed and torque in a motor.

- **Outer Loop (Speed Control)**: This PID loop controls the motor speed, using the reference speed from the PWM signal and feedback from the motor’s speed sensor.
- **Inner Loop (Current/Voltage Control)**: This loop controls the current or voltage applied to the motor to ensure the motor’s speed tracks the desired value set by the outer loop.

The advantage of a cascaded loop is its ability to react more effectively to disturbances, improving the stability and precision of the motor control.

### MATLAB Reference for Cascade PID Controller:
For a detailed explanation of cascaded PID loops, refer to this MATLAB resource:
- [MATLAB - Cascade PID Control Example](https://in.mathworks.com/help/control/ug/designing-cascade-control-system-with-pi-controllers.html)

## 4. Measuring Motor Speed Using a Shunt Resistor

To measure the motor's speed, you can use a **shunt resistor** to measure the current flowing through the motor. Here's how you can do it:

- **Place the Shunt Resistor in Series**: Position the shunt resistor in series with the motor to measure the current flowing into the motor.
- **Measure the Voltage Drop**: Measure the voltage drop across the shunt resistor using an ADC (Analog-to-Digital Converter) on your microcontroller.
- **Convert to Speed**: Since the current is proportional to the motor’s torque (and thus indirectly related to its speed), you can estimate the motor’s speed based on the current.

This feedback is then fed into the **inner PID loop** (current/voltage control) to stabilize the motor’s operation.

## 5. Cascaded Control Structure for Motor Speed Control

Here’s how to implement a cascaded PID control structure:

### Outer PID Loop (Speed Control):
- **Input**: Desired speed from the PWM signal.
- **Feedback**: Motor speed estimated from the shunt resistor.
- **Output**: Set point for the inner PID loop (current control).

### Inner PID Loop (Current/Voltage Control):
- **Input**: Set point from the outer loop.
- **Feedback**: Current or voltage measured across the motor using the shunt resistor.
- **Output**: Adjust the PWM duty cycle to control the motor’s speed.

## 6. Tuning the PID Loops

Proper tuning of the PID controllers is crucial to achieve stable and accurate control. Start by tuning the inner current loop first, then the outer speed loop. Tuning can be done manually by adjusting the **P**, **I**, and **D** gains or by using automated tuning tools available in MATLAB or other control systems.

## 7. Design a Compact PCB

Once you have developed the ESC circuitry, the next step is to design a compact PCB that integrates the components, such as the H-bridge motor driver, shunt resistor, PWM input circuitry, and feedback control system.

### Key Considerations for PCB Design:
- **Small Form Factor**: Ensure the PCB is compact enough to fit into the RC car, taking up minimal space.
- **High-Current Traces**: Make sure that the motor control section (especially around the H-bridge) has sufficiently wide traces to handle the current required by the motor.
- **Cooling Considerations**: Add heat dissipation mechanisms if needed, as high-power motor drivers may require additional cooling.
- **Separation of Power and Logic**: Isolate the high-current motor-driving components from the microcontroller and signal circuitry to reduce noise and improve reliability.

For designing your PCB, you can use **KiCad**, a powerful open-source PCB design tool:
- [KiCad Official Documentation](https://docs.kicad.org/)

## 8. Creating a GUI for ESC Configuration

Once your brushed ESC is up and running, it’s important to have a graphical interface for configuring the ESC parameters (such as PID values, motor limits, and control modes). Using **React**, you can create a clean and user-friendly GUI that communicates with your ESC via serial, WiFi, or Bluetooth.

### Key Features for the GUI:
- **PID Tuning**: Provide sliders or input boxes for adjusting the Proportional, Integral, and Derivative terms of the PID loops.
- **Motor Speed and Limit Configuration**: Let users set maximum and minimum motor speed, acceleration, and deceleration rates.
- **Real-time Monitoring**: Display real-time data from the motor, such as speed, voltage, current, and PWM signal.
- **Communication Interface**: Use React to send and receive configuration data from the ESC through a simple communication protocol.

To get started with React:
- [React Documentation](https://reactjs.org/docs/getting-started.html)

---
