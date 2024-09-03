# ESP32-CAM-Arduino-and-OpenCV

The ESP32-CAM is a compact and affordable development board designed for applications involving video streaming, image capture, and low-power IoT projects. It integrates an ESP32-S microcontroller with built-in Wi-Fi and Bluetooth capabilities, along with a camera module, making it an excellent choice for wireless surveillance, face recognition, or remote monitoring projects.

![image](https://github.com/user-attachments/assets/8f40cbfd-1e97-4f99-9699-7b2b19d9c931)

We will be using an ESP32-CAM-MB, which is an upgraded version of the ESP32-CAM module that includes an additional base board called "MB" (Module Base). This base board is designed to simplify programming and powering the ESP32-CAM, eliminating the need for a separate FTDI adapter (USB to serial converter) when uploading code or powering the device.

The MB base board includes a micro USB or USB-C connector (depending on the version), allowing you to connect the ESP32-CAM directly to a computer for programming and power without extra hardware.

![image](https://github.com/user-attachments/assets/f6d115f7-9af9-4ee6-981e-735190808bfd)

Once we have both pieces joined together, we can start the instalation process.

# STEP 1 Install Arduino

Arduino can be installed from its own webpage. Check if the download option suits your device OS (Windows/Linux/macOS). I am using the 2.3.2 version.

Click on this [link](https://www.arduino.cc/en/software) to go to the download webpage.

# STEP 2 Additional URL Manager

The first step is to open the Arduino IDE and access the board URL manager by clicking on File/Preferences/Additional Boards Manager URLs and adding the following link:

https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json


# STEP 3 Install ESP32 Board Manager

You can either click on the board icon on the left and search for the Espressif Systems esp32 Board Manager, or click on tools/board:""/boards manager. Newest versions work properly (at least the one I am using).

![image](https://github.com/user-attachments/assets/8c912a14-7f0a-478f-9cf8-f1e2619226dc)

# STEP 4 Select the board and port

Board has to be selected in /tools/board:"*****"/esp32/

We need to find * AI Thinker ESP32-CAM *. As there are plenty of them, it should appear more or less below all the Heltec Boards: 

![image](https://github.com/user-attachments/assets/06264973-118e-4e09-b633-bafcdf7816c7)

(ESP32 Wrover Module can also be used)

It is really important to select the port in tools/port 
Sometimes, the computer does not recognize the ESP32. In some occasions, this is due to the wire connecting the ESP32 and the PC, check that it is appropiate.

As soon as you connect the USB, a new COM port should appear to be connected to. If not, this can be solved installing the driver CH340.
This driver belongs to the CH340 chip, which allows us to use our PC's USB on one side and, on the other side, convert the communications we send to the ESP32 into serial format.

I`ll provide you one, but it can be downloaded from any webpage.

[](https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all)
