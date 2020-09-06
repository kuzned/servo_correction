# SG90 servo range correction

![SG90 image](/images/sg90.jpg)

## What's the problem?

GPIO Zero package is traditionally used for ubiquitous SG90 servo. But after connecting the servo to your Raspberry Pi and testing servo's maximum and minimum positions you will notice it only moved +45/-45 degrees. What's the matter?

## How to fix?

Using GPIO Zero assumes that the servo uses a signal frame width of 20ms, while the pulse width for the minimum and maximum rotation is assumed to be accordingly 1ms and 2ms. This information is available in the servo specification.

But if you start using the servo with these default settings you will quickly find that that your servo does not move a full 180 degrees from minimum to maximum as it should be.

To fix this issue you should change the pulse width parameters in order to get a full 90 degrees of rotation in either direction. The code attached helps to find right values for these parameters.

## Code explanation

The code has detail comments so use them for understanding what the code does. 

In short, it takes the correction value you entered and applies it to the servo minimum and maximum pulse widths. After that, the servo moves its needle from mid to min position, then back to mid, to max and again to mid. 

If you see the correction value is right (the servo moves full 180 degree), you answer "Yes" when the program asks you, and "No" otherwise thus repeating the loop until the appropriate value will be entered.
