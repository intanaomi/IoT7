from time import *
from gpio import *
from ioeclient import *
from physical import *

def onInputReceive(input):
	if input == "0":
		print("going up")
		moveBy(0, -20)
	elif input == "1":
		print("going down")
		moveBy(0, 20);
	elif input == "2":
		print("going left")
		moveBy(-20, 0);
	elif input == "3":
		print("going right")
		moveBy(20, 0);
	else:
		print("stop")

		

def main():
	# Setup Registration Server	
	IoEClient.setup({
		"type": "Car",
		"states": [{
			"name": "Direction",
			"type": "options",
			"options": {
				"0" : "Up",
				"1" : "Down",
				"2" : "Left",
				"3" : "Right",
				"4" : "Stop"
			},
			"controllable": True
		}]
	});

	IoEClient.onInputReceive(onInputReceive)

	while True:
		delay(500)

if __name__ == "__main__":
	main()
