# Design-an-Infrared-remote-control-circuit-using-Eagle-software-and-generate-the-Gerber-file.

## AIM:
To design the schematic and PCB layout diagram of an Infrared remote control circuit using Eagle software.

## EQUIPMENT REQUIRED:
●	Hardware: Personal Computer (PC)<br>
●	Software: Eagle <br>
## PROCEDURE:
1.	Create a New Project:<br>
* Launch EAGLE and start a new project for your PCB design.<br>
* Within the project, create a new schematic file.<br>
2.	Add Components:<br>
*	Utilize the built-in libraries in EAGLE or create custom libraries if needed.<br>
*	Use the 'Add' tool to place the required components onto the schematic sheet.<br>
3.	Make Connections:<br>
*	Connect the components using the 'Net' tool.<br>
*	Label the nets clearly to maintain clarity and organization in your design.<br>
4.	Check for Errors:<br>
*	Once the schematic design is complete, perform an Electrical Rule Check (ERC) to identify and correct any errors.<br>
*	Save the schematic after confirming that no errors are present.<br>
5.	Switch to Board Layout:<br>
*	Click on the 'Generate/Switch to Board' button to create the PCB layout from the schematic.<br>
6.	Arrange Components and Route Traces:<br>
*	In the board layout editor, arrange the components to optimize space and reduce signal interference.<br>
*	Use the 'Route' tool to connect the components based on the schematic design.<br>
*	Ensure proper routing by utilizing the available editing tools in EAGLE to avoid design rule violations.<br>
7.	Design Rule Check (DRC):<br>
*	Perform a Design Rule Check (DRC) to ensure that the routing and layout comply with design standards and that there are no issues.<br>
*	Save the board layout after resolving any errors.<br>
8.	Generate Gerber Files:<br>
*	Go to File > CAM Processor and configure the CAM jobs to generate Gerber files for all PCB layers, such as copper layers, silkscreen, solder mask, and drill files.<br>
*	Verify the generated files to ensure they contain all necessary information for manufacturing.<br>
9.	Save Manufacturing Files:<br>
*	Save the Gerber files and any other required manufacturing files to send to your PCB manufacturer for fabrication.<br>

## THEORY:
The Infrared Remote Control Switch is a simple electronic circuit that uses an infrared (IR) receiver to detect signals from a standard TV remote and control an electrical load, such as a lamp or appliance, through a relay. At the heart of the circuit lies the CD4027 IC, which is a dual JK flip-flop. JK flip-flops are bistable multivibrators capable of storing one bit of data and toggling their state with every pulse input. In this circuit, the TSOP1738 IR receiver module is used to detect IR pulses sent by a remote control. The TSOP1738 is designed to receive 38kHz modulated infrared signals and output a demodulated digital signal that can be read by a microcontroller or logic circuit. The 2N4403 PNP transistor is used to amplify and condition the signal from the TSOP1738, ensuring a reliable trigger for the flip-flop. This type of system demonstrates the fundamental concept of remote-controlled electronics using modulated IR signals, logic circuitry, and electromechanical switching components like relays.
## Working:
When a button on the IR remote is pressed, it sends a modulated 38kHz IR signal which is received by the TSOP1738. The TSOP demodulates the signal and produces a low pulse which is fed into the base of the first 2N4403 transistor, acting as an amplifier. This transistor then provides a strong triggering signal to the CD4027 flip-flop IC, which is wired to toggle its output state with each pulse received. The output from the flip-flop then controls the base of a second 2N4403 transistor, which functions as a switch to drive a 5V relay. When the flip-flop output goes high, the transistor conducts and energizes the relay coil, turning ON the connected load. On receiving the next IR pulse, the output toggles low, deactivating the relay and turning OFF the load. An LED indicator connected in parallel with the relay provides a visual cue of the ON/OFF status. The 1N4007 diode across the relay protects the circuit from voltage spikes due to back EMF when the relay is switched OFF. This toggling operation continues every time a button on the IR remote is pressed, making it suitable for simple wireless control applications.
## CIRCUIT DIAGRAM:
![image](https://github.com/user-attachments/assets/3e488286-ea7d-4a9b-a057-02a31fdf4430)

## EXPECTED OUTPUT:
### Schematic diagram
 <img width="1041" height="527" alt="image" src="https://github.com/user-attachments/assets/991190c8-39f1-4b7e-a52a-8593593a0e2b" />

### Layout diagram
 <img width="954" height="637" alt="image" src="https://github.com/user-attachments/assets/080f2cf7-9d45-4e0b-822b-b02346315777" />

## RESULT:
Thus, the schematic and PCB layout for the Infrared remote control circuit has been successfully designed using Eagle software.
