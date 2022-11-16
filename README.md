# LED WiFi Controller
A DIY WiFi controller for standard RBG LED Strips.


## Concept
I had RGB LED strips in my room for a while, but I never really used them because they were quite inconvenient to use. The IR remote that came with the LEDs was not the best. So, I decided I wanted to make a DIY WiFi controller for my LEDS. I wanted it to have the following features:

- WiFi control, for ease of use
- Any RGB colour
- Some animation (E.g. colour gradient)
- Music reactive (but not just depending on volume)

## The Build
BOM (Bill of Materials:

Part         | Qty | Cost(each)
-------------|-----|-----------
ESP32        |  1  |  $10.30
Perfboard    |  1  |  $0.47
Mic sensor   |  1  |  $0.71
N-MOSFET     |  3  |  $0.50
Slide switch |  1  |  $0.50


### First Prototype
My first prototype for this project was a bit messy, but it worked. However, I wasn't too satisfied with it, so I ended up creating my first custom PCB with this project(more on that later).

The RHB LED strips I had were 5V rated, with a 2A current consumption. They ran on USB power. I couldn't be bothered to find and buy a MOSFET online, so I used the SMD mosfet on the old LED controller (the one with the IR). I managed to pt it on the perboard, and wired the gates of each channel (R, Gnd B)

I used the perfboard to wire the gates of the MOSFETs to GPIO 12, 14, and 27 of the ESP32, which are all ADC pins (PWM).
