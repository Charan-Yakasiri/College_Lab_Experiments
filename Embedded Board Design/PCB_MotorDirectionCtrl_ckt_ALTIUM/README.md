# DC-motor-directional-control-using-Altium-software
# Exp-9--Design-a- DC motor direction control-circuit-using-Altium-software-and-generate-the-Gerber-file.
# AIM:
To design the schematic and PCB layout diagram of an DC motor direction control circuit using Altium software.
# EQUIPMENT REQUIRED:
●	Hardware: Personal Computer (PC)<br>
●	Software: Altium  <br>
# PROCEDURE:
•  Open Altium & create a project<br>
File → New → Project → choose PCB Project. Give it a name and folder.<br>
•  Add a schematic sheet<br>
Right-click the project → Add New to Project → Schematic. Save it (e.g., project.SchDoc).<br>
•  Place components<br>
Use Components panel or Place → Part. Search library parts (resistors, ICs, connectors). Place each part and assign a designator (R1, C1, U1).<br>
•  Wire the circuit<br>
Use the Wire tool to connect pins. Add net labels for power (VCC, GND) and important signals. Keep wires neat.<br>
•  Annotate & check<br>
Tools → Annotation to give unique designators if needed. Run Electrical Rule Check (ERC) and fix any errors/warnings.<br>
•  Add PCB document<br>
Right-click project → Add New to Project → PCB. Save it (e.g., project.PcbDoc).<br>
•  Compile and update PCB<br>
On the schematic: Design → Compile Project. Then Design → Update PCB Document → Review ECO → Execute to push parts to PCB.<br>
•  Define board shape<br>
In PCB view: Design → Define Board Shape → Draw outline to the required size.<br>
•  Place components on board<br>
Move parts from the component list onto the board. Place connectors at the edge, group related parts, keep critical parts (crystals, sensors) positioned carefully.<br>
•  Set design rules<br>
PCB → Design Rules → set trace width, clearance, via sizes. For beginners, use default rules or teacher-provided values.<br>
•  Route tracks<br>
Use Interactive Routing (Route → Interactive Route) to connect pads. Route power traces wider (e.g., 1.5–2×). Use ratsnest to see remaining connections.<br>
•  Add ground/power planes (optional)<br>
Place a polygon pour for GND or VCC for better grounding: Place → Polygon Pour → set layer & net → Pour.<br>
•  Run Design Rule Check (DRC)<br>
PCB → Design → Rules Check (or Tools → Design Rule Check). Fix spacing, un-routed nets, or overlapping pads.<br>
•  Add silkscreen & labels<br>
On the Silkscreen layer, add component names, polarity marks, board name/version.<br>
•  3D check (optional)<br>
View → 3D Layout Mode to inspect component heights and mechanical fit.<br>
•  Prepare fabrication outputs<br>
File → Fabrication Outputs → Gerber Files (select layers: top/bottom copper, solder mask, silkscreen). Also generate NC Drill Files.<br>
•  Generate assembly files<br>
File → Assembly Outputs → Pick and Place (Centroid) and BOM (Bill of Materials).<br>
•  Verify outputs<br>
Open generated Gerbers in a Gerber viewer to confirm layers and drill map look correct.<br>
•  Create final archive<br>
Zip the project folder and all output files (Gerbers, Drill, BOM, Pick-and-Place). Add a Readme with board name and revision.<br>
•  Send to manufacturer<br>
Upload the zip to your PCB fab and follow their order steps.<br>
# THEORY:
## Construction
The circuit is built using two NPN transistors (BC547), two 1 kΩ resistors, two pushbutton switches (FORWARD and REVERSE), a 100 nF capacitor, a DC motor, and a battery as the power source. Each transistor is connected in such a way that one drives the motor in the forward direction while the other drives it in the reverse direction. The push buttons control the base terminal of the transistors through the 1 kΩ resistors, ensuring safe biasing. The capacitor is placed across the two signal lines to help reduce electrical noise and provide smooth switching. The motor terminals are connected such that reversing the current path changes the rotation direction.
##  Working Principle
The circuit works based on the ability of the transistors to act as electronic switches. When a small voltage is applied at the base terminal of a BC547 transistor through a push button, it allows a larger current to flow from collector to emitter. This makes the transistor conduct and power the DC motor. By selecting which transistor is activated, the current through the motor can be made to flow in opposite directions, thereby changing its rotation direction.
## Operation
When the FORWARD switch (SW6) is pressed, the left BC547 transistor receives base current via the 1 kΩ resistor. This turns it ON, allowing current to pass through the motor in one direction, causing it to rotate forward. When the REVERSE switch (SW5) is pressed instead, the right BC547 transistor is triggered, reversing the direction of current flow through the motor and making it rotate in the opposite direction. The 100 nF capacitor reduces switching noise and protects the components from sudden current spikes during direction changes. Only one switch should be pressed at a time to avoid short-circuit-type conditions.
##  Applications
This circuit is useful for controlling the direction of small DC motors in low-power projects. It is commonly used in school and college robotics projects, motorized toys, conveyor belt models, mechanical arm movements, car wiper simulation models, and mini CNC or automation demonstrations. Because it uses fewer components, it is ideal for beginners learning about transistor-based motor control and the concept of forward–reverse rotation.

# CIRCUIT DIAGRAM:
 
 <img width="795" height="423" alt="image" src="https://github.com/user-attachments/assets/880378eb-9f90-4342-bc1a-1b7333c1ac87" />

# EXPECTED OUTPUT:
## Schematic diagram:
 <img width="1023" height="513" alt="image" src="https://github.com/user-attachments/assets/04b5d640-f199-4e2a-957e-8397c3d7db5e" />

## Layout diagram:

 <img width="1108" height="572" alt="image" src="https://github.com/user-attachments/assets/f21dec55-0541-4c44-8929-c3fdf7e8796d" />

# RESULT:
Thus, the schematic and PCB layout for the DC motor direction control circuit has been successfully designed using Altium software.
