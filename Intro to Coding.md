# Introduction to Arduino Coding

Welcome to the **IEEE Introduction to Arduino Coding Workshop!**

In this workshop, you will learn how to write Arduino programs to control electronic components. We will start with the basics of Arduino programming and gradually work toward controlling LEDs, reading buttons, measuring distances with ultrasonic sensors, and operating servo motors.

No previous programming experience is required!

## Table of Contents

1. [Introduction to Arduino Programming](#1-introduction-to-arduino-programming)
2. [Structure of an Arduino Program](#2-structure-of-an-arduino-program)
3. [Variables and Data Types](#3-variables-and-data-types)
4. [Arduino Pin Functions](#4-arduino-pin-functions)
5. [Timing Functions](#5-timing-functions)
6. [Conditional Statements and Loops](#6-conditional-statements-and-loops)
7. [Serial Monitor](#7-serial-monitor)
8. [Project 1: Blinking an LED](#8-project-1-blinking-an-led)
9. [Project 2: Pushbutton-Controlled LED](#9-project-2-pushbutton-controlled-led)
10. [Project 3: Ultrasonic Distance Sensor](#10-project-3-ultrasonic-distance-sensor)
11. [Project 4: Servo Motor](#11-project-4-servo-motor)
12. [Project 5: Ultrasonic Sensor + Servo Motor](#12-project-5-ultrasonic-sensor--servo-motor)
13. [Common Errors and Troubleshooting](#13-common-errors-and-troubleshooting)
14. [Practice Challenges](#14-practice-challenges)

---

# 1. Introduction to Arduino Programming

## What is Arduino Programming?

Arduino is a microcontroller platform that allows us to interact with electronic components using code.

By programming an Arduino, we can:

- Turn LEDs on and off
- Detect when buttons are pressed
- Measure distances using sensors
- Control motors
- Create automated electronic systems

Arduino programs are written using a language based on **C/C++**.

These programs are called **sketches** and are written using the Arduino IDE.

## How Does Arduino Code Work?

An Arduino program generally follows three steps:

1. **Input:** Receive information from a sensor or component.
2. **Processing:** Use code to decide what to do with the information.
3. **Output:** Control a component based on the decision.

For example, imagine a system where an LED turns on when a button is pressed.

- Input: The Arduino detects the button press.
- Processing: The Arduino checks whether the button is pressed.
- Output: The Arduino turns on the LED.

This is the foundation of many Arduino projects!

---

# 2. Structure of an Arduino Program

Every Arduino sketch contains two main functions:

```cpp
void setup() {

}

void loop() {

}
```

## What is a Function?

A function is a section of code that performs a specific task.

Functions allow us to organize code and execute instructions.

Arduino has many built-in functions, such as:

- `pinMode()`
- `digitalWrite()`
- `digitalRead()`
- `delay()`

We will explore each of these functions throughout this workshop.

## void setup()

The `setup()` function runs **once** when the Arduino starts or resets.

It is commonly used to:

- Configure input and output pins
- Initialize sensors
- Start serial communication
- Prepare components for operation

Example:

```cpp
void setup() {
  pinMode(8, OUTPUT);
}
```

This tells the Arduino to configure digital pin 8 as an output.

## void loop()

The `loop()` function runs **repeatedly** as long as the Arduino is powered on.

Example:

```cpp
void loop() {
  digitalWrite(8, HIGH);
  delay(1000);
  digitalWrite(8, LOW);
  delay(1000);
}
```

This code repeatedly turns an LED on and off.

Once the last instruction finishes, Arduino returns to the beginning of `loop()`.

## Understanding Arduino Syntax

### Semicolons

Most Arduino statements end with a semicolon (`;`).

```cpp
int ledPin = 8;
digitalWrite(ledPin, HIGH);
```

A missing semicolon can cause a compilation error.

### Curly Braces

Curly braces `{ }` group sections of code.

```cpp
void setup() {
  // Instructions go here
}
```

### Comments

Comments are notes in your code that the Arduino ignores.

Single-line comments:

```cpp
// This is a comment
```

Multi-line comments:

```cpp
/*
This is a
multi-line comment
*/
```

Comments help explain what different sections of code do.

---

# 3. Variables and Data Types

## What is a Variable?

A variable stores information that can be used throughout a program.

For example:

```cpp
int ledPin = 8;
```

Let's break this down:

- `int` specifies the data type.
- `ledPin` is the variable name.
- `8` is the value stored in the variable.
- `=` assigns a value to a variable.

Instead of repeatedly writing:

```cpp
digitalWrite(8, HIGH);
```

We can write:

```cpp
digitalWrite(ledPin, HIGH);
```

This makes code easier to read and modify.

## Common Data Types

| Data Type | Description | Example |
|-----------|-------------|---------|
| `int` | Stores whole numbers | `int count = 5;` |
| `float` | Stores decimal numbers | `float distance = 12.5;` |
| `bool` | Stores true or false | `bool pressed = false;` |
| `char` | Stores a character | `char letter = 'A';` |
| `long` | Stores larger whole numbers | `long duration = 30000;` |

## Constants

Sometimes we want a value that cannot change while the program runs.

We can use `const`.

```cpp
const int ledPin = 8;
```

This is especially useful for assigning Arduino pins.

---

# 4. Arduino Pin Functions

Arduino pins allow the microcontroller to communicate with electronic components.

Some pins are used to receive signals, while others are used to send signals.

## Digital vs. Analog Signals

### Digital Signals

Digital signals have two states:

- `HIGH`
- `LOW`

On a typical 5V Arduino Uno:

- `HIGH` represents approximately 5V.
- `LOW` represents approximately 0V.

Digital signals are useful for:

- Buttons
- LEDs
- Switches
- Detecting whether something is on or off

### Analog Signals

Analog signals can represent a range of voltage values.

For example, an Arduino Uno's analog input can measure voltages between approximately 0V and 5V.

The `analogRead()` function converts this voltage into a number from **0 to 1023** on a traditional 10-bit Arduino Uno.

Analog inputs are useful for:

- Potentiometers
- Light sensors
- Temperature sensors
- Other sensors that produce varying voltages

---

## 4.1 pinMode()

The `pinMode()` function configures how an Arduino pin will operate.

### Syntax

```cpp
pinMode(pin, mode);
```

The function takes two arguments:

1. `pin`: The Arduino pin number.
2. `mode`: How the pin will be used.

There are three common modes:

| Mode | Purpose |
|------|---------|
| `OUTPUT` | Sends signals to components |
| `INPUT` | Receives signals from components |
| `INPUT_PULLUP` | Receives input using an internal pull-up resistor |

### Example: OUTPUT

```cpp
pinMode(8, OUTPUT);
```

This configures digital pin 8 as an output.

We would use this when connecting an LED to pin 8.

### Example: INPUT

```cpp
pinMode(2, INPUT);
```

This configures digital pin 2 as an input.

We would use this when receiving a signal from a component, such as a button with an appropriate external resistor.

### Example: INPUT_PULLUP

```cpp
pinMode(2, INPUT_PULLUP);
```

This configures pin 2 as an input and activates an internal pull-up resistor.

For a button connected between pin 2 and GND:

- Button not pressed: `HIGH`
- Button pressed: `LOW`

This allows us to connect a button without needing an external pull-up resistor.

---

## 4.2 digitalWrite()

The `digitalWrite()` function sets a digital output pin to either `HIGH` or `LOW`.

### Syntax

```cpp
digitalWrite(pin, value);
```

Arguments:

1. `pin`: The pin to control.
2. `value`: Either `HIGH` or `LOW`.

### Example: HIGH

```cpp
digitalWrite(8, HIGH);
```

This sets digital pin 8 to HIGH.

For an LED connected between pin 8 and GND through a resistor, this turns the LED on.

### Example: LOW

```cpp
digitalWrite(8, LOW);
```

This sets digital pin 8 to LOW.

For the same LED circuit, this turns the LED off.

### Complete Example

```cpp
const int ledPin = 8;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
}
```

### How It Works

1. `ledPin` stores the number 8.
2. `pinMode()` configures pin 8 as an output.
3. `digitalWrite()` sets pin 8 to HIGH.
4. The LED remains on.

**Important:** Always use an appropriate current-limiting resistor with a standard LED.

---

## 4.3 digitalRead()

The `digitalRead()` function reads the current state of a digital input pin.

### Syntax

```cpp
digitalRead(pin);
```

It returns one of two values:

- `HIGH`
- `LOW`

### Example

```cpp
int buttonState = digitalRead(2);
```

This reads the digital signal on pin 2 and stores the result in the variable `buttonState`.

If the button uses `INPUT_PULLUP` and is connected to GND:

- `HIGH` means the button is not pressed.
- `LOW` means the button is pressed.

### Complete Example

```cpp
const int buttonPin = 2;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop() {
  int buttonState = digitalRead(buttonPin);

  Serial.println(buttonState);

  delay(100);
}
```

This program repeatedly reads the button and displays its state in Serial Monitor.

---

## 4.4 analogRead()

The `analogRead()` function measures an analog voltage on an analog input pin.

### Syntax

```cpp
analogRead(pin);
```

### Example

```cpp
int sensorValue = analogRead(A0);
```

On a traditional Arduino Uno:

- 0V corresponds to approximately 0.
- 2.5V corresponds to approximately 512.
- 5V corresponds to approximately 1023.

### Complete Example

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(A0);

  Serial.println(sensorValue);

  delay(100);
}
```

This reads an analog input and prints the result.

---

## 4.5 analogWrite()

The `analogWrite()` function generates a Pulse Width Modulation (PWM) signal on supported pins.

PWM rapidly switches a pin between HIGH and LOW.

By changing how long the pin stays HIGH, we can control the average power delivered to certain components.

This is commonly used to adjust LED brightness.

### Syntax

```cpp
analogWrite(pin, value);
```

On a traditional Arduino Uno, the PWM value ranges from:

- `0`: 0% duty cycle
- `127`: approximately 50% duty cycle
- `255`: 100% duty cycle

### Example

```cpp
analogWrite(9, 127);
```

This produces an approximately 50% duty-cycle PWM signal on pin 9.

### Example: Changing LED Brightness

```cpp
const int ledPin = 9;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  analogWrite(ledPin, 50);
  delay(1000);

  analogWrite(ledPin, 150);
  delay(1000);

  analogWrite(ledPin, 255);
  delay(1000);
}
```

The LED changes between three brightness levels.

**Note:** On an Arduino Uno, the usual PWM pins are 3, 5, 6, 9, 10, and 11.

---

# 5. Timing Functions

Timing functions allow us to control when instructions execute.

## 5.1 delay()

The `delay()` function pauses the program for a specified number of milliseconds.

### Syntax

```cpp
delay(milliseconds);
```

Remember:

**1000 milliseconds = 1 second**

Examples:

```cpp
delay(1000);  // Wait 1 second
delay(500);   // Wait 0.5 seconds
delay(2000);  // Wait 2 seconds
```

### Example

```cpp
digitalWrite(8, HIGH);
delay(1000);
digitalWrite(8, LOW);
```

The Arduino turns the LED on, waits one second, and then turns it off.

## 5.2 delayMicroseconds()

The `delayMicroseconds()` function pauses the program for a specified number of microseconds.

**1,000,000 microseconds = 1 second**

### Syntax

```cpp
delayMicroseconds(microseconds);
```

Example:

```cpp
delayMicroseconds(10);
```

This pauses the program for approximately 10 microseconds.

This function is useful for sensors requiring short timing pulses, such as the HC-SR04 ultrasonic sensor.

## 5.3 millis()

The `millis()` function returns the number of milliseconds since the Arduino program started.

```cpp
unsigned long currentTime = millis();
```

Unlike `delay()`, using `millis()` does not automatically pause the program.

It is useful when we want to track time while allowing other instructions to continue running.

---

# 6. Conditional Statements and Loops

## 6.1 if Statements

An `if` statement allows the Arduino to execute code only when a condition is true.

### Syntax

```cpp
if (condition) {
  // Code to execute if condition is true
}
```

### Example

```cpp
if (buttonState == LOW) {
  digitalWrite(8, HIGH);
}
```

If `buttonState` equals `LOW`, pin 8 is set to HIGH.

### Comparison Operators

| Operator | Meaning |
|----------|---------|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

**Important:**

- `=` assigns a value.
- `==` compares two values.

## 6.2 if/else Statements

An `else` statement specifies what to do when the `if` condition is false.

Example:

```cpp
if (buttonState == LOW) {
  digitalWrite(8, HIGH);
} else {
  digitalWrite(8, LOW);
}
```

If the button is pressed, the LED turns on.

Otherwise, the LED turns off.

## 6.3 for Loops

A `for` loop repeats a section of code a specified number of times.

### Syntax

```cpp
for (initialization; condition; update) {
  // Repeated code
}
```

### Example

```cpp
for (int i = 0; i < 5; i++) {
  digitalWrite(8, HIGH);
  delay(200);
  digitalWrite(8, LOW);
  delay(200);
}
```

Breaking down the loop:

- `int i = 0`: Start counting at 0.
- `i < 5`: Continue while i is less than 5.
- `i++`: Increase i by 1 after each iteration.

This makes the LED blink five times.

---

# 7. Serial Monitor

The Serial Monitor allows us to send information from the Arduino to our computer.

This is extremely useful for:

- Viewing sensor readings
- Checking button states
- Debugging programs
- Displaying messages

## 7.1 Serial.begin()

The `Serial.begin()` function starts serial communication.

### Syntax

```cpp
Serial.begin(baudRate);
```

Example:

```cpp
Serial.begin(9600);
```

The value `9600` specifies the communication speed in bits per second.

Make sure the Serial Monitor uses the same baud rate.

We normally place this function inside `setup()`.

## 7.2 Serial.print()

The `Serial.print()` function displays information without automatically moving to a new line.

```cpp
Serial.print("Distance: ");
```

## 7.3 Serial.println()

The `Serial.println()` function displays information and then moves to a new line.

```cpp
Serial.println(25);
```

### Example

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  Serial.print("Hello ");
  Serial.println("Arduino!");

  delay(1000);
}
```

Output:

```text
Hello Arduino!
Hello Arduino!
Hello Arduino!
```

---

# 8. Project 1: Blinking an LED

## Objective

Write a program that repeatedly turns an LED on and off.

## Components

- Arduino Uno
- Breadboard
- LED
- 220Ω or 330Ω resistor
- Jumper wires

## Wiring

1. Connect the LED's longer leg (anode) to digital pin 8 through a resistor.
2. Connect the LED's shorter leg (cathode) to GND.
3. Connect the Arduino to your computer.

## Code

```cpp
const int ledPin = 8;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(1000);

  digitalWrite(ledPin, LOW);
  delay(1000);
}
```

## Explanation

### Step 1

```cpp
const int ledPin = 8;
```

Creates a constant named `ledPin` and assigns it the value 8.

### Step 2

```cpp
pinMode(ledPin, OUTPUT);
```

Configures pin 8 as an output.

### Step 3

```cpp
digitalWrite(ledPin, HIGH);
```

Sets pin 8 HIGH, turning the LED on.

### Step 4

```cpp
delay(1000);
```

Waits one second.

### Step 5

```cpp
digitalWrite(ledPin, LOW);
```

Sets pin 8 LOW, turning the LED off.

### Step 6

```cpp
delay(1000);
```

Waits another second.

Because these instructions are inside `loop()`, the process repeats continuously.

## Challenge

Modify the code so that the LED:

1. Blinks twice as fast.
2. Stays on for 2 seconds and off for 0.5 seconds.
3. Blinks three times before pausing.

---

# 9. Project 2: Pushbutton-Controlled LED

## Objective

Write a program that turns an LED on when a button is pressed and turns it off when the button is released.

## Components

- Arduino Uno
- Breadboard
- Pushbutton
- LED
- 220Ω or 330Ω resistor
- Jumper wires

## Wiring

### LED

- LED anode → resistor → pin 8
- LED cathode → GND

### Button

- One side of the button → pin 2
- Opposite side of the button → GND

We will use `INPUT_PULLUP`, so an external pull-up resistor is not required.

**Note:** On typical four-legged tactile buttons, the two legs on the same side are internally connected. Use legs on opposite sides of the switch.

## Code

```cpp
const int ledPin = 8;
const int buttonPin = 2;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);
}

void loop() {
  int buttonState = digitalRead(buttonPin);

  if (buttonState == LOW) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }
}
```

## Explanation

### Step 1: Define Pins

```cpp
const int ledPin = 8;
const int buttonPin = 2;
```

Stores the LED and button pin numbers.

### Step 2: Configure Pins

```cpp
pinMode(ledPin, OUTPUT);
pinMode(buttonPin, INPUT_PULLUP);
```

The LED pin is configured as an output.

The button pin is configured as an input with the internal pull-up resistor activated.

### Step 3: Read the Button

```cpp
int buttonState = digitalRead(buttonPin);
```

The Arduino reads the electrical state of pin 2.

The result is stored in `buttonState`.

### Step 4: Check the Button State

```cpp
if (buttonState == LOW)
```

Checks whether the button is pressed.

Since we are using `INPUT_PULLUP`:

- Pressed = LOW
- Released = HIGH

### Step 5: Control the LED

```cpp
digitalWrite(ledPin, HIGH);
```

Turns on the LED when the button is pressed.

```cpp
digitalWrite(ledPin, LOW);
```

Turns off the LED when the button is released.

## Challenge

Modify the program so that:

1. The LED turns off when the button is pressed.
2. The LED turns on when the button is released.
3. Two LEDs alternate depending on the button state.

---

# 10. Project 3: Ultrasonic Distance Sensor

## Objective

Use an HC-SR04 ultrasonic sensor to measure the distance between the sensor and an object.

## What is an Ultrasonic Sensor?

An ultrasonic sensor measures distance using sound waves.

The HC-SR04 works by:

1. Sending out a high-frequency sound pulse.
2. Waiting for the sound to bounce off an object.
3. Detecting the returning echo.
4. Measuring how long the sound took to travel.
5. Calculating the distance.

## HC-SR04 Pins

The HC-SR04 has four pins:

| Pin | Purpose |
|-----|---------|
| VCC | Power supply (5V) |
| TRIG | Triggers an ultrasonic pulse |
| ECHO | Outputs a pulse representing travel time |
| GND | Ground |

## Components

- Arduino Uno
- HC-SR04 ultrasonic sensor
- Jumper wires

## Wiring

| HC-SR04 Pin | Arduino Uno |
|-------------|-------------|
| VCC | 5V |
| GND | GND |
| TRIG | Pin 9 |
| ECHO | Pin 10 |

## Understanding the Distance Formula

The speed of sound in air is approximately:

**0.0343 cm/µs**

Distance is calculated using:

\[
\text{Distance} =
\frac{\text{Duration} \times 0.0343}{2}
\]

We divide by 2 because the sound travels from the sensor to the object and then back to the sensor.

For example, if the echo duration is 1000 microseconds:

\[
\text{Distance} =
\frac{1000 \times 0.0343}{2}
= 17.15 \text{ cm}
\]

## New Function: pulseIn()

The `pulseIn()` function measures how long a digital pin stays HIGH or LOW.

### Syntax

```cpp
pulseIn(pin, value);
```

Example:

```cpp
duration = pulseIn(echoPin, HIGH);
```

This measures how long the ECHO pin stays HIGH.

The returned duration is measured in microseconds.

We can also specify a timeout:

```cpp
duration = pulseIn(echoPin, HIGH, 30000);
```

This waits up to approximately 30,000 microseconds for a pulse.

A return value of 0 means no complete pulse was detected before the timeout.

## Complete Code

```cpp
const int trigPin = 9;
const int echoPin = 10;

long duration;
float distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH, 30000);

  if (duration == 0) {
    Serial.println("No echo detected");
  } else {
    distance = duration * 0.0343 / 2.0;

    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");
  }

  delay(100);
}
```

## Code Explanation

### Step 1: Define Sensor Pins

```cpp
const int trigPin = 9;
const int echoPin = 10;
```

The trigger pin sends the signal to begin a measurement.

The echo pin receives the timing signal used to calculate distance.

### Step 2: Create Variables

```cpp
long duration;
float distance;
```

`duration` stores the echo pulse length in microseconds.

`distance` stores the calculated distance in centimeters.

### Step 3: Configure Pins

```cpp
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
```

The trigger pin is an output.

The echo pin is an input.

### Step 4: Prepare the Trigger Pin

```cpp
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
```

Ensures the trigger pin starts LOW before the measurement.

### Step 5: Send a Trigger Pulse

```cpp
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
```

This sends a HIGH pulse lasting 10 microseconds.

The HC-SR04 responds by transmitting an ultrasonic burst.

### Step 6: Measure Echo Time

```cpp
duration = pulseIn(echoPin, HIGH, 30000);
```

Measures the width of the ECHO pulse.

This represents the approximate round-trip travel time of the sound wave.

### Step 7: Calculate Distance

```cpp
distance = duration * 0.0343 / 2.0;
```

Converts the measured time into distance.

### Step 8: Display the Result

```cpp
Serial.print("Distance: ");
Serial.print(distance);
Serial.println(" cm");
```

Displays the measured distance in the Serial Monitor.

### Example Output

```text
Distance: 25.43 cm
Distance: 24.91 cm
Distance: 23.76 cm
Distance: 22.15 cm
```

## Challenge

Modify the program so that:

1. It prints "Object Nearby" when the distance is less than 10 cm.
2. It prints "Object Far Away" when the distance is greater than 30 cm.
3. An LED turns on when an object is within 15 cm.

---

# 11. Project 4: Servo Motor

## Objective

Control the angular position of a servo motor using Arduino.

## What is a Servo Motor?

A servo motor is a motor designed to move to a specific position.

Unlike a regular DC motor that continuously rotates, a standard positional servo can be commanded to move to particular angles.

Many hobby servo motors operate over a range of approximately 0° to 180°, although the actual movement range depends on the model.

Servo motors are commonly used in:

- Robotic arms
- Automated doors
- Remote-controlled vehicles
- Robotics projects
- Mechanical positioning systems

## Servo Motor Wires

A typical SG90 servo motor has three wires:

| Wire Color | Purpose |
|------------|---------|
| Brown | GND |
| Red | Power |
| Orange | Signal |

Wire colors may vary between servo models.

## Components

- Arduino Uno
- SG90 positional servo motor
- Jumper wires
- Suitable 5V power source

## Wiring

| Servo Wire | Connection |
|------------|------------|
| Brown | GND |
| Red | 5V power |
| Orange | Arduino Pin 9 |

**Power note:** A small unloaded SG90 may work from the Uno's 5V pin for a simple demonstration, but servos can draw substantial current. For more reliable operation, use a suitable external regulated 5V supply and connect its GND to Arduino GND. Do not power the servo from an Arduino digital I/O pin.

## Understanding Servo Libraries

Arduino has a Servo library that simplifies motor control.

A library provides prewritten functions for specific tasks.

For a servo motor, the library allows us to specify an angle without manually generating control pulses.

## New Command: #include

```cpp
#include <Servo.h>
```

This tells Arduino to include the Servo library.

The library provides functions used to operate servo motors.

## Creating a Servo Object

```cpp
Servo myServo;
```

Creates a servo object named `myServo`.

We can use this object to control the motor.

## Servo Function: attach()

### Syntax

```cpp
myServo.attach(pin);
```

Example:

```cpp
myServo.attach(9);
```

Associates the servo object with digital pin 9.

The Arduino will send servo control signals through this pin.

## Servo Function: write()

### Syntax

```cpp
myServo.write(angle);
```

Example:

```cpp
myServo.write(90);
```

Commands a standard positional servo to move toward approximately 90°.

Other examples:

```cpp
myServo.write(0);
myServo.write(45);
myServo.write(90);
myServo.write(180);
```

The actual physical angle depends on the servo motor.

## Complete Code

```cpp
#include <Servo.h>

Servo myServo;

void setup() {
  myServo.attach(9);
}

void loop() {
  myServo.write(0);
  delay(1000);

  myServo.write(90);
  delay(1000);

  myServo.write(180);
  delay(1000);
}
```

## Code Explanation

### Step 1: Include the Library

```cpp
#include <Servo.h>
```

Loads the Servo library.

### Step 2: Create the Servo Object

```cpp
Servo myServo;
```

Creates an object that represents the servo motor.

### Step 3: Attach the Servo

```cpp
myServo.attach(9);
```

Connects the servo object to pin 9.

### Step 4: Move to 0°

```cpp
myServo.write(0);
```

Commands the servo to approximately 0°.

### Step 5: Wait

```cpp
delay(1000);
```

Waits one second to allow time for the servo to move.

### Step 6: Move to 90°

```cpp
myServo.write(90);
```

Commands the servo to approximately 90°.

### Step 7: Move to 180°

```cpp
myServo.write(180);
```

Commands the servo to approximately 180°.

The program continuously repeats this sequence.

---

## Servo Motor Example: Sweeping Motion

We can also use a `for` loop to move the servo gradually.

```cpp
#include <Servo.h>

Servo myServo;

void setup() {
  myServo.attach(9);
}

void loop() {
  for (int angle = 0; angle <= 180; angle++) {
    myServo.write(angle);
    delay(15);
  }

  for (int angle = 180; angle >= 0; angle--) {
    myServo.write(angle);
    delay(15);
  }
}
```

## Explanation

The first loop:

```cpp
for (int angle = 0; angle <= 180; angle++)
```

Increases the commanded angle from 0° to 180°.

The second loop:

```cpp
for (int angle = 180; angle >= 0; angle--)
```

Decreases the commanded angle from 180° back to 0°.

This creates a sweeping motion.

The `delay(15)` provides time between successive angle commands.

## Challenge

Modify the program so that:

1. The servo moves between 45° and 135°.
2. The servo sweeps more slowly.
3. The servo only moves when a button is pressed.

---

# 12. Project 5: Ultrasonic Sensor + Servo Motor

## Objective

Combine an ultrasonic sensor and servo motor to create a simple automated system.

When an object comes within 15 cm of the ultrasonic sensor, the servo will rotate to approximately 90°.

When the object moves away, the servo returns to approximately 0°.

This is similar to how an automatic gate or barrier might operate.

## Components

- Arduino Uno
- HC-SR04 ultrasonic sensor
- SG90 positional servo motor
- Jumper wires
- Suitable servo power supply

## Wiring

### Ultrasonic Sensor

| HC-SR04 | Arduino |
|---------|---------|
| VCC | 5V |
| GND | GND |
| TRIG | Pin 7 |
| ECHO | Pin 6 |

### Servo Motor

| Servo | Connection |
|-------|------------|
| Signal | Pin 9 |
| Power | Suitable regulated 5V |
| GND | Common ground with Arduino |

If using an external servo supply, connect its ground to Arduino GND.

## Complete Code

```cpp
#include <Servo.h>

const int trigPin = 7;
const int echoPin = 6;
const int servoPin = 9;

Servo myServo;

long duration;
float distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  myServo.attach(servoPin);
  myServo.write(0);

  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH, 30000);

  if (duration == 0) {
    Serial.println("No echo detected");
  } else {
    distance = duration * 0.0343 / 2.0;

    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance < 15) {
      myServo.write(90);
    } else {
      myServo.write(0);
    }
  }

  delay(100);
}
```

## How the Program Works

### Step 1: Measure Distance

The Arduino triggers the ultrasonic sensor.

The ECHO pulse duration is measured using `pulseIn()`.

### Step 2: Calculate Distance

```cpp
distance = duration * 0.0343 / 2.0;
```

The measured duration is converted into centimeters.

### Step 3: Check Distance

```cpp
if (distance < 15)
```

Checks whether the detected object is closer than 15 cm.

### Step 4: Control the Servo

```cpp
myServo.write(90);
```

If the object is close, the servo moves toward 90°.

Otherwise:

```cpp
myServo.write(0);
```

The servo returns toward 0°.

If no echo is detected, the program reports that condition and leaves the servo at its most recently commanded position.

## Challenge

Modify the program so that:

1. The detection threshold changes from 15 cm to 25 cm.
2. The servo moves to 180° instead of 90°.
3. An LED turns on when the servo opens.
4. The servo only opens when an object is close AND a button is pressed.

---

# 13. Common Errors and Troubleshooting

## Error 1: Missing Semicolon

Incorrect:

```cpp
int ledPin = 8
```

Correct:

```cpp
int ledPin = 8;
```

Most Arduino statements require a semicolon.

## Error 2: Incorrect Capitalization

Incorrect:

```cpp
digitalwrite(8, HIGH);
```

Correct:

```cpp
digitalWrite(8, HIGH);
```

Arduino code is case-sensitive.

## Error 3: Incorrect Pin Mode

Incorrect:

```cpp
pinMode(8, INPUT);
digitalWrite(8, HIGH);
```

If we intend to drive an LED normally, configure its pin as an output.

Correct:

```cpp
pinMode(8, OUTPUT);
digitalWrite(8, HIGH);
```

## Error 4: Confusing = and ==

Incorrect:

```cpp
if (buttonState = LOW)
```

Correct:

```cpp
if (buttonState == LOW)
```

Remember:

- `=` assigns a value.
- `==` compares values.

## Error 5: Button Logic Is Reversed

When using `INPUT_PULLUP`:

- Pressed means LOW.
- Released means HIGH.

This is the opposite of what some beginners expect.

## Error 6: Servo Does Not Move Properly

Possible causes include:

- Incorrect wiring
- Insufficient power
- Missing common ground
- Incorrect servo pin
- Mechanical obstruction
- Servo angle outside its usable range

Check the wiring and use a suitable power supply.

## Error 7: Ultrasonic Sensor Returns Zero

Possible causes include:

- Incorrect TRIG or ECHO wiring
- Sensor not receiving power
- No valid echo detected
- Object outside the sensor's detection range
- Incorrect pulse timing

If `pulseIn()` returns zero, check the sensor and wiring.

## Error 8: Program Does Not Upload

Possible causes include:

- Incorrect board selected in Arduino IDE
- Incorrect serial port selected
- USB cable does not support data
- Another program is using the serial port
- Missing or incompatible USB-serial driver

Check **Tools → Board** and the selected port before uploading.

---

# 14. Practice Challenges

Try completing these challenges without looking at the example solutions!

## Beginner Challenges

### Challenge 1: LED Timing

Create a program that:

- Turns an LED on for 500 milliseconds
- Turns it off for 250 milliseconds
- Repeats continuously

### Challenge 2: Button Control

Create a program where:

- Pressing a button turns an LED off
- Releasing the button turns the LED on

### Challenge 3: LED Brightness

Use PWM to make an LED display three different brightness levels.

## Intermediate Challenges

### Challenge 4: Ultrasonic Warning System

Create a system where:

- Distance less than 10 cm: LED on
- Distance greater than or equal to 10 cm: LED off

### Challenge 5: Servo Button Control

Create a program where:

- Button pressed: Servo moves to 90°
- Button released: Servo returns to 0°

### Challenge 6: Servo Sweeping

Create a servo program that:

- Starts at 30°
- Moves to 150°
- Returns to 30°
- Repeats continuously

## Advanced Challenge

### Challenge 7: Automatic Barrier

Create a system using:

- Ultrasonic sensor
- Servo motor
- LED
- Pushbutton

Requirements:

1. The ultrasonic sensor detects an approaching object.
2. If the object is within 20 cm, the Arduino checks the button.
3. If the button is pressed, the servo rotates to open the barrier.
4. The LED turns on when the barrier is open.
5. Otherwise, the barrier remains closed and the LED is off.

---

# Additional Resources

For more information, visit the official Arduino documentation:

- [Arduino Official Website](https://www.arduino.cc/)
- [Arduino Language Reference](https://docs.arduino.cc/language-reference/)
- [Arduino IDE Download](https://www.arduino.cc/en/software)
- [Arduino Built-In Examples](https://docs.arduino.cc/built-in-examples/)
- [Arduino Servo Library](https://docs.arduino.cc/libraries/servo/)

---

# Conclusion

Congratulations on completing the Introduction to Arduino Coding Workshop!

You should now understand:

- How Arduino programs are structured
- How to use variables and functions
- How to configure input and output pins
- How to use `digitalWrite()` and `digitalRead()`
- How to control timing with `delay()`
- How to use conditional statements and loops
- How to read an ultrasonic distance sensor
- How to control a servo motor
- How to combine sensors and motors into automated systems

These concepts form the foundation for more advanced Arduino projects involving robotics, automation, and embedded systems.

**IEEE at the University of Maryland — Arduino Coding Workshop**
