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

https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all

There is another much easier way to select both board and port which is by clicking on the highlighted button on top with the name of the board, and then click on "select other board and port".

![image](https://github.com/user-attachments/assets/c9072d8c-5b6e-4417-a5dc-27804e94c5fd)

![image](https://github.com/user-attachments/assets/16a4588f-a5f5-4126-b968-a3825dd7f817)

# STEP 5 Test the camera

Once all of this is done, we can test the camera from the ESP32 with an already provided code. You can find it in File/examples/ESP32/Camera/CameraWebServer

![image](https://github.com/user-attachments/assets/3486db22-1608-4281-b7f2-98f3abaf7d7e)

# STEP 6 Modify the code

First of all we need to comment the default camera model and use the AI thinker cam:

![image](https://github.com/user-attachments/assets/67850573-b91a-4d12-9693-1a6a5b1d7435)

Then, we need to add an ssid and a password to connect to wifi in this part of the code: 
```
const char *ssid = "**********";
const char *password = "**********";
```
Eg.
```
const char *ssid = "*budaphone5G";
const char *password = "3d6hB46f";
```
Once it is done, we can upload the code to the ESP32 by clicking on the top left arrow. It does not only debug the code, but also uploads it.

![image](https://github.com/user-attachments/assets/57046f99-ba3b-4670-b0d9-b6a6ddd05fb3)

To see what is happening, we need to open the Serial monitor, if it does not appear below, we can open it up by clicking on the top right corner icon: 

![image](https://github.com/user-attachments/assets/0b68f915-9082-4d19-87c2-52e092b4a7ba)

It is important to set the Serial Monitor with the same frecuency as the Serial is set with, in this case: 

![image](https://github.com/user-attachments/assets/c89f7077-8ade-4ce8-8039-05f94cc705e5)
![image](https://github.com/user-attachments/assets/9b9ae6a4-ee9d-40e5-8575-ac0a4da54927)

It is important to press the reset button on the ESP32 once the code is uploaded, in case something went wrong.

![image](https://github.com/user-attachments/assets/8e1c1056-8939-4158-acd6-a40fe58f2d03)

If the code was successfully uploaded, you will get a message like this: 
![image](https://github.com/user-attachments/assets/ef1cd6b2-52ec-40ee-aac4-c263ea8b7903)

It shows your device IP, and the webpage to see what the camera is seeing.
It is important that the device in wich you are using the browser to search this webpage, is connected to the same network.

# STEP 7 Open camera web server

If we click on the "Start Stream" button below the menu, we can start streaming!

![image](https://github.com/user-attachments/assets/e124a15f-a7ef-47c3-8d54-0282c110b5d8)

