# Postura – Real-Time Posture Monitoring and Correction System

## Overview

Postura is a wearable posture monitoring system designed to detect incorrect neck and upper-body posture in real time. The system utilizes the MPU6050 motion sensor to continuously monitor body orientation and movement. Whenever an unhealthy posture is detected, the system provides immediate feedback through a buzzer, encouraging users to correct their posture.

The project aims to promote ergonomic sitting habits and reduce posture-related discomfort caused by prolonged slouching or neck bending.

---

## Hardware Components Used

| Component     | Description                               |
| ------------- | ----------------------------------------- |
| Arduino Uno   | ATmega328P-based microcontroller board    |
| MPU6050       | 3-axis accelerometer and gyroscope sensor |
| Active Buzzer | Audio feedback device                     |
| Breadboard    | Prototyping platform                      |
| Jumper Wires  | Electrical connections                    |

---

## Software Requirements

* Arduino IDE
* Adafruit MPU6050 Library
* Adafruit Unified Sensor Library
* Wire Library

---

## Circuit Connections

| Device              | Arduino Pin |
| ------------------- | ----------- |
| MPU6050 VCC         | 5V          |
| MPU6050 GND         | GND         |
| MPU6050 SDA         | A4          |
| MPU6050 SCL         | A5          |
| Buzzer Positive (+) | D6          |
| Buzzer Negative (-) | GND         |

---

## Working Principle

The MPU6050 continuously measures acceleration and rotational motion along the X, Y, and Z axes.

The Arduino processes these sensor readings and evaluates predefined posture conditions. When the sensor detects a neck bend or slouched posture beyond the configured threshold values, the buzzer is activated to alert the user.

Once the posture returns to a healthy position, the buzzer is automatically turned off and monitoring continues.

---

## Features

* Real-time posture monitoring
* MPU6050 accelerometer and gyroscope integration
* Buzzer-based corrective feedback
* Wearable and lightweight design
* Continuous posture analysis
* Low-cost ergonomic assistance system

---

## Arduino Code

```cpp
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <Wire.h>

#define buzzer 6

Adafruit_MPU6050 mpu;

void setup(void) {
  Serial.begin(115200);

  while (!Serial)
    delay(10);

  if (!mpu.begin()) {
    Serial.println("Failed to find MPU6050 chip");
    while (1) {
      delay(10);
    }
  }

  mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
  mpu.setGyroRange(MPU6050_RANGE_500_DEG);
  mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);

  pinMode(buzzer, OUTPUT);

  delay(100);
}

void loop() {

  sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);

  Serial.print("Acceleration X: ");
  Serial.println(a.acceleration.x);

  if(a.acceleration.x < 10 &&
     a.acceleration.y < 0 &&
     a.acceleration.z > 5)
  {
    digitalWrite(buzzer, HIGH);
    delay(2000);
    Serial.println("neck bend");
  }
  else
  {
    digitalWrite(buzzer, LOW);
    delay(2000);
  }
}
```

---

## Procedure

### Step 1

Connect the MPU6050 sensor to Arduino Uno using I2C communication.

### Step 2

Connect the buzzer to digital pin D6.

### Step 3

Install the required Arduino libraries.

### Step 4

Upload the Arduino sketch to Arduino Uno.

### Step 5

Wear or position the device near the neck or upper-body region.

### Step 6

Maintain a correct posture and observe the sensor readings.

### Step 7

Bend the neck or slouch forward to trigger the posture detection logic.

### Step 8

Observe the buzzer alert indicating incorrect posture.

---

## Output

### Correct Posture

* Buzzer OFF
* Continuous posture monitoring

### Incorrect Posture Detected

* Buzzer ON
* Neck bend alert generated
* User notified to correct posture

---

## Demonstration

🎥 [Watch Demo Video](postura.mp4)

---

## Applications

* Posture Correction Systems
* Ergonomic Monitoring
* Student Study Assistance
* Workplace Health Monitoring
* Wearable Electronics
* Smart Healthcare Devices
* Office Wellness Systems

---

## Skills Demonstrated

* MPU6050 Interfacing
* I2C Communication
* Accelerometer Data Processing
* Gyroscope Data Processing
* Motion Sensing
* Embedded System Development
* Real-Time Monitoring
* Wearable Electronics
* Sensor-Based Decision Making
* Arduino Programming

---

## Future Improvements

* Angle-based posture analysis
* OLED/LCD display integration
* Mobile application connectivity
* Bluetooth-based monitoring
* Data logging and posture analytics
* Vibration motor feedback
* Machine learning-based posture classification
