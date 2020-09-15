# SG90 servo range correction

*A Python script for the SG90 servo to achieve the full 180 degrees moving range*

![SG90 image](/images/sg90.jpg)

## What's the problem?

GPIO Zero package is traditionally used for the ubiquitous SG90 servo. But after connecting the servo to your Raspberry Pi and testing the servo's maximum and minimum positions you will notice it only moved +45/-45 degrees. What's the matter?

## How to fix?

Using GPIO Zero assumes that the servo uses a signal frame width of 20ms, while the pulse width for the minimum and maximum rotation is assumed to be accordingly 1ms and 2ms. This information is available in the servo specification.

As you can see in the picture below, position "0" (1.5 ms pulse) is middle, "90" (~2ms pulse) is all the way to the right, "-90" (~1ms pulse) is all the way to the left.

![SG90 image](/images/sg90_pwm.jpg)

But if you start using the servo with these default settings you will quickly find that your servo does not move a full 180 degrees from minimum to maximum as it should be.

To fix this issue you should change the pulse width parameters in order to get a full 90 degrees of rotation in either direction. Min setting has to be decreased, while the max otherwise to be increased by the value in the range 0.45 - 0.55 (0.5 on average).

The code attached helps to find the right values for these parameters.

## Code explanation

The code has detailed comments so use them for understanding what the code does. 

In short, it takes the correction value you entered and applies it to the servo minimum and maximum pulse widths. After that, the servo moves its arm from mid to min position, then back to mid, to the max, and again to mid.

You could start from the average value of 0.5 and then increase/decrease the correction value in increments of 0.05. This will allows you to find the best change you could make to reach the full 180 degrees range.

If you see the correction value is right (the servo moves the full range), you answer "Yes" when the program asks you, and "No" otherwise thus repeating the loop until the appropriate value will be entered.

## Acknowledgements

I am grateful to the people who noticed the same issue for the servo and offered their code to fix, among them **Matt Hawkins** with his article [Basic Servo Use With the Raspberry Pi and GpioZero](https://www.raspberrypi-spy.co.uk/2018/02/basic-servo-use-with-the-raspberry-pi/), also **Colin Dow** with his book [Internet of Things Programming Projects](https://github.com/PacktPublishing/Internet-of-Things-Programming-Projects).
