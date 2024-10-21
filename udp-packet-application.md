# Mobile Application for RC Car

Now that you have implemented the UDP control of your RC car on ESP32, using an ExpressLRS-compatible transmitter might not always be an option. No worries, since we are sending data over WiFi, we can generate the same control packets using a mobile application.

For creating a mobile application, there are multiple options available:

## 1. React Native

React Native is a popular framework that allows you to create cross-platform mobile applications using JavaScript and React. It enables you to build mobile apps for both iOS and Android while maintaining a single codebase. Using React Native, you can easily create an interface to send control data (e.g., throttle and steering values) via UDP to the ESP32.

You can learn more about React Native and its setup by visiting the official documentation:  
[React Native Documentation](https://reactnative.dev/docs/getting-started)

## 2. Capacitor

Capacitor is a modern, open-source, cross-platform app runtime that allows you to create web applications that run natively on iOS, Android, and even desktop platforms. It is a great choice for building mobile apps that need access to native device features, and it works seamlessly with frameworks like Ionic and modern front-end libraries such as React.

You can explore how to use Capacitor for mobile app development here:  
[Capacitor Documentation](https://capacitorjs.com/docs)

---

## Key Features to Implement in the Mobile App

### 1. Specify IP Address and Port  
In the app, users should be able to manually enter the IP address and port number of the ESP32 to establish UDP communication. This can be done through a simple settings menu where users input:
- ESP32 IP Address (e.g., `192.168.1.101`)
- UDP Port (e.g., `4210`)

Make sure to store this information in the app's local storage, so users do not need to enter it every time they use the app.

### 2. MDNS for Auto Discovery  
To make things easier for users, you can implement **MDNS (Multicast DNS)** for auto-discovery of the ESP32 on the local network. This way, the app can automatically find the ESP32 by its hostname (e.g., `rc-car.local`) without the need for users to manually enter the IP address. MDNS can help eliminate network setup issues and improve user experience.

### 3. RSSI (Signal Strength Indicator)  
Include a feature that shows the current RSSI (Received Signal Strength Indicator) of the ESP32 from the mobile device. This helps users monitor the strength of the WiFi connection and ensure stable communication with the car. The ESP32 can broadcast RSSI data along with the control packets, and the app can parse this information to display it to the user in real time.

Example RSSI display:
- "Signal Strength: Strong (RSSI: -50 dBm)"
- "Signal Strength: Weak (RSSI: -80 dBm)"

### 4. Control Interface for RC Car  
Create a user interface that allows the user to send throttle and steering commands via UDP. This can be achieved through simple UI elements like:
- **Slider** for throttle control (speed).
- **Joystick** or **buttons** for steering control (left/right).

The app will send the control values in a specific format as UDP packets to the ESP32.

---

By implementing these basic features, you can provide an intuitive and efficient way for users to control their RC car over WiFi, regardless of the device platform, while ensuring robust connectivity with features like MDNS and RSSI monitoring.
