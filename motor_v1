import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)

class Motor:
    'The motor class, will control on/off status'

    # 0 --> Stopped
    # 1 --> Going Forward
    # 2 --> Going Reverse
    running = 0


    PIN_NUMBER_FORWARD = 18
    PIN_NUMBER_REVERSE = 19
    

    GPIO.setwarnings(False)

    def __init__(self):
        self.running = 0
        self.PIN_NUMBER_FORWARD = 18
        self.PIN_NUMBER_REVERSE = 19
        
        GPIO.cleanup(self.PIN_NUMBER_FORWARD)
        GPIO.cleanup(self.PIN_NUMBER_REVERSE)
        
        GPIO.setup(self.PIN_NUMBER_FORWARD, GPIO.OUT)
        GPIO.setup(self.PIN_NUMBER_REVERSE, GPIO.OUT)

    def turnOnPin(self, pin_number):
        GPIO.output(pin_number, GPIO.HIGH)
        
    def turnOffPin(self, pin_number):
        GPIO.output(pin_number, GPIO.LOW)


    

    def power(self, command):
        if (command == 'on'):
            if(self.running > 0):
                print("Motor is already running")
            else:
                self.turnOnPin(self.PIN_NUMBER_FORWARD)
                self.running = 1
        if (command == "off"):
            if(self.running > 0):
                self.turnOffPin(self.PIN_NUMBER_FORWARD)
                self.turnOffPin(self.PIN_NUMBER_REVERSE)
                self.running = 0
                
            else:
                print("Motor is already off")

    def direction(self, command):
        if (command == 'forward'):
            if(self.running == 1):
                print("Motor is already running forward")
            elif(self.running == 2):
                self.running = 1
                self.turnOffPin(self.PIN_NUMBER_REVERSE)
                time.sleep(1)
                self.turnOnPin(self.PIN_NUMBER_FORWARD)

                
        if (command == "reverse"):
            if(self.running == 2):
                print("Motor is already in reverse, bitch")
            elif(self.running == 1):
                self.running = 2
                self.turnOffPin(self.PIN_NUMBER_FORWARD)
                time.sleep(1)
                self.turnOnPin(self.PIN_NUMBER_REVERSE)
                


    def controller(self):
        command = ''
        command = input("Type in the motor command ")
        self.power(command)
        self.direction(command)
