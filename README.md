
# OCEAN (Orientation Calculation Engine AddoN)
The OCEAN system can calculate your ships current orientation for all three axis while beeing stationary. This is handy for figuring out which way you neeed to turn in order to move in a certain direction. This can also enable you to build an autopilot/autoalignment system. The system currently supports two ways of beeing setup. One where you can stop and start the execution of the calculations and display and one where it runs continiously. Where the one with start and stop capabilities will be considered the default one as it enables resetting the system.

You will need to place three receivers on your ship so that they on the same plane. They can be placed on top bottom or inbetween on your ship just make sure there is no height difference between them. See the following image for an example.
![Example with receiver numbering](https://i.imgur.com/GCQeCro.jpg)
The documentation will refer to the receivers and their corresponding ISAN module with the numbers shown above.

Please report any issues you have. If something differs between SSC and "normal" world I forgto to flip things around as the x and z axis are flipped.
## Demo
Long:
https://youtu.be/2f8PTyunn_E
Short:
https://www.youtube.com/watch?v=azsX-w3OqR8

The repository also includes a sample blueprint in the "samples" folder for quick testing.

## **Global Variables**
The system need the following global variables/device fields
### Receivers
| New Fieldname | Contains |Where to set |Default Fieldname
|--|--|--|--|
| AT | ISAN1 Receiver Target Message |Receiver in the back|TargetMessage
| a | ISAN1 Receiver Signal Strength |Receiver in the back|SignalStrength
|AU|ISAN 2 Receiver Target Message| Receiver in the front|TargetMessage
|u| ISAN 2 Receiver Signal Strength| Receiver in the front|SignalStrength
|AV|ISAN 3 Receiver Signal Strength| Receiver under ISAN 2 Receiver|TargetMessage
|v|ISAN 3 Receiver Signal Strength| Receiver under ISAN 2 Receiver|Signal Strength

### Textpanels
|New Fieldname|Contains |Where to set|Default Fieldname
|--|--|--|--|
| _| ISAN Coordinates | Textpanel of your choice|PanelValue
| _1| OCEAN Orientation | Textpanel of your choice|PanelValue

### Buttons
The buttons can also be replaced by fields in a memory chip if you dont want to place additional buttons.
|New Fieldname|Contains |Where to set|Default Fieldname
|--|--|--|--|
|arun|determines if attitude calculation runs (optional)|Button of your choice|ButtonState
|br|determines if bank calculation runs (optional)|Button of your choice|ButtonState
|r|determines if heading calculation runs(optional)|Button of your choice|ButtonState
|drun|determines if display output runs(optional)|Button of your choice|ButtonState

### Memory chips
The system needs the following fields  set in memory chips.

|New Fieldname|Contains |Where to set|
|--|--|--|
|1|x coordinate ISAN1|Memorychip
|2|y coordinate ISAN1|Memorychip
|3|z coordinate ISAN1|Memorychip
|4|x coordinate ISAN2|Memorychip
|5|y coordinate ISAN2|Memorychip
|6|z coordinate ISAN2|Memorychip
|7|x coordinate ISAN3 |Memorychip
|8|y coordinate ISAN3|Memorychip
|9|z coordinate ISAN3|Memorychip
|h|Heading Value|Memorychip
|q1|Attitude Valueinput|Memorychip
|t|bank atan input|Memorychip
|t1|Vank Value|Memorychip
|p1|"debug" variable for ISAN 2|Memorychip/Textpanel
|p2|"debug" variable for ISAN 3|Memorychip/Textpanel


## Chips
You need three chips that each run an ISAN instance.
You will also three advanced chip for attitude, heading and bank calculation.
### ISAN1
The following replacements need to be done
|Original Name|New Name  |
|--|--|
|xx  | :1 |
|yy| :2 |
|zz| :3 |

### ISAN2
The following replacements need to be done:
|Original Name|New Name  |
|--|--|
|xx  | :4 |
|yy| :5 |
|zz| :6 |
|:AT|:AU|
|:a|:u|
|:_|:p1|

### ISAN3 
The following replacements need to be done:

|Original Name|New Name  |
|--|--|
|xx  | :7 |
|yy| :8 |
|zz| :9 |
|:AT|:AV|
|:a|:v|
|:_|:p2|

If you dont want to replace them manually you can use the pre modified code: [here](https://gist.github.com/SirBitesalot/57b1ec278d72ba3b8bdd01115864248f).
Note that this code may already be outdated or may become so in the future.
For optimal setup I recommend getting the newest ISAN code and doing the above replacements yourself.

### Needed chips
|Chiptype|Used for|
|--|--|
| Advanced| Heading calculation |
| Advanced| Attitude calculation n |
| Advanced| Bank calculation |
| Basic/advanced| ISAN1 |
| Basic| ISAN2 |
| Basic| ISAN3|
|Basic |Output to textpanel|
|Memorychip|Variables|
|Memorychip|More variables|
## Setup
Download the repositiory. The code is inside the src folder. It is split into two sub folders. 
One "Default" this includes the code for the "normal" world OCEAN.
The other one "SSC" contains the code for SSC/Testflight OCEAN.
Both contain a version running continously and one that is stoppable. This guide handels the recommended stoppable setup.
 
1. Place receivers as shown in the image

 ![Example with receiver numbering](https://i.imgur.com/GCQeCro.jpg)
 
2. Name receiver device fields according to section "Receivers"

Receiver1:

![Receiver1](https://i.imgur.com/HYynezz.png)

Receiver2:

![Receiver2](https://i.imgur.com/Z7yDfAU.png)

Receiver3:

![Receiver3](https://i.imgur.com/TBAaUYF.png)

3. Install two memory chips and name the fields as shown in "Memory chips" section
4. Take three yolol chips and copy your modified ISAN code onto each one See "Chips section" and install them.
5. Take an advanced yolol chips and copy the code from "Attitude_restartable.yolol" onto it and install the chip.
6. Take an advanced yolol chips and copy the code from "bank_restartable.opt.yolol" onto it and install the chip.
7. Take an advanced yolol chips and copy the code from "heading_restartable.opt.yolol" onto it and install the chip.
8. Take a basic yolol chip and copy the code from "Display_restartable.yolol" onto it and install the chip.
The chips could for example be installed as the following image show:
![Chip example](https://i.imgur.com/6QSmTlp.png)

|Number|Chip|
|--|--|
| 1| ISAN1 |
| 2| ISAN2 |
| 3| ISAN3 |
| 4| Memorychip1|
| 5| Memorychip2|
| 6| Attitude calculation |
| 7| Heading calculation |
| 8| Bank calculation |
| 8| Display output |
9. Install 4 Buttons and change the ButtonState field names see "Buttons" section

Button1: 

![button1](https://i.imgur.com/GujxaoY.png) 

Button2: 

![button2](https://i.imgur.com/LJyMiwE.png)

Button3: 

![button3](https://i.imgur.com/yz7gRr0.png)

Button4:

![button4](https://i.imgur.com/ZU0LhUZ.png)

Sample button arrangement:

![Sample buttons](https://i.imgur.com/uSXVffZ.png)

