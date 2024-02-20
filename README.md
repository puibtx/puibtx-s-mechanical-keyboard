This is a mechanical keyboard using an Arduino Nano ( or any of the knock-offs that running on the ATmega328P)
**********************************************************************************************************************************

1) Determine the layout of the keyboard using http://www.keyboard-layout-editor.com/
After designing the layout to your liking, make sure to save the layout and save the information under the raw data tab. 
(make sure you save your keyboard layout as permalinks to come back from this)
I went with a modified version of the 68-key layout with an extra knob. On the top right corner

![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/ad36e540-a87c-4a69-8465-95ce6c71ea98)

**********************************************************************************************************************************

2) Remember the Raw data I told you to save; now go to http://builder.swillkb.com/
and put in your raw data to generate a plate; you can mess around with which switch type you want to include, but MX t:3 will work in most cases.
you will get something like this 

![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/14acd4b4-5b78-4093-834c-514670d231df)

You can find ways to download the CAD drawing in SVG, DXF, and EPS, just in case you download all three.
**********************************************************************************************************************************

3) Now, we need to generate a keyboard matrix. To learn what a matrix is, you can read (https://github.com/EanNewton/Awesome-Keebs/blob/main/tutorials/How%20to%20make%20a%20keyboard%20-%20the%20matrix.md)

once again, grab the layout you have designed and put it in https://kbfirmware.com/. 
Under the wiring tab, we can see how many rows and columns you need to complete the matrix, but remember the number of pins on an Arduino nano is limited. Thus, you need to reduce the number of columns
and rows required for the keyboard. 

For example the default wiring for my layout is: 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/2164a85e-6f96-47a5-84ab-78b9459e5238)
after rearranging 
![image](https://github.com/puibtx/puibtx-s-mechanical-keyboard/assets/99428766/42ceb12b-e478-49ec-97ec-fbeafbc0f64a)
This might look confusing, but the 

