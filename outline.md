# Outline for School Outreach Program

* Each day is ~90 minutes

## Initial setup
Arrange with teachers to ensure that the Arduino IDE is installed on student computers: https://arduino.cc/download/

## Week 1: Intro to Programming and LEDs

* Introduction (5 minutes)
    * Introduce ourselves, WiC, and MESA
    * Briefly go over the program
* Students introduce themselves (20 minutes)
    * Name and year
    * Why did you sign up for this program?
    * Have you programmed before?
    * One fun fact about yourself :)*
* Lecture (20 minutes)
    * What is a program?
        * Talk about how computers require you to be very specific
        * It might seem hard, but we'll learn bit-by-bit
        * **Show the make-up of an Arduino program with a screenshot**
    * What is a Zumo?
    * What is an Arduino?
* Hands-on programming (40 minutes)
    * Open the Arduino IDE
    * Install the ZumoShield library
    * Program comes preloaded with two functions, `setup()` and `loop()`
    * A function is a block of reusable code that does something specific
    * Setup is played once at the beginning
    * Loop loops
    
``` C++
    void setup() {
        pinMode(13, OUTPUT);
        digitalWrite(13, HIGH);
}
```

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
* Outro (5 minutes)
    * Go over the day's accomplishments
        * Learned about our Arduino Zumo robot, programs, and functions
        * `pinMode()`, `digitalWrite()`, and `delay()`
        * Hands-on coding with the Arduino Zumo's LED
    * What's planned for next week?
        * Making the robot move!

## Week 2: Functions and Motors

* Review of last week (10 minutes)
* Students install ZumoShield library (necessary in order to use Zumo header files) (5 minutes)
* Lesson (55 minutes)
    * Helper code for today, include at top of program, above setup():
```C++
    #include <ZumoMotors.h>
    const int SPEED = 100;
    ZumoMotors motors;
```

**Explain while the students copy the code.**

`include <ZumoMotors.h>`: ZumoMotors is a **library**, pre-written code made by a programmer so we can do specific things, in this case, making our robot move. Someone has written all the functions to make the robot move - this statement takes the contents of the file "ZumoMotors.h" and copies and pastes it into our code, so we can use them in our program. Note there is no semicolon at the end of the line!

`const int SPEED = 100;` is us making a **constant**, that is called `SPEED`. Compare it to a variable in math where x or y can stand for certain numbers like how in x + 4 = 6, x stands for 2. It's similar in programming, but constants are basically containers for information or **data** as we call it. Think of it like every time we write `SPEED` in our program, the computer knows it actually means `100`. `int` is short for integer, meaning that `SPEED` represents an integer. `const` means that `SPEED` can't change throughout our program, which will be important.

`ZumoMotors motors;` allows us to use the ZumoMotors code in our program.

`motors.setSpeeds(SPEED, SPEED)` is code from the **library** we imported earlier. The two numbers inside the parentheses are **arguments**. Think of them like inputs to the function. *What do you guys think will happen if we ran this code, knowing it relates to the movement motors?* However, it would probably get hard to retype over and over again. We made our own variable earlier with `SPEED`, why don't we try writing our own functions as well? 

```C++
    void turnOnMotors() {
        motors.setSpeeds(SPEED, SPEED);
    }
```
Now everytime we write `turnOnMotors();`, it will run the `motors.setSpeeds(SPEED, SPEED)` code inside of it. Before we test it out, we should have a function that turns off the motors as well. *Does anyone know what number we could put here to make the robot stop moving?*
```C++
    void turnOffMotors() {
        motors.setSpeeds(???, ???)
    }
```
**Solution:**
```C++
    void turnOffMotors() {
        motors.setSpeeds(0, 0)
    }
```
Let's try to think back to our lesson last week where we made the robot's LED to flash for 3 seconds and then stop. *Do you guys think you can modify the code we had last week to make it move for 3 seconds and then come to a stop?*

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
We're going to allot some time to allow you guys to experiment with the movement motors on the robot! **Lead and helpers walk around, help with code, and encourage the students to have fun with the robot while making sure it doesn't fall!**


* Outro (10 minutes)
    * Go over the day's accomplishments
        * Learned about robot movement, libraries, and constants
        * `motors.setSpeeds()`, `turnOnMotors()`, `turnOffMotors()`, `turnInPlace()`
        * Experimenting with the robot's movements
    * What's planned for next week?
        * Buzzers and Sensors!

## Week 3: Conditional Statements and Sensors

* Review of last week (10 minutes)
* Lesson (60 minutes)
  * A lot of coding revolves around **conditional statements**. If you're already familiar with coding, you may recognize them as `if`-`then`-`else` statements.
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
The statement inside the parentheses is a **Boolean** value, which means it can either be **true** or **false**. *In the example above, is `x > 10` true or false?* That means our program only does something if the integer `x` is greater than 10.

If you flip your Arduino Zumo upside down, you will see six sensors. These sensors detect how light or dark the surface under it is. Tying this back to what we were doing last week with movement, what if I wanted my robot to move until it hit this black strip of electrical tape? We would use a conditional statement, similar to our simple program here (x > 10 program).
