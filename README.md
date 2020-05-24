# raspivid IP Camera
Using raspivid as streaming IP Camera and use it in (for example) Zoneminder.

## Installation
Make sure the raspi camera is enabled in raspi-config...

* Place raspivid.service in /etc/systemd/system
* enable service: ```sudo systemctl enable raspivid```
* start: ```sudo systemctl start raspivid```

Other options:
* stop:  ```sudo systemctl stop raspivid```
* restart:  ```sudo systemctl restart raspivid```

## GPU Memory
If you are seeing errors like this:

```raspivid[746]: mmal: Failed to write buffer data (4096 from 120376)- aborting```

This can be caused by not having assiged enough gpu memory (or by selecting an image size wiich is too large). Either assign more gpu memory (if possible) or lower the requested video size. The gpu memory gcan be assigned in raspi0config > Advanced options

## Configure in Zoneminder
To use this camera in Zoneminder, create a new Monitor / camera and set the following properties:
* General tab
  * Source Type: ffmpeg
* Source Tab
  * Source path: ```tcp://<hostname or ip>:<port>```
    ```tcp://10.0.0.1:8081```
  * Method: TCP
  * Target Colorspace: 32 bit
  * Capture resolution: set to size set in raspivid.service: for example: 2592x1944
