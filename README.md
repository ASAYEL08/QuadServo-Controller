<div align="center">

# 🤖 Quad Servo Motor Control System
### ⚡ Arduino Uno & Tinkercad Simulation ⚡

[![Arduino](https://img.shields.io/badge/Platform-Arduino%20Uno-blue?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Tinkercad](https://img.shields.io/badge/Simulation-Tinkercad-orange?style=for-the-badge&logo=autodesk&logoColor=white)](https://www.tinkercad.com/)
[![Language](https://img.shields.io/badge/Language-C++%20%2F%20Arduino-teal?style=for-the-badge&logo=cplusplus&logoColor=white)](https://en.wikipedia.org/wiki/C%2B%2B)

</div>

---

## 📋 🌟 Project Overview
This project showcases a precise multi-channel servo motor coordination routine programmed via an Arduino Uno. The execution handles dynamic transition states, transitioning smoothly from timed continuous movement to a locked stabilization checkpoint.

---

## 🎯 ⚡ Operational Sequence & Requirements
The control algorithm executes a strict two-stage routine:
1. 🔄 Stage 1 (Sweep Mode): All four servo motors simultaneously perform a continuous back-and-forth oscillating sweep (`0°` to `180°`) for an exact duration of 2 seconds.
2. 🛑 Stage 2 (Hold Mode): Immediately upon expiration of the temporal window, all motors snap to and rigidly hold a precise orientation of 90 degrees.

---

## 🛠️ 🔌 Hardware Architecture & Pin Mapping

| Component | Interface / Pin | Description |
| :--- | :--- | :--- |
| 🧠 Microcontroller | Arduino Uno | Central processing unit |
| ⚙️ Servo Motor 1 | Digital Pin 9 (PWM) | Independent signal channel |
| ⚙️ Servo Motor 2 | Digital Pin 10 (PWM) | Independent signal channel |
| ⚙️ Servo Motor 3 | Digital Pin 11 (PWM) | Independent signal channel |
| ⚙️ Servo Motor 4 | Digital Pin 6 (PWM) | Independent signal channel |
| 🔋 Power Distribution | Breadboard | Shared 5V & GND bus for high-current delivery |

---

## 💻 ⚡ Firmware Implementation

```cpp
#include <Servo.h>

Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

void setup() {
  servo1.attach(9);
  servo2.attach(10);
  servo3.attach(11);
  servo4.attach(6);
}

void loop() {
  unsigned long startTime = millis();

  while (millis() - startTime < 2000) {
    for (int pos = 0; pos <= 180; pos += 1) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(15);
    }
    for (int pos = 180; pos >= 0; pos -= 1) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(15);
    }
  }

  servo1.write(90);
  servo2.write(90);
  servo3.write(90);
  servo4.write(90);

  while (true) {
  }
}
