facetrack
=========

OpenCV face tracking on the Raspberry Pi using Python


Core code borrowed from [Pan / Tilt face tracking with the raspberry pi](http://instructables.com/id/Pan-Tilt-face-tracking-with-the-raspberry-pi "instructables")

To install the RPIO library, you can use the following:
```
sudo apt-get install python-setuptools
sudo easy_install -U RPIO
```


RPIO docs are [here](http://pythonhosted.org/RPIO/rpio_py.html) if you need them.


Additional Info
---------------
I replaced the calls to ServoBlaster with RPIO just to keep everything a little more in the Python realm codewise.  The RPIO library is generally a drop-in replacement for RPi.GPIO, but is usually a few steps ahead of it in terms of features.  One thing to keep in mind is that you probably don't want to import both RPi.GPIO and RPIO in the same project as they'll step on each other.

RPi.GPIO doesn't work for this project because it's implementation of PWM is software based, and the resulting signal is too erratic to control the servos smoothly enough for OpenCV tracking.  RPIO (and ServoBlaster) uses DMA and while not a full hardware implementation, it removes enough servo jitter to be usable.

