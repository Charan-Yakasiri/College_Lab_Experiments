# INTERFACING LED AND PWM, WITH LPC1768 ARM PROCESSOR.
## AIM:
To write an embedded c program to interface LED and PWM with ARM processor LPC1768

## COMPONENTS REQUIRED:
### HARDWARE:
* ARM LPC1768 LED

### SOFTWARE:
* KEIL MICRO VISION 4.0 IDE

## PROCEDURE:
* Open the Keil software and select the New uvision project from Project Menu as shown below. ⮚ Browse to your project folder and provide the project name and click on save.

* Once the project is saved a new pop up “Select Device for Target” opens, Select the controller (NXP: LPC1768) from NXP (founded by philips) and click on OK. ⮚ Select the controller (NXP: LPC1768) and click on OK.

* As LPC1768 needs the startup code, click on Yes option to include the LPC17xx Startup file.

* Create a new file by file → new to write the program.

* Type the code.

* After typing the code save the file as main.c eg. (abc.c).

* Right click target and Add the suitable files to source group1 and header for the project.

* Add the main.c along with system_LPC17xx.c.

* Build the project and fix the compiler errors/warnings if any.

* Code is compiled with no errors. The .bin file is still not generated.

* Right Click on Target Options to select the option for generating .bin file.

* Set IROM1 start address as 0x2000. Bootloader will be stored from 0x0000-0x2000 so application should start from 0x2000 ⮚ Write the command to generate the .bin file from .axf file Command: fromelf --bin projectname.axf --output filename.bin ⮚ in c/c++ → include paths → desktop (00-libfiles). ⮚ .Bin file is generated after a rebuild. ⮚ Check the project folder for the generated .Bin file. ADD FILES:

## ADD FILES:
* Target1:
* Source group1:
 Startuplpc17xx.s, delay.c , gpio.c , pwm.c , sysytemlpc17xx.c, main.c
* Header:
  delay.h, gpio.h, pwm.h, stdulils.h

## PIN DIAGRAM :
<img width="619" height="369" alt="512600444-3a047c5b-aed8-4cbe-82e4-ed82c0891d09" src="https://github.com/user-attachments/assets/3efc3279-3079-42b8-9232-b28c6bbe3c43" />


## CIRCUIT DIAGRAM:
<img width="1071" height="542" alt="512595450-344add23-41a1-402f-b223-b2547c8ccceb" src="https://github.com/user-attachments/assets/e7243152-d7c8-4a5c-83f7-d835f27a675f" />


## PROGRAM:
~~~
#include <lpc17xx.h>
#include "pwm.h"
#include "delay.h"
#define CYCLE_TIME 100
/* start the main program */
int main()
{
int dutyCycle;
SystemInit(); /* Clock and PLL configuration */
PWM_Init(CYCLE_TIME); /* Initialize the PWM module and the Cycle time(Ton+Toff) is
set to 255(similar to arduino)*/
PWM_Start(PWM_3); /* Enable PWM output on PWM_1-PWM_4 (P2_0 - P2_3) */
while(1)
{
for(dutyCycle=0;dutyCycle<CYCLE_TIME;dutyCycle++) /* Increase the Brightness of the
Leds */
{
PWM_SetDutyCycle(PWM_3,dutyCycle); //P2_2
DELAY_ms(10);
}
17
for(dutyCycle=CYCLE_TIME;dutyCycle>0;dutyCycle--) /* Decrease the Brightness of the
Leds */
{
PWM_SetDutyCycle(PWM_3,dutyCycle); //P2_2
DELAY_ms(10);
}
}
}
~~~
## Output:
<img width="756" height="519" alt="512595712-3b4f55e2-8c24-4aef-a24d-0a500115e6d7" src="https://github.com/user-attachments/assets/dae24c8c-4e69-4041-baf6-f037aa4e10ae" />



## Result :
Thus,an embedded C program is written in order to interface PWM with LPC1768.
