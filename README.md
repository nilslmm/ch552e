# ch552e
A simple PCB for the ch552e

I wanted to learn SMD soldering and PCB creation. That's why I came up with this small project.

The PCB comes with two LEDs. One Power indicator and one that can be programmed. One programmable button.
It has pads that can be bridged to enter bootloader mode.

![PCB front](img/pcb_front.png)
![PCB back](img/pcb_back.png)


# Usage
After getting the PCB manufactured and soldering all the components you can program it as you wish.

To program the ch552e using the Arduino IDE you need to add a Board Manager URL.
For this you go to File > Preferences and add ```https://raw.githubusercontent.com/DeqingSun/ch55xduino/ch55xduino/package_ch55xduino_mcs51_index.json```
After that you open the board manager and install 

# Example Code

```c
#include <USBHID.h>

const int ledPin = P1_4;  // Updated for LED on Pin P1.4

void setup() {
  pinMode(ledPin, OUTPUT);
  USBInit();  // Initialize USB HID keyboard stack
  
  // Wait 2 seconds on power-up so OS detects USB device before typing
  delay(2000);

  // Turn LED on to indicate typing sequence start
  digitalWrite(ledPin, HIGH);
  
  // Type out the passphrase string
  Keyboard_print("password123ch552");
  
  // Press Enter key to submit
  Keyboard_write(KEY_ENTER);
  
  delay(1000);  // Keep LED on for 1 second after typing
  
  // Turn LED off
  digitalWrite(ledPin, LOW);
}

void loop() {
}
```

Go to Tools and make sure you are using those settings:
Bootloader Pin: P3.6 (D+) pull-up
Clock Source: 16MHz (internal), 3.3v or 5v
Upload Method: USB
USB Settings: USER CODE w/ 148B USB (based on your use case you might want to use something else. For simple keystrokes this is the best. Do you own research for other use cases)


# BOM
2x 100nF Capacitors 0805               
2x LED 0805 (One Power LED (e.g. Green) + one Status LED (e.g. Orange))
2x 330 Ohm Resistors 0805
1x 1.5kOhm Resistor 0805
1x Tac Switch SKQGABE010
1x CH552E (about 50 cents)
| Amount | Component | Value | Size | Price | Link
|:---|:---:|:---:|:---:|:---:|---:|
| 2x | Capacitor | 100nF |  0805 | 1.35 EUR | https://de.aliexpress.com/item/1005006142309480.html 
| 1x | LED | Green |  0805 | 1.59 EUR | https://de.aliexpress.com/item/1005009128722843.htm
| 1x | LED | Orange |  0805 | 1.79 EUR | https://de.aliexpress.com/item/1005006142309480.html 
| 2x | Resistor | 330Ohm |  0805 | 2.99 EUR | https://de.aliexpress.com/item/1005011779163101.html
| 1x | Resistor | 1.5kOhm |  0805 | 2.89 EUR | https://de.aliexpress.com/item/1005011779163101.html
| 1x | Tac Switch | SKQGABE010 | / | 1.24 EUR | https://www.lcsc.com/product-detail/C115351.html
| 1x | Chip | CH552E | / | 0.57 EUR | https://www.lcsc.com/product-detail/C967938.html

Ordering the PCB on JLCPCB costs $4.20
