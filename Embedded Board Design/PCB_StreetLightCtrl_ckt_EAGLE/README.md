# Design an Automatic street light PCB circuit using Eagle software and generate the Gerber file.

## AIM:
To design the schematic and PCB layout diagram of an automatic street light circuit using Eagle software.
## EQUIPMENT REQUIRED:
●	Hardware: Personal Computer (PC)<br>
●	Software: Eagle<br>
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
The automatic street light circuit is a practical application of a light-sensing system using an LDR (Light Dependent Resistor) and basic transistor switching. The core concept behind this system is to detect ambient light levels and control an external electrical load (such as a lamp) accordingly, without manual intervention. The LDR is a passive electronic component whose resistance varies inversely with the intensity of light falling on it. That is, the resistance of the LDR is high in darkness and low in bright light. This property makes it an ideal sensor for distinguishing between day and night. In this circuit, the LDR is connected in series with a variable resistor (or potentiometer), forming a voltage divider network. This setup is designed such that it triggers the transistors based on the voltage developed across the LDR. Two NPN transistors (BC547) are used in a Darlington-like arrangement to amplify the small signal from the LDR divider and control a 12V relay, which ultimately switches a 220V AC lamp. A diode is connected across the relay coil to protect the transistor from voltage spikes that occur due to the sudden de-energizing of the relay coil. This simple yet efficient theory allows for automated control of lighting systems, reducing energy consumption and providing hands-free operation.
## Working
The circuit functions by sensing the amount of light falling on the LDR and responding accordingly by turning the connected AC lamp ON or OFF. During daytime or in a well-lit environment, the LDR’s resistance drops significantly, resulting in a lower voltage at the base of the first transistor (Q1). Since this voltage is below the transistor's threshold, Q1 remains OFF, and as a result, the second transistor (Q2) also stays OFF. With both transistors non-conducting, the relay coil receives no current and remains de-energized, keeping the lamp circuit open and the lamp OFF. As night approaches and ambient light reduces, the resistance of the LDR increases, causing a higher voltage drop across it and increasing the voltage at the base of Q1. Once this voltage crosses the required threshold, Q1 begins to conduct, allowing current to flow into the base of Q2, which also starts conducting. When Q2 turns ON, it completes the circuit for the relay coil, energizing it. This activates the relay, closing its normally open contacts and allowing the 220V AC supply to power the connected lamp (L1). The diode (D1) acts as a flyback diode, safely dissipating the back emf produced by the relay coil when switching, thereby protecting Q2 from damage. In this way, the circuit ensures that the lamp automatically switches ON at night and turns OFF during the day, based solely on surrounding light conditions.
## CIRCUIT DIAGRAM:
![image](https://github.com/user-attachments/assets/72aa69d2-792f-46bc-810e-50b25a13864f)

## EXPECTED OUTPUT:
### Schematic diagram
 <img width="1919" height="1018" alt="image" src="https://github.com/user-attachments/assets/136b87a4-c220-4ed8-b843-178d4dfadad1" />

### Layout diagram
 <img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/110c1363-c255-41f3-af2a-007424431812" />

## RESULT:
Thus, the schematic and PCB layout for the automatic street light circuit has been successfully designed using Eagle software.
