# BlueHam-Mini by W1BTR
Adds Bluetooth CAT control and programming to any ham radio that supports wired programming
![image](https://github.com/ITCMD/BlueHam-Mini/assets/32961763/200b5f63-1bd8-4b42-a35f-77c8dff1ac7f)
## WARNING: This has NOT been tested as of yet and is theoretical code and application. We need testers! Submit your issues in the issues tab here on Github. I made this with zero arduino / ESP32 experience and I dont have any ESP32 modules to test this on yet.

## How it works
These scripts use an ESP32 module. The scripts create a Bluetooth device called “Blueham Mini” using the BluetoothSerial library. It sets up a serial connection between the ESP32 and a device connected via Bluetooth, and includes code to handle both full-duplex and half-duplex communication.

In the loop function, the script checks if there is data available on either the hardware serial or Bluetooth serial connections and transfers data between them if necessary. This allows for full-duplex communication between the ESP32 and the connected device.

The script also includes code to handle half-duplex communication without requiring the serial device to signal the direction of data flow. It uses a timer to alternate between sending and receiving data. When the sendData variable is true, the script sends data from the ESP32 to the connected device, and when sendData is false, it receives data from the connected device.

### OLED VERSION
There is also a version of the script that supports an integrated OLED screen. It will display a title and the Bluetooth SSID.

# Hardware
Requires:

- An ESP32 module that supports bluetooth For example: https://www.amazon.com/ESP-WROOM-32-Development-Microcontroller-Integrated-Compatible/dp/B08D5ZD528/
- 2A+ DC to DC buck converter that can supply 5-7V to the ESP32 from ~13.8v coming from the radio for example: https://www.amazon.com/gp/product/B07PDGG84B/ **or a power supply OR a 5v USB cable to input to the ESP32's USB port**.

# Setup
## Flash Firmware
1. If not already installed, install the **Arduino IDE** https://www.arduino.cc/
2. Add the ESP32 by going to `File` -> `Preferences` -> `Additional Boards url` -> and add `https://dl.espressif.com/dl/package_esp32_index.json` (if you already have any modules, add a comma before pasting in this url) and click OK.
3. Go to `Tools` -> `Board: "Currently Selected Board"` -> `Boards Manager`, search `esp32`, and select `Install`
4. Now go to `Tools` -> `Board: "Currently Selected Board"` -> `ESP32 Arduino` -> `ESP32 Dev Module`
5. Choose the proper code for your board (whether it has an OLED or not) and paste it in
6. Open Device Manager and list the COM ports. Note what's there.
7. Plug in your ESP32 card. Refresh Device manager and see what new COM port there is.
8. Go to `Tools` -> `COM[somenumber]` and set it to the correct com port, such as `COM5`.
9. Click the arrow in the top left next to the check mark to upload the code to the board. It should compile and upload it, and right off the bat it should broadcast it's bluetooth signal.

*If it fails to program, check if the specific esp32 board you got requires you to press a key before it lets you flash it.*
## Wiring
1. wire DC power to the ESP32 module with 5-7 v on the pins, or exactly 5v on the USB port
2. Wire GND to the Data GND port on the radio
3. Wire RX and TX Data to their corresponding pins on the radio (on some radios you may need to reverse these). If your radio only has a GND and a Data pins (RX and TX are one pin) it likely works in half duplex mode. For this, wire the wire to either the RX or TX port. It does not matter which one.
![image](https://github.com/ITCMD/BlueHam-Mini/assets/32961763/86bc9978-49e4-42db-b7a5-4c7d8c918981)

Now, connect over Bluetooth and open your CAT control app of choice. Pocket TX RX Lite is a favorite of mine for the FT-857D.



