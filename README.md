NTP Projection Clock
====================

A NodeMCU based clock that wirelessly connects to your network and runs
an NTP client to retrieve the time and project it onto a wall or ceiling.

![](/images/IMG_20201216_215617_small.jpg?raw=true "ntp projection clock")

Construction
------------

Print the [stl files](tree/master/models/printable) that comprise the chassis.

Wire the NodeMCU and Adafruit LED Backback like:

![](/images/NodeMCU-LCD-Screen-i2c-16x2-Display.jpg?raw=true "wiring diagram")

Screw these boards into the chassis and then plug the NodeMCU into your computer via a USB cable for programming.

The lens I used was the 10x lens piece found ing the <a target="_blank" href="https://www.amazon.com/iMagniphy-Illuminated-Magnifying-Magnifier-Degeneration/dp/B018I1S2Q6/?&_encoding=UTF8&tag=chrisspen05-20&linkCode=ur2&linkId=9c56961c9553f8b3b0992ff2598e1a36&camp=1789&creative=9325">iMagniphy Glass</a>. Note, it's actually made of two lens sandwiched in a housing.

Programming
-----------

Install the Arduino IDE 1.8 or later and NodeMCU Arduino support:

    https://www.arduino.cc/

Launch the IDE with:

    cd /usr/share/arduino; arduino

Install [NodeMCU Arduino Support](https://github.com/esp8266/Arduino#installing-with-boards-manager):

* Start Arduino and open Preferences window.
* Enter http://arduino.esp8266.com/stable/package_esp8266com_index.json into Additional Board Manager URLs field. You can add multiple URLs, separating them with commas.
* Open Boards Manager from Tools->Board menu and install or update the esp8266 platform.
* Under Tools->Boards, select "NodeMCU 1.0 (ESP-12E Module)".

Load the `firmware.ino` sketch, select NodeMCU board and board, verify and upload.

To set the Wifi password dynamically, shell into the `scripts` directory and run:

    cd src/scripts
    ./init_virtualenv.sh
    . .env/bin/activate
    ./clock_controller.py login ssid ssidpwd

Otherwise, create the file src/firmware/credentials.h and enter your credentials there, recompile and upload your firmware.

Debugging
---------

To inspect output, select "Serial Monitor" under Tools in Arduino IDE. Select 115200 baudrate.

Also, via the clock_controller.py script with:

    ./clock_controller.py monitor

To get detailed time output:

    ./clock_controller.py time
