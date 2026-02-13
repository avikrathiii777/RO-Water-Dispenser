# Arduino Automatic RO System Using Ultrasonic Sensor

This project uses:
- Arduino Uno
- HC-SR04 Ultrasonic Sensor
- SG90 Servo Motor

When a hand is detected within 18 cm, the servo opens the RO tap.
When the hand moves away, it closes automatically.

## Components Used
- Arduino Uno
- HC-SR04 Ultrasonic Sensor
- SG90 Servo Motor
- Jumper wires

## Pin Connections
Ultrasonic TRIG -> D2
Ultrasonic ECHO -> D3
Servo Signal -> D9
VCC -> 5V
GND -> GND

## Code

```cpp
#include <Servo.h>

Servo servoMotor;

const int trigPin = 2;
const int echoPin = 3;
const int servoPin = 9;

long duration;
int distance;

void setup()
{
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  servoMotor.attach(servoPin);
  servoMotor.write(0);
}

void loop()
{
  digitalWrite(trigPin, LOW);
  delayMicroseconds(5);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  if (distance > 0 && distance < 18)
  {
    servoMotor.write(90);
  }
  else
  {
    servoMotor.write(0);
  }

  delay(100);
}
