## YouTube tutorial video
English: https://www.youtube.com/watch?v=u2O082hDafs
	
	
## What you need?
- A camera, I used SONY A6300
- Raspberry Pi, mine is version 2 model B
- HC-SR501 motion sensor
	
	
## Here are the steps for the Raspberry Pi
	Step 1:
		Connect the motion sensor to the Pi 5V, GND and GPIO pin (note the pin number)
		Connect the camera to Pi, make sure it is in PC Remote mode
		
	Step 2:
		Make sure it is updated:
  		ssh pi@raspberrypi.local (default password raspberry, need to wait 1-2 minutes after powering up)
		sudo apt-get update
		sudo apt-get upgrade
		
	Step 3:
		Install git if necessary:
		sudo apt-get install git
		
	Step 4:
		Install gphoto2 lib with this one line command:
		wget https://raw.githubusercontent.com/gonzalo/gphoto2-updater/master/gphoto2-updater.sh && chmod +x gphoto2-updater.sh && sudo ./gphoto2-updater.sh
		More info: http://gphoto.sourceforge.net/
  	Manual alternative:
   		Build and install libgphoto2:
		cd ~
		git clone https://github.com/gphoto/libgphoto2.git
		cd libgphoto2
		./autogen.sh
		make -j4
		sudo make install
		sudo ldconfig

		Build and install gphoto2:
  		cd ~
		git clone https://github.com/gphoto/gphoto2.git
		cd gphoto2
		./autogen.sh
		make -j4
		sudo make install

	Step 5:
		Download the python script detection.py from:
		https://github.com/romanpon/rpi_camera_sensor
	  	git clone https://github.com/romanpon/rpi_camera_sensor.git
    
	Step 6:
		Run the script:
  		cd rpi_camera_sensor
		python ./detection.py
