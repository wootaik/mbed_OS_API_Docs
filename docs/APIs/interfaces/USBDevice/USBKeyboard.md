# USBKeyboard


The USBKeyboard interface is used to emulate a keyboard over the USB port. You can type strings and send keycodes, keys with modifiers (like CTRL + S), function keys and media control keys.

The USB connector should be attached to :

* **p31 (D+), p32 (D-) and GND** for the **LPC1768 and the LPC11U24**.
* The on-board USB connector of the **FRDM-KL25Z**.

## Video tutorial 

<span class="images">[![Video tutorial](http://img.youtube.com/vi/NKSlkUcoOjY/0.jpg)](http://www.youtube.com/watch?v=NKSlkUcoOjY)</span>

## Hello World

[![View code](https://www.mbed.com/embed/?url=https://developer.mbed.org/users/samux/code/USBKeyboard_HelloWorld/)](https://developer.mbed.org/users/samux/code/USBKeyboard_HelloWorld/file/tip/main.cpp) 

## API

[![View code](https://www.mbed.com/embed/?type=library)](https://docs.mbed.com/docs/mbed-os-api/en/mbed-os-5.1.0/api/classUSBKeyboard.html)  

## Examples

Control sound and your playlist with switches:

```
#include "mbed.h"
#include "USBKeyboard.h"

USBKeyboard keyboard;

//Bus of buttons
BusInOut buttons(p21, p22, p23, p24, p25, p26, p29);

int main(void) {
    uint8_t p_bus = 0;

    while (1) {
        //if the bus of buttons has changed, send a report
        if (buttons.read() != p_bus) {
            p_bus = buttons.read();
            if(p_bus & 0x01)
               keyboard.mediaControl(KEY_MUTE);
            if(p_bus & 0x02)
               keyboard.mediaControl(KEY_VOLUME_DOWN);
            if(p_bus & 0x04)
               keyboard.mediaControl(KEY_VOLUME_UP);
            if(p_bus & 0x08)
               keyboard.mediaControl(KEY_NEXT_TRACK);
            if(p_bus & 0x10)
               keyboard.mediaControl(KEY_PLAY_PAUSE);
            if(p_bus & 0x20)
               keyboard.mediaControl(KEY_PREVIOUS_TRACK);
            if(p_bus & 0x40)
               keyboard.printf("Hello World\r\n");
        }
        wait(0.01);
    }
}
```
