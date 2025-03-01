Smart Health Monitoring System using Arduino 🚑💡
📌 Project Overview
This Smart Health Monitoring System is an IoT-based embedded project that measures heart rate, SpO₂ (Oxygen Saturation), and body temperature in real time using MAX30100 and MLX90614 sensors. The data is displayed on an OLED screen and can be extended for cloud monitoring.

🛠️ Technologies Used
Arduino Uno/Nano (Microcontroller)
C/C++ (Embedded Programming)
MAX30100 (Pulse Oximeter for Heart Rate & SpO₂)
MLX90614 (Infrared Temperature Sensor)
OLED Display (SSD1306)
GitHub (Version Control)


⚙️ Features
✔️ Measures Heart Rate & SpO₂ using MAX30100
✔️ Measures Body Temperature using MLX90614
✔️ Displays real-time data on OLED Display
✔️ Alerts for abnormal health conditions
✔️ (Optional) Sends data to the cloud via WiFi (ESP8266)

🛠️ Hardware Requirements
1️⃣ Arduino Uno/Nano
2️⃣ MAX30100 (Pulse Oximeter)
3️⃣ MLX90614 (Temperature Sensor)
4️⃣ OLED Display (SSD1306)
5️⃣ Jumper Wires & Breadboard
6️⃣ Battery (9V) or USB Power

🔧 Circuit Diagram
📌 Upload an image of the circuit connection or Fritzing diagram here.

🚀 Installation & Setup
Step 1: Clone the Repository
sh
Copy
Edit
git clone https://github.com/yourusername/Smart-Health-Monitor.git
cd Smart-Health-Monitor
Step 2: Install Required Libraries
Open Arduino IDE and install the following libraries via Library Manager:
✅ Adafruit_GFX.h
✅ Adafruit_SSD1306.h
✅ Adafruit_MLX90614.h
✅ Wire.h
✅ MAX30100_PulseOximeter.h

📜 Code (Main Sketch)
Here is a basic Arduino sketch for the project:

cpp
Copy
Edit
#include <Wire.h>
#include <Adafruit_SSD1306.h>
#include <Adafruit_MLX90614.h>
#include "MAX30100_PulseOximeter.h"

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

Adafruit_MLX90614 mlx = Adafruit_MLX90614();
PulseOximeter pox;

void setup() {
    Serial.begin(115200);
    display.begin(SSD1306_SWITCHCAPVCC, 0x3C);
    mlx.begin();
    pox.begin();
}

void loop() {
    float temperature = mlx.readObjectTempC();
    pox.update();
    float heartRate = pox.getHeartRate();
    float spo2 = pox.getSpO2();

    display.clearDisplay();
    display.setCursor(0, 0);
    display.print("Temp: "); display.print(temperature); display.print("C");
    display.setCursor(0, 20);
    display.print("HR: "); display.print(heartRate); display.print(" BPM");
    display.setCursor(0, 40);
    display.print("SpO2: "); display.print(spo2); display.print(" %");
    display.display();

    delay(2000);
}
👉 For the full code, check the health_monitor.ino file in this repository.

📌 Future Enhancements
✅ IoT Integration – Send data to Blynk/ThingSpeak for remote monitoring
✅ SMS Alerts – Notify users if health readings are abnormal
✅ Battery-Powered Version – Make it portable
✅ Android App – Display real-time health data on mobile

🤝 Contributing
Want to improve this project? Feel free to fork the repo and submit a Pull Request! 🚀
