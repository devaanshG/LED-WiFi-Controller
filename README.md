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

The RGB LED strips I had were 5V rated, with a 2A current consumption. They ran on USB power. I couldn't be bothered to find and buy a MOSFET online, so I used the SMD mosfet on the old LED controller (the one with the IR). I managed to put it on the perfboard, and wired the gates of each channel (R, G and B).

I used the perfboard to wire the gates of the MOSFETs to GPIO 12, 14, and 27 of the ESP32, which are all ADC pins (PWM). I'd initially made the mistake of using ADC2 pins, which are used by the WiFi drivers when they're activated (which was true in my case). I also added a slide switch for on an off and a mic, and that was basically it for the electronics.

This is it here:


### V2 with Custom PCB
The second version is my current version, and I created a custom PCB for this using EasyEDA (and then ordered it from JLCPCB). I foudn their services easy to use and relatively cheap. This was my first time making a PCB, so I'm quite happy with the product:


The PCBs are very high quality, and it amazed me especially looking at the price of just $2.

I soldered the components liek before. I had to make a little breakout board for the SMD MOSFETS, because on the PCB I designed it for normal MOSFETS.

Here is what it looks like:


This was great but quite thick due to the ESP32 being on female headers, which I added to make sure everything worked but I'll remove those in the final product for a lower profile. I'll also make the PCB a bit longer, so that the mic can fit on the same side as all the other electronics, to further reduce thickness.

### The Code
The code started off simple - just a simple web server with an input for R, G, and B. But I quickly learnt how to use the AsyncWebServer library, and designed - what I think is - a nice looking UI. I gave it a silicon type of effect and kept it simple. Here is what it looks like:

I realised that for the animation I will need a second core, because it should be running asynchronously, so I also learnt how to use that. I had a fade animation at this point.

I then was working on the music reactive mode, and begun with just using the noise level, but this wasn't looking like it was in synch. I then came across FFTs. This is basically - from what I understand - splitting a sound wave into it's multiple different frequencies. Essentially, a sound is a random-looking wave that is made up of different sine waves for example. So it just splits that into different frequencies. I wanted the LEDs to sunch to the bass/percussion, so, I used the lower frequency bins.
