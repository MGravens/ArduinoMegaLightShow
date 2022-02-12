# ArduinoMegaLightShow
There are a few #define lines on top to set the serial speed, the number of channels to use, and whether the relays activate with a high or low signal:
-Set the number of channels that you will use with the line #define CHANNEL_COUNT 16

-Set the mode line to "#define MODE INVERTED" or "#define MODE NOT_INVERTED" as needed. If your channels are doing the opposite than expected, change it to the other mode.

-Set the com port speed (currently to 57600) #define VIXEN_COM_SPEED 57600

-Set the timeout (in milliseconds) for Random mode with #define TIME_OUT 1000

It only uses 1 library for the watchdog timer, included in the arduino IDE, so just copy the code to a new sketch, change the channels, speed, and relay mode settings, and upload to your Arduino. 

NOTE: If you use an Arduino Uno, remove all the #define lines for channels after 18, and remove those channels from the line with "int channels[] = {CH01..." as all those pins are only valid in the Arduino Mega and would give a compilation error in an Arduino Uno.

It works in the following way:

-Vixen needs to be setup to use a header of: ~!
-Sets all the channels to off in startup.
-Wait for up to 2 seconds (can be changed for longer) and if there is no valid input, it goes into random mode, blinking some lights on and off every second.
-If it detects valid input (with ~! header), it writes to the relays, as long as Vixen is working.
-If Vixen goes off for more than 2 seconds, back to random mode.

