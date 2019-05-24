analogOneWire
=============

Bi-directional one wire bus with analog filtering capabilities.
This library cannot be used to communicate with one wire devices!
It is intedned to be used to communicate between multiple nodes running this library.

Differences compared to regular one wire bus:
- Analog filtering of the communication.
- Simple acknowledge after transmission
- Slower communication (usually AC-Mains frequency dependant)
- longer wires
- currently only point to point communication possible

Purpose
-------
This bus is intended to replace existing floor heater installation.
Usually every room is equipped with a temerature controller 
switching the corresponding valve for the heating loop.

So the existing installation allows for a single wire communication 
interface to bring intelligence to the system. The regular one wire bus would be disturbed by the AC mains capacitive coupled disturbances, so I changed the timing to be AC-Mains synchronized and added analog read to be able to filter the disturbances. Of course on the physical layer it is Necessary to inroduce proper voltage levels and offsets to make the filtering possible.

License
-------
Copyright 2019 Moritz Wagner
Licensed under the GPL License, Version 3.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.gnu.org/licenses/gpl-3.0.en.html

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Installation
------------
Click the "Download ZIP" button to download a .zip of the entire
analogOneWire library. Unpack the .zip and rename the top-level
directory to analogOneWire. Move or copy that directory to the
`libraries/` directory inside the sketch folder for your Arduino IDE.
You may need to create that `libraries/` directory if this is the
first library you install. Restart the Arduino IDE to make it
available in the Sketch > Import Library... menu.

Basic Usage
-----------
Use the Sketch > Import Library... menu item to add the analogOneWire
library to your sketch. This will add a line at the top of your
sketch that includes the library definitions:

    #include <analogOneWire.h>

Or, add that `#include` by hand, instead.

You need to create an instance of the `analogOneWire` class, usually a
global variable. 

Examples
--------



**NOTE:** C
**WARNING:** 

References
----------
* AtMega328 reference manual - http://www.atmel.com/Images/Atmel-8271-8-bit-AVR-Microcontroller-ATmega48A-48PA-88A-88PA-168A-168PA-328-328P_datasheet.pdf

API Reference
-------------
Only the public API is described here. More information about the private class members and the implementation can be found within the source files.

### `analogOneWire()`

The constructor to create a new instance of the analog one wire module. For every node you want to connect to you'll need one instance. This makes it possible to receive/send to all nodes simultaneously. Please note that evey connection is capable of exactly two communicating partners. One must be configured as "Master", and one as "Slave", whereas only the Master device can initiate the packet transfer. If the Slave wants to send it has to wait for the master to init the transfer first.

#### `void setCallback(int pin, void (*pFn)(int index, int pin, int value))`

Sets a callback function for an analog pin. The callback function will be invoked whenever a new value is read from the specified pin. Define the callback function like this:

    void myCallback(int index, int pin, int newValue) {
        ... process the value ...
    }


Release Notes
-------------
* 2019-05-24 - Initial start of the Project, work in progress everything's about to change
