# Arduino-Line-Follower-Car
Arduino-based line follower car project

Line Follower Car Using Arduino
A simple yet effective autonomous robot that follows a line using Arduino, infrared (IR) sensors, and a motor driver module. This project demonstrates the basics of robotics and control systems.

Table of Contents
	1	Overview
	2	Features
	3	Components
	4	Circuit Diagram
	5	How It Works
	6	Setup Instructions
	7	Code

Overview
This project involves building a line follower car that autonomously tracks and follows a black line on a white surface (or vice versa). It uses IR sensors to detect the line and adjusts motor speeds accordingly to stay on track.

Features
	•	Detects and follows lines on the ground using IR sensors.
	•	Adjustable sensor positions for accuracy.
	•	Simple control logic for turning, moving forward, and stopping.

Components


| Component           | Quantity    |
|---------------------|-------------|
| Arduino Uno/Nano    | 1           |
| DC Motors           | 2           |
| Motor Driver (L298N)| 1           |
| IR Sensors          | 2-3         |
| Robot Chassis       | 1           |
| Wheels              | 2           |
| Caster Wheel        | 1           |
| Battery Pack (7.4V) | 1           |
| Jumper Wires        | As needed   |


Circuit Diagram
![Arduino Diagram](images/robot-car.jpg)



How It Works
	1	IR Sensors detect whether they are over a black line (low reflectivity) or white surface (high reflectivity).
	2	Arduino reads the sensor outputs and determines the car’s movement:
	◦	Turn left if the left sensor detects the line.
	◦	Turn right if the right sensor detects the line.
	◦	Move forward if both sensors detect the line.
	◦	Stop if no sensors detect the line.
	3	Motor Driver controls the speed and direction of the motors based on Arduino signals.

Setup Instructions
	1	Hardware Assembly:
	◦	Mount the Arduino, motor driver, and sensors on the chassis.
	◦	Connect motors, sensors, and power supply as per the circuit diagram.
	2	Upload Code:
	◦	Open the Arduino IDE.
	◦	Upload the provided line_follower.ino file to your Arduino.
	3	Test the Car:
	◦	Place the car on a track with a clear black line on a white surface.
	◦	Adjust sensor positions if necessary for optimal detection.

Code
Here’s the core Arduino code for the project. The full code can be found in the line_follower.ino file in this repository.
#define LEFT_SENSOR 2
#define RIGHT_SENSOR 3
#define MOTOR_A1 5
#define MOTOR_A2 6
#define MOTOR_B1 9
#define MOTOR_B2 10

void setup() {
  pinMode(LEFT_SENSOR, INPUT);
  pinMode(RIGHT_SENSOR, INPUT);
  pinMode(MOTOR_A1, OUTPUT);
  pinMode(MOTOR_A2, OUTPUT);
  pinMode(MOTOR_B1, OUTPUT);
  pinMode(MOTOR_B2, OUTPUT);
}

void loop() {
  bool left = digitalRead(LEFT_SENSOR);
  bool right = digitalRead(RIGHT_SENSOR);

  if (left && !right) {
    digitalWrite(MOTOR_A1, LOW);
    digitalWrite(MOTOR_A2, HIGH);
    digitalWrite(MOTOR_B1, HIGH);
    digitalWrite(MOTOR_B2, LOW);
  } else if (!left && right) {
    digitalWrite(MOTOR_A1, HIGH);
    digitalWrite(MOTOR_A2, LOW);
    digitalWrite(MOTOR_B1, LOW);
    digitalWrite(MOTOR_B2, HIGH);
  } else if (left && right) {
    digitalWrite(MOTOR_A1, HIGH);
    digitalWrite(MOTOR_A2, LOW);
    digitalWrite(MOTOR_B1, HIGH);
    digitalWrite(MOTOR_B2, LOW);
  } else {
    digitalWrite(MOTOR_A1, LOW);
    digitalWrite(MOTOR_A2, LOW);
    digitalWrite(MOTOR_B1, LOW);
    digitalWrite(MOTOR_B2, LOW);
  }
}

