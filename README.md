# Reglo-CPF
Arduino controller for the Reglo-CPF digital pump.

## Installation

Download the library by using the `Download Zip` button to the right and 
decompress the zip.  Rename the decompressed folder to `reglocpf` and copy it
into your `Arduino/libraries` folder.

## Usage

To use the controller, create an instance of the `RegloCPF` class using a
`Stream`-like object as the first parameter (typically `Serial`) and the
address of the pump as the second parameter (typically 1):

```arduino
#include <RegloCPF.h>

// Create a RegloCPF controller using the default address.
RegloCPF pump(&Serial, 1);
```

Note that **the library does not initialise the serial port for you**, you
must do this as part of your setup routine.  The Reglo-CPF uses the same
default settings as the Arduino (9600-baud, 8-bit, 1 stop bit, no parity).

Now, you can use the methods of the pump object to control the Reglo-CPF
digital pump.  For example, to start and then stop the pump:

```arduino
// Attempt to start the pump, if an error occurs display the light.
if (pump.start() != REGLO_OK) {
    digitalWrite(PIN_LED, HIGH);
} else {

    // Wait for a second.
    delay(1000);
    
    // Attempt to stop the pump, again displying the light if an error
    // occurs.
    if (pump.stop() != REGLO_OK) {
        digitalWrite(PIN_LED, HIGH);
    }

}
```

All control methods return a value indicating whether the command was
successful, and if not, where possible why not.  Documentation for these
return values can be found in [RegloCPF.h](RegloCPF.h).

[Further examples](examples/) are included with the library.

