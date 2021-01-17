# piCAMTracker
This is another Raspberry Pi motion tracker based on Python, picamera and opencv.   
It makes heavily use of the motion blocks generated by GPU of the Raspberry Pi.   
**Target** A crossing event is detected on a GPIO port and a picture of the event is transmitted via nginx to a smart phone for example.
# News
2021-01-17: [V0.6.4](https://drive.google.com/file/d/1xuHntIMFQ1BPVGnHj9Ad_DN_oLKLxGlQ/view?usp=sharing) image released today. There are no code changes included.
            The operating system has been updated to the latest. Tested on RPi4 only. (No further updates needed so far)
            
2019-12-01: [V0.6.3](https://drive.google.com/open?id=14-Zqk-uW1Q9dErGkBKbVC-Mp4glUpEsP) image released today. You need to install this image because development now depends on the latest Raspbian Buster operating system. Simple updates (git pull) will not work any longer on the v0.4 and v0.5 based systems. This image is running on Raspberry 4 B, 3 B and 3 B Plus.
To enable the filemanager again you need to upgrade the operating system with the following command:
```
sudo update
sudo apt full-upgrade
sudo apt-get upgrade
```
 
# Status
* The new Raspberry Pi 4 Model B is working now. I don't have tested the power consumption yet. (Internal speed is improved a lot. Framerate is limited by lightning conditions, camera and GPU wich has not been changed)
* The Raspberry now provides a Wifi hotspot (PICAM/Olav0101) in parallel to the Wifi client. You can use the Raspberry in your local Wifi environment without any changes. In parallel it will provide a Wifi hotspot (name is configurable via the config.json file) and you can connect via http://192.168.16.1 to the piCAMTracker web interface. 
* You need to enable the access point in config.json
* The object detection is working quiet well in different light conditions.
  * Low light performance increased a lot by variable framerate adaption.
  * Dark backgrounds may be lightened by manually configurable exposure compensation. (to be verified) 
* The object detection has limits: 
  * The camera cannot distinguish between birds/bees and planes. All moving things are evaluated.
  * moving objects in the turn area can lead to false positives. (grass, bushes, flags, etc)
  * The minimum distance for fast moving objecst should be 7 meters. Objects moving too fast in front of the camera cannot be detected by the internal algorithm. (rule of thumb is trackMaturity x 2 in meters for a plane flying 40 m/s)
  * to make faster movements possible I implemented a bypass of the full tracking. We have to evaluate if this option is usefull.
  * The fisheye setup with the V1 camera seems to be the best setup for our purposes. (F3F model air racing)
  * If you want to follow up more far away objects (F3B speed for example) the newer V2 camera is the better choice.
  * To improve nearby crossing detection the camera could be mounted straight. (Not in 90 degrees as used before)
    * Crossing is now in X direction (viewAngle: 0, xCross: 40, yCross: -1)  
* V1 camera from Waveshare with fisheye lens (module G); 1280x960 pixels, 42 f/s; full FOV; 192MB GPU memory
  * Mode 5 (1280x720p @ 49 f/s) does not center the frames horizontally
* V2 camera with standard lens; 1632x896, 40 f/s; full FOV; 192MB GPU memory.
  * 1280x720p @ 62 f/s (FOV is very small)
  * In general the V2 camera needs more light than the V1 with the fisheye
* In stormy conditions you need to fix the camera very well. Otherwise a lot of wrong positives are genenrated.
* The web interface supports the most rudimentary stuff to control the camera.
* Up to 5 short video sequences (15 seconds) are saved by pressing the debug button. (todo: move them  to USB stick if connected)   
* we have a printed cover available. (see wiki section)
* you can download the V0.6.4 image [here](https://drive.google.com/file/d/1xuHntIMFQ1BPVGnHj9Ad_DN_oLKLxGlQ/view?usp=sharing)
  pi-password: Olav01
* you can download the V0.6.3 image [here](https://drive.google.com/open?id=14-Zqk-uW1Q9dErGkBKbVC-Mp4glUpEsP)
  pi-password: Olav01
* The v0.6.X images are created on a Raspberry 4 B.

# FAQ
see [FAQ](https://github.com/barney-NG/piCAMTracker/wiki/FAQ) section

# Documentation
see [wiki](https://github.com/barney-NG/piCAMTracker/wiki) section

# TODO
* More testing in real conditions is needed.
