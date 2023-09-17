# t-deck-ulisp
Attempt at getting ulisp running on the [Lilygo T-Deck](https://github.com/Xinyuan-LilyGO/T-Deck) 

# status 
Modified pserial and gserial functions such that the terminal is mirrored on the t-deck display and the t-deck keyboard types to the terminal. No scrolling yet and backspacing doesnt work on newlines, but is otherwise vaguely usable.


# notes
The [T-Deck repo](https://github.com/Xinyuan-LilyGO/T-Deck)  contains instructions for how to upload code with the arduino IDE  

I used the [Arduino gfx](https://github.com/moononournation/Arduino_GFX) library instead of the adafruit one because the T-Deck repo examples had it working.  

The second I2C port (Wire1) is routed to pins SDA -> 18 and SCL -> 8 and is dedicated to the keyboard
