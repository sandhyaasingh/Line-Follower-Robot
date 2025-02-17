# Line Follower Robot

## Description
This project demonstrates the working of a line follower robot using Arduino. The robot uses infrared sensors to detect and follow a black line on a white surface. The robot adjusts its movement based on the line's direction, ensuring it stays on track. It uses an Arduino Uno for controlling the robot and is a great way to understand basic robotics principles.

## Components Used
- **Arduino Uno**: Microcontroller for controlling the robot.
- **Infrared Sensors (IR)**: Detects the black line on a white surface.
- **DC Motors with L298 Motor Driver**: Powers the motors of the robot.
- **Jumper wires, wheels, and chassis**: For assembling the robot.
- **Power Supply (Battery)**: Powers the entire setup.

## Key Features
- **Line Following**: Follows a black line on a white surface using infrared sensors.
- **Real-Time Control**: Adjusts its movement based on sensor input to stay on track.
- **Simple & Fun**: Easy to build and program, perfect for beginners in robotics.

## Installation & Setup
1. **Hardware Setup**:
   - Connect the DC motors to the L298 motor driver.
   - Connect the infrared sensors to the Arduino (VCC, GND, and signal pins).
   - Wire the motor driver to the Arduino and power the motors using a suitable battery.

2. **Software Setup**:
   - Download and install the Arduino IDE if not already installed.
   - Open the Arduino IDE and upload the code to your Arduino Uno.

3. **Run the Robot**:
   - After the setup, place the robot on a surface with a black line, and it will follow the line autonomously.

## Source Code:

```cpp
// Line Follower Robot Code

//motor one
#define A1 5
#define A 6

//motor two
#define B1 9
#define B 10

//sensor pins
#define SL 3
#define SR 2

int mSpeed = 130;//motor speed

void setup() {
  pinMode(A1, OUTPUT);
  pinMode(A, OUTPUT);
  pinMode(B1, OUTPUT);
  pinMode(B, OUTPUT);

  pinMode(SL, INPUT);
  pinMode(SR, INPUT);
  Serial.begin(9600);
}

void loop() {
  bool LValue = digitalRead(SL);//get sensor value one
  bool RValue = digitalRead(SR);//get sensor value two

  Serial.print(LValue);
  Serial.println(RValue);

  if (RValue == 1 && LValue == 0 ) {
    turnRight();
    Serial.println("turnRight");
  } else if (LValue == 1 && RValue == 0) {
    turnLeft();
    Serial.println("turnLeft");
  } else if (LValue == 0 && RValue == 0) {
    forward();
    Serial.println("forward");
  } else if (LValue == 1 && RValue == 1) {
    Stop();
    Serial.println("stop");
  }

}
void turnRight() {
  analogWrite(B1, 140);
  analogWrite(B, 0);
  analogWrite(A1, 0);
  analogWrite(A, 0);
}
void turnLeft() {
  analogWrite(B1, 0);
  analogWrite(B, 0);
  analogWrite(A1, 140);
  analogWrite(A, 0);
}
void forward() {
  analogWrite(B1, 140);
  analogWrite(B, 0);
  analogWrite(A1, 140);
  analogWrite(A, 0);
}
void Stop() {
  analogWrite(A1, LOW);
  analogWrite(A, LOW);
  analogWrite(B1, LOW);
  analogWrite(B, LOW);
}
```
Final Setup:



## How It Works:
1. The robot moves forward by default if both infrared sensors detect the black line.
2. If the left sensor detects the line, the robot turns left, and if the right sensor detects the line, the robot turns right.
3. If both sensors lose the line, the robot stops.

## Future Scope:
- Add more advanced line-following algorithms, such as PID control.
- Implement a maze-solving algorithm.
- Integrate additional sensors for improved navigation.
