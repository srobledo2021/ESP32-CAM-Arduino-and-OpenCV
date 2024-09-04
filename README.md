# ESP32-CAM-Arduino-and-OpenCV

The ESP32-CAM is a compact and affordable development board designed for applications involving video streaming, image capture, and low-power IoT projects. It integrates an ESP32-S microcontroller with built-in Wi-Fi and Bluetooth capabilities, along with a camera module, making it an excellent choice for wireless surveillance, face recognition, or remote monitoring projects.

![image](https://github.com/user-attachments/assets/8f40cbfd-1e97-4f99-9699-7b2b19d9c931)

We will be using an ESP32-CAM-MB, which is an upgraded version of the ESP32-CAM module that includes an additional base board called "MB" (Module Base). This base board is designed to simplify programming and powering the ESP32-CAM, eliminating the need for a separate FTDI adapter (USB to serial converter) when uploading code or powering the device.

The MB base board includes a micro USB or USB-C connector (depending on the version), allowing you to connect the ESP32-CAM directly to a computer for programming and power without extra hardware.

![image](https://github.com/user-attachments/assets/f6d115f7-9af9-4ee6-981e-735190808bfd)

Once we have both pieces joined together, we can start the instalation process.

## STEP 1 Install Arduino

Arduino can be installed from its own webpage. Check if the download option suits your device OS (Windows/Linux/macOS). I am using the 2.3.2 version.

Click on this [link](https://www.arduino.cc/en/software) to go to the download webpage.

## STEP 2 Additional URL Manager

The first step is to open the Arduino IDE and access the board URL manager by clicking on File/Preferences/Additional Boards Manager URLs and adding the following link:

https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json

![image](https://github.com/user-attachments/assets/ef960f5e-7570-4a77-9ffb-44d219d5681e)


## STEP 3 Install ESP32 Board Manager

You can either click on the board icon on the left and search for the Espressif Systems esp32 Board Manager, or click on tools/board:""/boards manager. Newest versions work properly (at least the one I am using).

![image](https://github.com/user-attachments/assets/8c912a14-7f0a-478f-9cf8-f1e2619226dc)

## STEP 4 Select the board and port

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

## STEP 5 Test the camera

Once all of this is done, we can test the camera from the ESP32 with an already provided code. You can find it in File/examples/ESP32/Camera/CameraWebServer

![image](https://github.com/user-attachments/assets/3486db22-1608-4281-b7f2-98f3abaf7d7e)

## STEP 6 Modify the code

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

## STEP 7 Open camera web server

We have to use that provided link in a browser.

If we click on the "Start Stream" button below the menu, we can start streaming!

![image](https://github.com/user-attachments/assets/e124a15f-a7ef-47c3-8d54-0282c110b5d8)


![image-17-1024x766](https://github.com/user-attachments/assets/2141b9f9-d8d2-4819-a280-1c1a406887c2)


----------------------------------------------------------------------

# OpenCV 

Once we are able to access that video , we can use any method that can handle openCV to apply its features.

Here is a simple way to do it using Python.

First of all we need to upload a library. It can be downloaded from this github webpage:

https://github.com/yoursunny/esp32cam

Click on code/Download zip

![image](https://github.com/user-attachments/assets/87544c95-3980-4570-a1d4-db43c96af5d5)

Once downloaded add this zip library to Arduino Libray Folder. To do so, follow the following steps:
Sketch -> Include Library -> Add .ZIP Library… -> Navigate to downloaded zip file -> add

Then we need to upload this code via Arduino, to the ESP32:
```
#include <WebServer.h>
#include <WiFi.h>
#include <esp32cam.h>
 
const char* WIFI_SSID = "****";
const char* WIFI_PASS = "****";
 
WebServer server(80);
 
 
static auto loRes = esp32cam::Resolution::find(320, 240);
static auto midRes = esp32cam::Resolution::find(350, 530);
static auto hiRes = esp32cam::Resolution::find(800, 600);
void serveJpg()
{
  auto frame = esp32cam::capture();
  if (frame == nullptr) {
    Serial.println("CAPTURE FAIL");
    server.send(503, "", "");
    return;
  }
  Serial.printf("CAPTURE OK %dx%d %db\n", frame->getWidth(), frame->getHeight(),
                static_cast<int>(frame->size()));
 
  server.setContentLength(frame->size());
  server.send(200, "image/jpeg");
  WiFiClient client = server.client();
  frame->writeTo(client);
}
 
void handleJpgLo()
{
  if (!esp32cam::Camera.changeResolution(loRes)) {
    Serial.println("SET-LO-RES FAIL");
  }
  serveJpg();
}
 
void handleJpgHi()
{
  if (!esp32cam::Camera.changeResolution(hiRes)) {
    Serial.println("SET-HI-RES FAIL");
  }
  serveJpg();
}
 
void handleJpgMid()
{
  if (!esp32cam::Camera.changeResolution(midRes)) {
    Serial.println("SET-MID-RES FAIL");
  }
  serveJpg();
}
 
 
void  setup(){
  Serial.begin(115200);
  Serial.println();
  {
    using namespace esp32cam;
    Config cfg;
    cfg.setPins(pins::AiThinker);
    cfg.setResolution(hiRes);
    cfg.setBufferCount(2);
    cfg.setJpeg(80);
 
    bool ok = Camera.begin(cfg);
    Serial.println(ok ? "CAMERA OK" : "CAMERA FAIL");
  }
  WiFi.persistent(false);
  WiFi.mode(WIFI_STA);
  WiFi.begin(WIFI_SSID, WIFI_PASS);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
  Serial.print("http://");
  Serial.println(WiFi.localIP());
  Serial.println("  /cam-lo.jpg");
  Serial.println("  /cam-hi.jpg");
  Serial.println("  /cam-mid.jpg");
 
  server.on("/cam-lo.jpg", handleJpgLo);
  server.on("/cam-hi.jpg", handleJpgHi);
  server.on("/cam-mid.jpg", handleJpgMid);
 
  server.begin();
}
 
void loop()
{
  server.handleClient();
}
```

Remember to change the ssid and password.
This code will keep publishing images constantly. We can also decide wether we want the low, mid or high resolution.

We need to have Python installed. Here is a [webpage](https://www.python.org/downloads/windows/) if you are using windows instead of linux.

Then go to the command prompt and install NumPy, OpenCV and cvlib libraries. In windows you can find it by typing "cmd" in the search bar below.

![image](https://github.com/user-attachments/assets/46c23dbf-0762-4080-bc98-5bfb74b4c8d9)

Then type:
```
pip install numpy
pip install opencv-python
pip install cvlib
```
If you are using windows and you do not have pip installed, follow the instructions of this webpage and then type the previous commands: 

https://phoenixnap.com/kb/install-pip-windows

After that you can use this python code below to test if everything went alright. 
If not, try these commands first:
```
pip install matplotlib
pip install tensorflow
pip install opencv-python numpy requests

```
This is the code: 
```python
import cv2
import matplotlib.pyplot as plt
import cvlib as cv
import urllib.request
import numpy as np
from cvlib.object_detection import draw_bbox
import concurrent.futures

#use your url here
url='http://192.168.10.162/cam-hi.jpg'
im=None
 
def run1():
    cv2.namedWindow("live transmission", cv2.WINDOW_AUTOSIZE)
    while True:
        img_resp=urllib.request.urlopen(url)
        imgnp=np.array(bytearray(img_resp.read()),dtype=np.uint8)
        im = cv2.imdecode(imgnp,-1)
 
        cv2.imshow('live transmission',im)
        key=cv2.waitKey(5)
        if key==ord('q'):
            break
            
    cv2.destroyAllWindows()
        
 
if __name__ == '__main__':
    print("started")
    with concurrent.futures.ProcessPoolExecutor() as executer:
            f1= executer.submit(run1)
```


Execute this code in any programming app like VisualCode or by typing on the prompt:
```
python -m [code_name]
```
(move to the directory where the code is located by using "cd [directory_name]")

If it worked, a new window should pop up and show the camera video. From here you can use openCV however you want and modify this easy code with anything you are interested in doing!

Here is an example using Real-Time Object Detection with YOLO:

-------------------------------------

# Real-time Object Detection with YOLO

We have already installed openCV but we only have one thing left to install to work with YOLO: ultralytics. This library makes working with YOLO easy and hassle-free.
```
pip install ultralytics
```

YOLO model is loaded using this library. It specifies the location of the YOLO weights file in the yolo-Weights/yolov8n.pt. For this code, we need to instantiate a classNames variable containing a list of object classes which the YOLO model is trained to detect.

Here is the full code: 

```python
import cv2
import urllib.request
import numpy as np
import math
from ultralytics import YOLO
import concurrent.futures

# Define cam URL
url = 'http://192.168.30.183/cam-hi.jpg'

# Model YOLO
model = YOLO("yolo-Weights/yolov8n.pt")

# Classes
classNames = ["person", "bicycle", "car", "motorbike", "aeroplane", "bus", "train", "truck", "boat",
              "traffic light", "fire hydrant", "stop sign", "parking meter", "bench", "bird", "cat",
              "dog", "horse", "sheep", "cow", "elephant", "bear", "zebra", "giraffe", "backpack", "umbrella",
              "handbag", "tie", "suitcase", "frisbee", "skis", "snowboard", "sports ball", "kite", "baseball bat",
              "baseball glove", "skateboard", "surfboard", "tennis racket", "bottle", "wine glass", "cup",
              "fork", "knife", "spoon", "bowl", "banana", "apple", "sandwich", "orange", "broccoli",
              "carrot", "hot dog", "pizza", "donut", "cake", "chair", "sofa", "pottedplant", "bed",
              "diningtable", "toilet", "tvmonitor", "laptop", "mouse", "remote", "keyboard", "cell phone",
              "microwave", "oven", "toaster", "sink", "refrigerator", "book", "clock", "vase", "scissors",
              "teddy bear", "hair drier", "toothbrush"
              ]

def run1():
    cv2.namedWindow("live transmission", cv2.WINDOW_AUTOSIZE)
    while True:
        # Capture URL image
        img_resp = urllib.request.urlopen(url)
        imgnp = np.array(bytearray(img_resp.read()), dtype=np.uint8)
        img = cv2.imdecode(imgnp, -1)

        # Process the image with YOLO
        results = model(img, stream=True)
        
        # Draw boxes and labels
        for r in results:
            boxes = r.boxes

            for box in boxes:
                # Box coordinates
                x1, y1, x2, y2 = box.xyxy[0]
                x1, y1, x2, y2 = int(x1), int(y1), int(x2), int(y2)

                # Rectangle drawing
                cv2.rectangle(img, (x1, y1), (x2, y2), (255, 0, 255), 3)

                # Model confidence
                confidence = math.ceil((box.conf[0]*100))/100
                print("Confidence --->", confidence)

                # Class Name
                cls = int(box.cls[0])
                print("Class name -->", classNames[cls])

                # Object Details
                org = [x1, y1]
                font = cv2.FONT_HERSHEY_SIMPLEX
                fontScale = 1
                color = (255, 0, 0)
                thickness = 2

                cv2.putText(img, classNames[cls], org, font, fontScale, color, thickness)

        # Show image
        cv2.imshow('live transmission', img)
        key = cv2.waitKey(5)
        if key == ord('q'):
            break

    cv2.destroyAllWindows()

if __name__ == '__main__':
    print("started")
    with concurrent.futures.ProcessPoolExecutor() as executor:
        executor.submit(run1)

```

![image](https://github.com/user-attachments/assets/eafdf21f-7db8-43a6-97d9-47d47dd6e3a4)

