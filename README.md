# Atmega4808 example using UPDI programmer

### Important links
Schematic: https://github.com/kakushinAU/Atmega4808/blob/main/UPDI_Schematic.pdf

MegaCoreX URL:  https://github.com/MCUdude/MegaCoreX

MegaCoreX board manager URL: https://mcudude.github.io/MegaCoreX/package_MCUdude_MegaCoreX_index.json

JTAG2UPDI firmware: https://github.com/ElTangas/jtag2updi


### Example code
```
#include <Wire.h>                               // include "wire" library for i2c communications
#include <Adafruit_SSD1306.h>                   // include adafruit library to drive the display
#include <Fonts/FreeSansBoldOblique24pt7b.h>    // include a nice looking font

Adafruit_SSD1306 display(128,64,&Wire,4);       // initialize i2c display 128px by 64px. Oled reset = 4
int i=0;                                        // initialize variable i

void setup() {
 display.begin(SSD1306_SWITCHCAPVCC, 0x3C);     // start talking to the i2c display at address 0x3C
 display.setFont(&FreeSansBoldOblique24pt7b);   // set font to a nice large 24pt font
 pinMode(24, OUTPUT);                           // set gpio 24 (pin24) as an output pin
}

void loop() {
 display.clearDisplay();                        // clear all text from the display at start of the loop
 display.setTextColor(SSD1306_WHITE);           // set text colour to white
 display.setCursor(20,50);                      // start the bottom left corner of text down 20px and over 50px
 display.print(i);                              // print the value of variable i to display buffer
 display.display();                             // display the buffer on the display
 i=i+1;                                         // increment the variable i by one
 delay(500);                                    // wait 500ms before moving to next step
 digitalWrite(24, LOW);                         // turn off output pin 24
 delay(500);                                    // wait 500ms
 digitalWrite(24, HIGH);                        // turn on output pin 24
}
```
