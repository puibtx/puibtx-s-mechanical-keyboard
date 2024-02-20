This is a mechanical keyboard using an Arduino MICRO ( or any of the knock-offs that running on the ATmega32U4)
**********************************************************************************************************************************

1)
Determine the layout of the keyboard using http://www.keyboard-layout-editor.com/
After designing the layout to your liking, make sure to save the layout and save the information under the raw data tab. 
(make sure you save your keyboard layout as permalinks to come back from this)
I went with a modified version of the 68-key layout with an extra knob. On the top right corner

![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/ad36e540-a87c-4a69-8465-95ce6c71ea98)

**********************************************************************************************************************************

2)
Remember the Raw data I told you to save; now go to http://builder.swillkb.com/
and put in your raw data to generate a plate; you can mess around with which switch type you want to include, but MX t:3 will work in most cases.
you will get something like this 

![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/14acd4b4-5b78-4093-834c-514670d231df)

You can find ways to download the CAD drawing in SVG, DXF, and EPS, just in case you download all three.
**********************************************************************************************************************************

3)
Now, we need to generate a keyboard matrix. To learn what a matrix is, you can read (https://github.com/EanNewton/Awesome-Keebs/blob/main/tutorials/How%20to%20make%20a%20keyboard%20-%20the%20matrix.md)

once again, grab the layout you have designed and put it in https://kbfirmware.com/. 
Under the wiring tab, we can see how many rows and columns you need to complete the matrix, but remember the number of pins on an Arduino MICRO is limited. Thus, you need to reduce the number of columns
and rows required for the keyboard. 

For example, the default wiring for my layout is: 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/2164a85e-6f96-47a5-84ab-78b9459e5238)
after rearranging 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/42ceb12b-e478-49ec-97ec-fbeafbc0f64a)
This might look confusing, but the idea is to fit keys into the 13x5 matrix. 

I ended up with a 15x5 matrix, meaning I needed to use 20 pins on the Arduino Uno.  
keep the screenshot of your wiring diagram, and download the .hex and the zip file under the compile tab.
**Now decide which microcontroller or dev board you want to use, make sure you have enough pins for # of rows and # of columns. 

**********************************************************************************************************************************
4) 
This will be where you spend a big portion of your time, now use any of the CAD software you like
Such as Autodesk Eagle or a great free alternative: https://easyeda.com/

import the layout of your CAD drawing of the plate from step 2. 
Start creating the schematic according to the wiring diagram you created in step 3. 

**Remember, in the matrix, for each column, or if you decided the other way, each column needed a diode. Depending on your liking and ease of soldering, you may prefer an SMD device or a hole component.
**You might want to add a backlight to the Keyboard; now it is time to make a decision on what type of LED you want to use. 
**You might want to add a knob to the Keyboard; now it is time to make a decision on what type of encoder you want to use. 
**You will also need to use some capacitors for your LED if you decide to include them. Because the instant current draw required by the LED might be too much for the thin wires in the PCB, leading to 
a voltage drop, a capacitor will smooth it out.

I have decided to backlight via SK6812 RGB LEDS (https://www.aliexpress.us/item/3256804063588369.html?spm=a2g0o.order_list.order_list_main.126.457d1802xfLeyL&gatewayAdapt=glo2usa)
and adding a generic decoder on Amazon. 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/61403414-3498-40bd-a3e5-089047288142)
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/ecfb8362-1003-43b0-98e4-7ce33ccac191)

After selecting what type of switch you want to use, maybe some LED and capacitors, you would have to figure out their package size. 
I have chosen a flipped switch + sk6812 RGB + SOD-123 package size diode and 32*16 size SMD size.

You either have to create your own parts with the proper pin name and footprint. Or you can find them online with the magic of https://www.google.com/

Using the plate and the wiring diagram, start placing your part and create a schematic.

This is what mine looks like. 
![lol123123png](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/2a021cd8-4d96-4167-b182-09d8c28b4056)

With the schematic, now you would have to learn how to place parts that you created or found in the board view. 
Painstakingly connect all the parts together in the front and back. Eagle has an auto-router that is good enough for a simple project like this. 

Mine turned out like this, and I made the mistake of having some right angle connection, but this should not be a huge issue with 5v VCC. 
![3](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/f5b4d46d-6569-43d5-ad17-5d5c30f6c5e9).

**********************************************************************************************************************************
5)
To print the PCB, I recommend JLC PCB: https://jlcpcb.com/
they offer cheap or sometimes even free PCB fabrication, but here is the catch: shipping is a big part of the final price.
In my case, I had to order 5 PCBs, but shipping (US, California) was ~$25 total, which is still reasonable. \

the final PCB arrive and looks like: 
![c9851ba372f73256a2a66e2067f7871](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/9773cc75-ceb7-46e5-84b0-38e9e0d7128c)
![a2949e3136599316f9804f63e5c191d](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/026f73f1-043c-4ba6-baae-f34696a312c0).

**********************************************************************************************************************************
6)
Solder time, because I used SMD components, a hot air station is necessary; they can be found relatively cheaply for ~$50 USD.
** Make sure to have solder paste that is not expired; it will be a nightmare dealing with expired solder paste. 
It was a pain to solder more than 68 switches, SMD diodes, SMD Caps, and LEDs.

The model of the Arduino MICRO knockoff had a USB micro B port, and I wanted to convert it to USB-C; you can just adapt a standard USB 2.0 by soldering the corresponding wires to the same pins. 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/3e5bc62a-1bcd-46b9-adfd-7c4d0883dd3c)
** Since the USB C device needs to know which is the host and which is a peripheral device to provide power, we need to connect the CC1 and CC2 channels, each with a 5.1k ohm resistor for pulldown.

**********************************************************************************************************************************
7)
The complete product. 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/f0f6bba9-c70a-42f3-a61a-02ddcc58f657)
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/09babc43-a07d-41fa-9b51-0f78f7e9ba7e)

**********************************************************************************************************************************
8)
Software Part.

I recommend QMK Firmware for Atmega32U4, https://github.com/qmk/qmk_toolbox. Pick your poison depending on your OS.
Also, go and grab some example firmware from https://docs.qmk.fm/#/newbs_getting_started for reference. 


**********************************************************************************************************************************
9)
now decide what pin you want to use for your keyboard, make sure you have enough pins for # of rows and # of columns.

you can reference the available pin at https://store-usa.arduino.cc/products/arduino-micro.
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/1c800fe7-dea9-4b3e-97e6-1119d3606dc5)

These pins are what I decided on. 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/0fa31fe6-5b98-4ba7-8fec-64cd2f5abff2)

**********************************************************************************************************************************
10) 
now go under the folder of the QMK firmware that we have downloaded in step 8).
and check out any of the projects that have already been created by the community.
I went with 9key. But pick what you like, by viewing the QMK firmware GitHub page, and there are some previews of the keyboards. 

LET go over some files you need to edit. 

  1) 9key.c 
     if you want to have a rotatory encoder in your keyboard, enable it by put the following line
````
bool encoder_update_kb(uint8_t index, bool clockwise) {
    return encoder_update_user(index, clockwise);
}
````
  2) 9key.h
     place holder
  3)  to be finished . 
     
