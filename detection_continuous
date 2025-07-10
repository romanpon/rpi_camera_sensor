import RPi.GPIO as GPIO
import subprocess
from datetime import datetime, timedelta
import time
import signal
import os

GPIO.setmode(GPIO.BOARD)
pir_pin = 7  # change to your connected GPIO pin
GPIO.setup(pir_pin, GPIO.IN)

# How long to wait with no motion before stopping
no_motion_timeout = timedelta(seconds=7)

print(f"Sensor initialized at {datetime.now()}")
time.sleep(3)
print(f"Detecting motion at {datetime.now()}")

recording = False
last_motion_time = None
gphoto_proc = None

def stop_recording():
    global recording, gphoto_proc
    if recording:
        print(f"No motion for {no_motion_timeout.seconds}s — stopping recording at {datetime.now()}")
        # send the gphoto2 stop command
        subprocess.call(["gphoto2", "--set-config", "movie=0"])
        recording = False
        gphoto_proc = None

try:
    while True:
        if GPIO.input(pir_pin):
            now = datetime.now()
            print(f"Motion detected at {now}")
            last_motion_time = now

            if not recording:
                print(f"Starting recording at {now}")
                # start recording indefinitely
                subprocess.call(["gphoto2", "--set-config", "movie=1"])
                recording = True

        # if we're recording, check whether we've gone too long with no motion
        if recording and last_motion_time:
            if datetime.now() - last_motion_time > no_motion_timeout:
                stop_recording()

        time.sleep(0.5)  # poll twice per second

except KeyboardInterrupt:
    print("Interrupted — cleaning up.")
finally:
    # ensure we stop recording if exiting
    stop_recording()
    GPIO.cleanup()
