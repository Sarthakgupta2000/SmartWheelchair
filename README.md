# SmartWheelchair
SmartWheelchair using arduino

The circuit consists of two ultrasonic three pin sensors, one buzzer, one push-button, slide-switch, rgb light, two dc motors with an H-bridge motor driver and a 9-volt battery.

I have developed a Smart Wheelchair with obstacle detection and temporary avoidance 
as product to be helpful for the differently-abled. 
What we have used here are the following components- Two dc motors with a H-bridge 
motor driver, IR sensor with IR remote, RGB led with slide-switch, piezo buzzer with 
pushbutton, two ultrasonic sensors and finally an Arduino UNO 3 board. 
Instead, if IR remote, sensor we may also use a Bluetooth module in our project according 
to convenience/requirement. 
Basically, what our Smart wheelchair can do is – you can control its movements :-
(forward, rotate right/left, backward and stopping) using the remote. 
The two ultrasonic sensors detect obstacle when moving forward (obstacle in range of 
20cm) and automatically rotates right (for convenience - built-in, setting can be modified 
later).
It includes an RGB light that stays on so other people can easily detect location at night. 
This led also changes colour on different operation: -
green for normal movement, blue for change in movement using remote, and red for 
obstacle detection.
The led can be switched off using slide switch during the day if not required. 
We also have a pushbutton for buzzer in cases of emergency which also changes red 
colour to red. 

![SmartWheelchair](https://user-images.githubusercontent.com/51722099/117536510-fa4d3680-b018-11eb-8ebb-cd107a0c3691.png)


Flowchart for working logic

![SmartWheelchairArduinoTinkercad](https://user-images.githubusercontent.com/51722099/117581759-1e457080-b11c-11eb-965c-2e3002ebfbdf.png)
