# INTERFACING-OF-ADC-WITH-ARM-PROCESSOR

## AIM: 
   To interface and toggle the led with ARM LPC 1768 microprocessor           
           
## COMPONENTS REQUIRED:

### Hardware:
* ARM LPC1343 / LPC1768
* LCD module
## Software:
* Coocox IDE

## PROCEDURE:
- Step 1: Go to start All programs  COIDE.
- Step 2: Give a suitable file name for your project and give the destination folder and then next. Step 3: Go to chip NXP LPC 13XX  LPC1343  Next.
- Step 4: Select the required library file (SYSCON and GPIO) from the repository.
- Step 5: A new project will be created.
- Step 6: Double click on main.c and type the program.
 - Step 7: Add the required library source file to the project (Right click on include Add file to group and
add the source file).
- Step 8: Build the program using build option.
- Step 9: Flash the program by clicking on download code to flash. Step 10: Interface the required component and note down the output. ADD FILES:
#### Repository:
CMSIS core, CMSIS boot, common header files, SYSCON, GPIO.

## Source files:
simple example.c, Uart Receiver interrupt.c, lcd.c, lcd.h
 
## DIAGRAM:

<img width="923" height="443" alt="image" src="https://github.com/user-attachments/assets/c0045e52-162c-44b8-9d86-a119cc8b754d" />

 
 
# PROGRAM:
~~~
#include"lcd.h" 
void ADCExp(); 
int main(void)
{
ReceiverInterrupt(); 
init_lcd();
lcd_putstring(LINE1, "RAANA ADC DEMO "); 
ADCExp();
while(1)
{
}
}
~~~
## Output
<img width="558" height="375" alt="514693376-43724009-8749-424c-934a-9600e558e026" src="https://github.com/user-attachments/assets/648f6a34-301a-4a28-a18b-d365d671e85a" />

 
## RESULTS
Thus, an embedded c program to interface ADC with ARM processor was executed and output was verified successfully
