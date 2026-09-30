# **🎵 Raspberry Pi Pico 2 W Smart Mini MP3 Player & Weather Station**

This project is an advanced embedded audio terminal built on the Raspberry Pi Pico 2 W microcontroller. It features high-quality MP3 playback from an SD card, automatic NTP time synchronization over Wi-Fi, real-time weather fetching via the OpenWeatherMap API, and a smart screensaver mode.

📺 Watch the Full Project Video on YouTube: https://youtu.be/KwW4RNYulAw

## **🛠️ Bill of Materials (BOM)**

- **Microcontroller:** Raspberry Pi Pico 2 W (or Pico W).
- **Display & SD:** ILI9341 SPI TFT Display (320x240 pixels) + Built-in MicroSD Card Slot.
- **Audio Amplifier:** MAX98357A I2S Amplifier Module.
- **Speaker:** 3W 4-ohm / 8-ohm mini speaker.
- **Input Devices:** 3x Momentary Push Buttons and QRE1113 Optical Sensor.

## **📌 Hardware and Pin Connections**

### **🖥️ ILI9341 + Built-in MicroSD**

| **Module Pin** | **Pico 2 W** | **Physical Pin** |
| -------------- | ------------ | ---------------- |
| **VCC**        | 3.3V         | Pin 36           |
| ---            | ---          | ---              |
| **GND**        | GND          | Pin 38           |
| ---            | ---          | ---              |
| **CS**         | GPIO17       | Pin 22           |
| ---            | ---          | ---              |
| **RESET**      | GPIO15       | Pin 20           |
| ---            | ---          | ---              |
| **DC / RS**    | GPIO14       | Pin 19           |
| ---            | ---          | ---              |
| **SDI / MOSI** | GPIO19       | Pin 25           |
| ---            | ---          | ---              |
| **SCK / CLK**  | GPIO18       | Pin 24           |
| ---            | ---          | ---              |
| **LED**        | 3.3V         | Pin 36           |
| ---            | ---          | ---              |
| **SDO / MISO** | Unconnected  | —                |
| ---            | ---          | ---              |
| **SD_CS**      | GPIO22       | Pin 29           |
| ---            | ---          | ---              |
| **SD_MOSI**    | GPIO19       | Pin 25           |
| ---            | ---          | ---              |
| **SD_SCK**     | GPIO18       | Pin 24           |
| ---            | ---          | ---              |
| **SD_MISO**    | GPIO16       | Pin 21           |
| ---            | ---          | ---              |

###

### **🔊 MAX98357A Audio Amplifier**

| **Module Pin** | **Pico 2 W** | **Physical Pin** |
| -------------- | ------------ | ---------------- |
| **VIN**        | VBUS 5V      | Pin 40           |
| ---            | ---          | ---              |
| **GND**        | GND          | Pin 38           |
| ---            | ---          | ---              |
| **BCLK**       | GPIO0        | Pin 1            |
| ---            | ---          | ---              |
| **LRC / WS**   | GPIO1        | Pin 2            |
| ---            | ---          | ---              |
| **DIN**        | GPIO2        | Pin 4            |
| ---            | ---          | ---              |
| **GAIN**       | Unconnected  | —                |
| ---            | ---          | ---              |
| **SD_MODE**    | Unconnected  | —                |
| ---            | ---          | ---              |
| **OUT+**       | Speaker +    | —                |
| ---            | ---          | ---              |
| **OUT−**       | Speaker −    | —                |
| ---            | ---          | ---              |

###

### **🎛️ Control Buttons (INPUT_PULLUP)**

| **Button**       | **Pico GPIO** | **Physical Pin** | **Other Terminal** |
| ---------------- | ------------- | ---------------- | ------------------ |
| **Previous**     | GPIO6         | Pin 9            | GND (Pin 8)        |
| ---              | ---           | ---              | ---                |
| **Play / Pause** | GPIO7         | Pin 10           | GND (Pin 8)        |
| ---              | ---           | ---              | ---                |
| **Next**         | GPIO8         | Pin 11           | GND (Pin 8)        |
| ---              | ---           | ---              | ---                |

###

### **🔌 Power and Common Rail Connections**

- **3.3V Rails:** Pin 36 \$\\rightarrow\$ ILI9341 VCC, ILI9341 LED, QRE1113 VCC
- **GND Rails:** Pin 38 \$\\rightarrow\$ ILI9341 GND, MAX98357A GND; Pin 8 \$\\rightarrow\$ Buttons GND; Pin 28 \$\\rightarrow\$ QRE1113 GND
- **5V Power:** Pin 40 (VBUS 5V) \$\\rightarrow\$ MAX98357A VIN

##

## **📚 Required Libraries**

To be installed via the Arduino IDE Library Manager:

- **ESP8266Audio** (Earle F. Philhower) — For I2S audio output and MP3 decoding from the SD card.
- **Adafruit ILI9341** — TFT display driver.
- **Adafruit GFX Library** — Core graphics library.

_(Note: WiFi, HTTPClient, and SD libraries are included natively with Earle F. Philhower's Raspberry Pi Pico Arduino core.)_

## **⚙️ Software Architecture and Key Features**

- **Non-Blocking Structure:** Uses millis()-based timers to handle Wi-Fi and API operations in the background without interrupting the audio stream.
- **Dynamic SD Scanning:** Automatically scans all .mp3 files in the root directory of the SD card and adds them to the playlist.
- **Smart Button Management:** Short presses handle track changes, while long presses (>500ms) allow for precise volume adjustment.
- **Screensaver Mode:** Switches to a black screensaver displaying the time, date, weather, and currently playing track after 30 seconds of inactivity.
