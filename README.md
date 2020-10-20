## Nema23_TB6600_Python
Code to show how to use a nema 23 with a TB6600 controller and python

### Wiring Diagram:
<a href="https://raw.githubusercontent.com/danielwilczak101/Nema23_TB6600_Python/main/images/stepper_motor_wire_diagram.png">
<img  src="https://raw.githubusercontent.com/danielwilczak101/Nema23_TB6600_Python/main/images/stepper_motor_wire_diagram.png" height="500"></a>

### Raspberry PI Pins:
<a href="https://raw.githubusercontent.com/danielwilczak101/Nema23_TB6600_Python/main/images/Raspberry-Pi-GPIO-Header-with-Photo.png">
<img  src="https://raw.githubusercontent.com/danielwilczak101/Nema23_TB6600_Python/main/images/Raspberry-Pi-GPIO-Header-with-Photo.png" height="500"></a>

### Code:
```py
import RPi.GPIO as GPIO
from time import sleep

# Direction pin from controller
DIR = 10
# Step pin from controller
STEP = 8
# 0/1 used to signify clockwise or counterclockwise.
CW = 1
CCW = 0

# Setup pin layout on PI
GPIO.setmode(GPIO.BOARD)

# Establish Pins in software
GPIO.setup(DIR, GPIO.OUT)
GPIO.setup(STEP, GPIO.OUT)

# Set the first direction you want it to spin
GPIO.output(DIR, CW)

try:
	# Run forever.
	while True:

		"""Change Direction: Changing direction requires time to switch. The
		time is dictated by the stepper motor and controller. """
		sleep(1.0)
		# Esablish the direction you want to go
		GPIO.output(DIR,CW)

		# Run for 440 steps. This will change based on how you set you controller
		for x in range(440):

			# Set one coil winding to high
			GPIO.output(STEP,GPIO.HIGH)
			# Allow it to get there.
			sleep(.0010) # Dictates how fast stepper motor will run
			# Set coil winding to low
			GPIO.output(STEP,GPIO.LOW)
			sleep(.0010) # Dictates how fast stepper motor will run

		"""Change Direction: Changing direction requires time to switch. The
		time is dictated by the stepper motor and controller. """
		sleep(1.0)
		GPIO.output(DIR,CCW)
		for x in range(440):
			GPIO.output(STEP,GPIO.HIGH)
			sleep(.0010)
			GPIO.output(STEP,GPIO.LOW)
			sleep(.0010)

# Once finished clean everything up
except KeyboardInterrupt:
	print("cleanup")
	GPIO.cleanup()
  ```
