# Fridge-door-opening-alarm-circuit

## Exp 4: Design an fridge door opening alarm circuit using Eagle software
## AIM:
To design the schematic and PCB layout diagram of an fridge door opening alarm circuit using Eagle software.

## EQUIPMENT REQUIRED:
●	Hardware: Personal Computer (PC)<br>
●	Software: Eagle <br>

## PROCEDURE:
	Create a New Project:<br>   
o	Launch EAGLE and start a new project for your PCB design.<br>
o	Within the project, create a new schematic file.<br>
	Add Components:<br>
o	Utilize the built-in libraries in EAGLE or create custom libraries if needed.<br>
o	Use the 'Add' tool to place the required components onto the schematic sheet.<br>
	Make Connections:<br>
o	Connect the components using the 'Net' tool.<br>
o	Label the nets clearly to maintain clarity and organization in your design.<br>
	Check for Errors:<br>
o	Once the schematic design is complete, perform an Electrical Rule Check (ERC) to identify and correct any errors.<br>
o	Save the schematic after confirming that no errors are present.<br>
	Switch to Board Layout:<br>
o	Click on the 'Generate/Switch to Board' button to create the PCB layout from the schematic.<br>
	Arrange Components and Route Traces:<br>
o	In the board layout editor, arrange the components to optimize space and reduce signal interference.<br>
o	Use the 'Route' tool to connect the components based on the schematic design.<br>
o	Ensure proper routing by utilizing the available editing tools in EAGLE to avoid design rule violations.<br>
	Design Rule Check (DRC):<br>
o	Perform a Design Rule Check (DRC) to ensure that the routing and layout comply with design standards and that there are no issues.<br>
o	Save the board layout after resolving any errors.<br>
	Generate Gerber Files:<br>
o	Go to File > CAM Processor and configure the CAM jobs to generate Gerber files for all PCB layers, such as copper layers, silkscreen, solder mask, and drill files.<br>
o	Verify the generated files to ensure they contain all necessary information for manufacturing.<br>
	Save Manufacturing Files:<br>
o	Save the Gerber files and any other required manufacturing files to send to your PCB manufacturer for fabrication.<br>

## THEORY:
The fridge door opening alarm circuit consists of a 9V supply, an LDR light sensor, and two NE555 timer ICs configured in monostable and astable modes. The LDR is positioned such that it remains in the dark when the fridge door is closed, resulting in very high resistance. This keeps the voltage at the trigger pin of the first 555 timer (U1) above the threshold level, so the IC does not activate. When the fridge door opens, the fridge light falls on the LDR and its resistance decreases sharply, causing the trigger pin voltage to fall below the trigger point. This event enables U1 to switch ON and generate a pulse of fixed duration, determined by components R3, R4, and capacitor C1. The diode D1 ensures correct polarity protection, while the remaining resistors provide stable biasing and timing control.

The output of U1 is supplied to the second 555 timer (U2), which is configured in astable mode to produce continuous square wave pulses. When enabled by U1, the astable oscillations repeatedly turn the LED and buzzer ON and OFF, resulting in a blinking light and beeping sound that alerts the user that the fridge door has been left open. Components R5, R6, and C2 decide the rate of blinking and beeping. Once capacitor C1 in the first timer fully charges, U1 automatically switches OFF, thereby stopping the activation of U2 and turning the alarm OFF even if the fridge door remains open. This design saves battery power and prevents irritation due to continuous alarm sound. Overall, the circuit offers a reliable, low-cost electronic solution for reminding the user to close the fridge door, reducing cooling loss and preserving stored food effectively.
## CIRCUIT DIAGRAM:

<img width="783" height="285" alt="image" src="https://github.com/user-attachments/assets/0c5e20fe-1f9d-4ec0-8558-d7b8db74dc24" />


## EXPECTED OUTPUT:

### Schematic diagram

 ![WhatsApp Image 2025-11-21 at 21 22 18_9bea5260](https://github.com/user-attachments/assets/64c50b82-0168-4d3c-8d16-7a74ca66b458)


### Layout diagram

 ![WhatsApp Image 2025-11-21 at 21 22 18_fb679d12](https://github.com/user-attachments/assets/7fc76a57-039e-455e-8050-2b759bdb76f3)


## RESULT:
Thus, the schematic and PCB layout for the fridge door opening alarm circui has been successfully designed using Eagle software.
