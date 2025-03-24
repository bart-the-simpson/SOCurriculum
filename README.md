# Outline for WiC School Outreach Program

* Each day is ~90 minutes
* *italicized* text means a question that you can turn and ask the students 
  * Rhetorical questions generally are not italicized
* **bold** is for important vocabulary
* ==highlighted== text is for actions

## Initial Setup

Arrange with teachers to ensure that the Arduino IDE is installed on student computers: https://arduino.cc/download/

## Week 1: Intro to Programming and LEDs

### Introductions

(30 minutes)

* Introduce ourselves, WiC, and MESA
    * Briefly go over the program
* Students introduce themselves (20 minutes)
    * Name and year
    * Why did you sign up for this program?
    * Have you programmed before?
    * One fun fact about yourself :)

### Brief Lecture 

(20 minutes)

  * What is a **program**?
      * Computers require you to be very specific
      * It might seem hard, but we'll learn bit-by-bit
      * ==Show the make-up of an Arduino program with a screenshot==
  * What is a **Zumo**?
  * What is an **Arduino**?

### Lesson Plan

(40 minutes)

  * Open the Arduino IDE
  * Program comes preloaded with two functions, `setup()` and `loop()`
  * A **function** is a block of reusable code that does something specific
      * You can write your own functions, but today we'll be working with functions that are already in the program
  * `setup()` is run once at the beginning and `loop()` loops your code
    
#### Intro to Functions

``` C++
    void setup() {
        pinMode(13, OUTPUT);
        digitalWrite(13, HIGH);
}
```

To upload your code into the Arduino, you must:

1. **link** the cable to your computer
2. **select** the correct Port
    * *Drop-down menu* on newer versions
    * Tools > Port > COM# on older versions
    * The Port won't appear if the robot is not connected
3. and press **Upload**!

`pinMode()` and `digitalWrite()` are also functions, notice how they have parentheses following their names. When we use functions, we end the line with a semicolon, similar to using a period to end a sentence.

`pinMode(13, OUTPUT)` configures the given pin, in this case pin 13, as an output. Pin 13 is the LED found on the top of your Zumo robots.

`digitalWrite(13, HIGH)` turns pin 13 (the LED) on. LOW would turn it off.

Say we wanted to turn the LED off after 3 seconds. How would you do it? How would we be able to tell the computer that it should wait 3 seconds?

The function `delay()` pauses the program for a given amount of time. `delay(1000)` pauses the program for 1 second. Knowing that, and that putting LOW instead of HIGH into the `digitalWrite()` function will turn it off, *can you add to the code and turn the LED off after 3 seconds?*

**Solution:**

``` C++
    void setup() {
        pinMode(13, OUTPUT);
        digitalWrite(13, HIGH);
        delay(3000);
        digitalWrite(13, LOW);
    }
```

### Outro 

(5 minutes)

  * Go over the day's accomplishments
      * Learned about our Arduino Zumo robot, programs, and functions
      * `pinMode()`, `digitalWrite()`, and `delay()`
      * Hands-on coding with the Arduino Zumo's LED
  * What's planned for next week?
      * Making the robot move!

## Week 2: Functions and Motors

* Review of last week (10 minutes)
### Lesson Plan

(60 Minutes)

  * Students install **ZumoShield** library 
    * necessary in order to use Zumo header files

#### Intro to Motors

  Helper code for today, include this at top of program, above `setup()`:

```C++
    #include <ZumoMotors.h>
    const int SPEED = 100;
    ZumoMotors motors;
```

==Explain while the students copy the code.==

`include <ZumoMotors.h>`: ZumoMotors is a **library**, pre-written code made by a programmer so we can do specific things, in this case, making our robot move. Someone has written all the functions to make the robot move - this statement takes the contents of the file "ZumoMotors.h" and copies it into our code, so we can use them in our program. Note there is no semicolon at the end of the line!

`const int SPEED = 100;` is us making a **constant**, that is called `SPEED`.  Compare it to a constant in math, like pi, where when you write down pi, it actually stands in for the number 3.14... It's similar in programming, but constants are basically containers for information or **data** as we call it. Think of it like every time we write `SPEED` in our program, the computer knows it actually means `100`. `int` is short for integer, meaning that `SPEED` represents an integer. `const` is what makes it a constant and means that `SPEED` can't change throughout our program, which will be important.

`ZumoMotors motors;` allows us to use the ZumoMotors code in our program.

`motors.setSpeeds(SPEED, SPEED)` is code from the **library** we imported earlier. The two numbers inside the parentheses are **arguments**. Think of them like inputs to the function. *What do you guys think will happen if we ran this code, knowing it relates to the movement motors?* 

Let's try to think back to our lesson last week where we made the robot's LED to flash for 3 seconds and then stop. *Do you guys think you can modify the code we had last week to make it move for 3 seconds and then come to a stop?*

```C++
    void setup() {
        motors.setSpeeds(SPEED, SPEED);
        delay(3000);
        motors.setSpeeds(0, 0);
    }
```

#### Writing Our Own Functions

 However, it would probably get hard to retype over and over again. We made our own variable earlier with `SPEED`, why don't we try writing our own functions as well? 

```C++
    void turnOnMotors() {
        motors.setSpeeds(SPEED, SPEED);
    }
```
Now everytime we write `turnOnMotors();`, it will run the `motors.setSpeeds(SPEED, SPEED)` code inside of it. Before we test it out, we should have a function that turns off the motors as well. *Does anyone know what number we could put here to make the robot stop moving?*
```C++
    void turnOffMotors() {
        motors.setSpeeds(???, ???);
    }
```
**Solution:**
```C++
    void turnOffMotors() {
        motors.setSpeeds(0, 0);
    }
```
Let's try using these new functions to make our previous code easier to understand.

**Solution:**
```C++
    void setup() {
        turnOnMotors();
        delay(3000);
        turnOffMotors();
    }
```

Let's go back to the original code for the motor's speed `motors.setSpeeds(SPEED, SPEED)`. The function's first **parameter** is the robot's left wheels and the second **parameter** is the robot's right wheels. *What do you think will happen if we change the inputs so that they're not the same? What if they're opposite?*

```C++
    void turnInPlace() {
        motors.setSpeeds(-SPEED, SPEED);
    }
```
We're going to allot some time to allow you guys to experiment with the movement motors on the robot! 
==Lead and helpers walk around, help with code, and encourage the students to have fun with the robot while making sure it doesn't fall!==


### Outro 

(10 minutes)

  * Go over the day's accomplishments
      * Learned about robot movement, libraries, and constants
      * `motors.setSpeeds()`, `turnOnMotors()`, `turnOffMotors()`, `turnInPlace()`
      * Experimenting with the robot's movements
  * What's planned for next week?
      * Buzzers and Sensors!

## Week 3: Conditional Statements and Sensors

* Review of last week (10 minutes)

### Lesson Plan

A lot of coding revolves around **conditional statements**. If you're already familiar with coding, you may recognize them as `if`-`then`-`else` statements.

#### Conditional Statements

``` C++
    int x = 5;
    if (x > 10) {
        // number is greater than 10
        // does some code
    } else {
        // number is less than or equal to 10
        // does nothing
    }
```
Here, x is a **variable**. It's similar to a constant in that it stores data, but a variable could change in the middle of a program.

The statement inside the parentheses is a **Boolean** value, which means it can either be **true** or **false**. *In the example above, is* `x > 10` *true or false?* That means our program only does something if the integer `x` is greater than 10.

If you flip your Arduino Zumo upside down, you will see six sensors. These sensors detect how light or dark the surface under it is. Tying this back to what we were doing last week with movement, what if I wanted my robot to move until it hit this black strip of electrical tape? We would use a conditional statement, similar to our simple program here (x > 10 program).

#### Arrays and Sensors

We're going to represent the set of six sensors as an **array**. An array in C++ is a collection of data items. See `int values[6] = {3, 2, 12, 54, 2, 1}`. `values` is the name of the array, [6] is the size of the array, and `int` is the data type that's allowed to be in the array. `{3, 2, 12, 54, 2, 1}` is the values in the actual array and notice these are all `int`s. 

Each space in the array is used to store a number similar to the constants and variables we worked with before. To access the numbers in the array, we type `values[number]` where `number` is the location of the value, starting at 0. `values[0]` would be `3`, `values[1]` would be `2`, `values[2]` would be `12`, and so on. 

What we're going to do is have the sensors feed their inputs -- what they "see" -- into the array. This way, we can check for when the sensor detects something. Today we'll be adding onto the code we worked on last week with the motors.

```C++
    #include <ZumoReflectanceSensorArray.h> //new
    #include <ZumoMotors.h>

    const int DETECTION_THRESHOLD = 1300; // new
    const int SPEED = 100;
    int values[6];

    ZumoReflectanceSensorArray sensors; //new
    ZumoMotors motors;

    void setup() {
        sensors.init(); // new
    }

    void loop() {
        sensors.read(values); // new
    }
    
    void turnOnMotors() { motors.setSpeeds(SPEED, SPEED); }

    void turnOffMotors() { motors.setSpeeds(0, 0); }

    void turnInPlace() { motors.setSpeeds(-SPEED, SPEED); }
    
```

Here's a simple program where if the sensors detect a dark line, it activates its LED.

```C++
    void loop() {
        sensors.read(values);
        if (values[0] > DETECTION_THRESHOLD) {
            digitalWrite(LED_PIN, HIGH);
        }
    }
```

Using the functions we wrote last week, can you guys write a program that starts with the robot moving and then the robot comes to a stop when it detects a black line? 
==Lead and helpers walk around and help.==

**Solution:**
```C++
void loop() {
    sensors.read(values);
    turnOnMotors();
    if (values[0] > DETECTION_THRESHOLD) {
        turnOffMotors();
    }
}
```

#### Debugging with Serial Monitor*

*Only include if time allows AND lots of students are struggling with the robot's sensors detecting the line

The Serial Monitor allows you to print data to your screen. It's similar to the various `print` commands in other programming languages. You can use it to debug your code, in this case, to check the values of the robots's sensors.

```C++
void setup() {
	Serial.begin(9600);
}

void loop() {
    Serial.print(values[0]);
}
```

This will output the value stored in sensor 0 to your screen so you can see them in real time. Keep in mind that sensor 0 is the left-most sensor. Use this information to tweak the `DETECTION_THRESHOLD` constant in your code so your robot stops at the line!

### Outro

(10 minutes)

  * Go over the day's accomplishments
      * Learned about conditional statements, variables, arrays, and sensors
      * `sensors.init()`, `sensors.read()`, `if`-`else`
      * Experimenting with the robot's sensors and movements
  * What's planned for next week?
      * Buzzers!

## Week 4: Buzzers

* Review of last week (10 minutes)

### Lesson Plan

Our Arduino Zumo also has the capacity to produce sounds!

#### Buzzers

At the top of your old program, include this **helper code**:

```C++
#include <ZumoBuzzer.h>

int VOLUME = 9; 
int DURATION = 500;

ZumoBuzzer buzzer;
```

This code is very similar to the code we needed to include for the ZumoMotors section. One thing of note is that the **maximum volume on our Arduino is 15** and **the minimum is 9**. Any lower and the Arduino will not output any sound.

*Who here is familiar with playing and reading music?* As a refresher, notes have a pitch (typically represented by a letter) and a duration based on the number of beats.

The command that we will use to actually play sound is `buzzer.playNote(note, length, volume)`.

The `note` parameter will look like `NOTE_C(4)`. If played, this will play the C4 note also known as Middle C. You can change the letter and the octave to play any note on the scale. We won't be making music exactly, so don't worry about which note you choose, as long as the octave is around 3 to 5.

The `length` parameter will use our `DURATION` constant we used earlier. It is currently set at `500` for 500ms or half a second. If you want the robot to play for longer than that, you can multiply it in the function call.

The `volume` parameter will simply use our `VOLUME` constant.

One last thing before we implement this into our program: after the `buzzer.playNote()` call, we must **wait** or `delay()` for the same amount of time. If not, it will lead to overlap in the sounds.

Since we always have to `delay` after using `playNote()`, why don't we create a function that does that?

**Solution:**
```
void myPlayNote(int note, int length)
{
  buzzer.playNote(note, length, VOLUME);
  delay(length);
}
```

Recall our program that used conditional statements and the sensor. You should have this open.
```C++
void loop() {
    sensors.read(values);
    turnOnMotors();
    if (values[0] > DETECTION_THRESHOLD) {
        turnOffMotors();
    }
}
```
Can you make it so the Arduino plays 3 beeps of all different notes that each last a quarter of a second when it stops?

**Solution:** (up to this point)
```C++
#include <ZumoMotors.h>
#include <ZumoReflectanceSensorArray.h>
#include <ZumoBuzzer.h> // NEW

int VOLUME = 9; // NEW
int DURATION = 500; // NEW
const int DETECTION_THRESHOLD = 1300;
const int LED_PIN = 13;
const int SPEED = 100;
int values[6];

ZumoMotors motors;
ZumoReflectanceSensorArray sensors;
ZumoBuzzer buzzer; // NEW

void setup() {
  sensors.init();
}

void loop() {
    sensors.read(values);
    turnOnMotors();
    if (values[0] > DETECTION_THRESHOLD) {
        turnOffMotors();
        myPlayNote(NOTE_C(4), DURATION / 2); // NEW
        myPlayNote(NOTE_B(5), DURATION / 2); // NEW
        myPlayNote(NOTE_D(5), DURATION / 2); // NEW
    }
}

void turnOnMotors()
{
  motors.setSpeeds(SPEED, SPEED);
}

void turnOffMotors()
{
  motors.setSpeeds(0, 0);
}

void turnInPlace()
{
  motors.setSpeeds(-SPEED, SPEED);
}

void myPlayNote(int note, int length) // NEW
{
  buzzer.playNote(note, length, VOLUME);
  delay(length);
}
```

Now it's time to experiment with incorporating the buzzer into fun routines that you create for your robot!

### Outro 

(10 minutes)

* Go over the day's accomplishments
    * Learned about the buzzer function
    * `buzzer.playNote()`, `myPlayNote()`
    * Further experimentation with the Arduino's movements, sensors, and buzzers
* What's planned for next week?
    * Brief final project!