facetrack
=========

OpenCV face tracking on the Raspberry Pi using Python
```
sudo apt-get install python-opencv
```
Be sure to enable the camera on the Raspberry pi and add bcm2835-v4l2 to /etc/modules

Core code borrowed from [Pan / Tilt face tracking with the raspberry pi](http://instructables.com/id/Pan-Tilt-face-tracking-with-the-raspberry-pi "instructables")

If not preinstalled with Raspbian, you can use the following to install the PIGPIO library:
```
wget abyz.co.uk/rpi/pigpio/pigpio.zip
unzip pigpio.zip
cd PIGPIO
make
sudo make install

#setup pigpiod to auto load by adding a line to crontab
sudo crontab -e
@reboot  /usr/local/bin/pigpiod
```


PIGPIO docs are [here](http://abyz.me.uk/rpi/pigpio/python.html) if you need them.


Additional Info
---------------
I replaced the calls to ServoBlaster with ~~RPIO~~ PIGPIO just to keep everything a little more in the Python realm codewise.  The RPIO library has had a history of not keeping up with hardware updates so I switched over to pigpio which is now included as part of the default raspian installation.

RPi.GPIO doesn't work for this project because it's implementation of PWM is software based, and the resulting signal is too erratic to control the servos smoothly enough for OpenCV tracking.  RPIO (and ServoBlaster) uses DMA and while not a full hardware implementation, it removes enough servo jitter to be usable.

