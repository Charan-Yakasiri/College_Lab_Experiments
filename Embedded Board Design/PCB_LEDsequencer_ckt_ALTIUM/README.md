# Exp-6 Design a 10-Led Sequencer circuit using Altium software and generate the Gerber file.
## AIM:
To design the schematic and PCB layout diagram of an LED Sequencer circui circuit using Altium software.
## EQUIPMENT REQUIRED:
●	Hardware: Personal Computer (PC)<br>
●	Software: Altium  <br>
## PROCEDURE:
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
>

## THEORY:

555 Timer as Clock Pulse Generator<br>
In the circuit, the 555 timer IC is configured in astable mode, which means it generates continuous square wave pulses without any external triggering. The resistors (R1 and R2) and the capacitor (C1) connected to the timer determine the timing frequency. These pulses appear at pin 3 of the 555 timer and serve as clock inputs for the next stage — the CD4017 counter. The frequency of blinking (how fast LEDs move from one to another) depends on the values of R1, R2, and C1.

CD4017 Decade Counter for Sequential Switching<br>
The output pulses from the 555 timer are connected to pin 14 (Clock) of the CD4017 decade counter. This IC has 10 output pins (Q0–Q9), each going HIGH one at a time in sequence for every clock pulse it receives. The RESET (pin 15) is grounded to allow full counting, and ENABLE (pin 13) is also grounded to ensure the counter functions without being disabled.

LEDs Connected to CD4017 Outputs<br>
Each of the 10 outputs (Q0 to Q9) is connected to an individual LED via a current-limiting resistor (R3 to R12). When an output pin goes HIGH, the corresponding LED turns ON. On the next clock pulse, the output shifts to the next pin, and the LED connected to that pin lights up. This creates a chasing LED effect, where only one LED is ON at a time, and it moves in a sequence from D1 to D10.

Cyclic Repetition of Sequence<br>
After reaching Q9 (D10), the CD4017 automatically resets back to Q0 (D1) on the next clock pulse, creating a continuous loop of sequential lighting. This cycle will keep repeating as long as the 555 timer continues to produce clock pulses.

Power Supply and Grounding<br>
The circuit is powered by a DC supply (typically 5V or 9V) connected at the VCC and GND lines. All ICs and components share a common ground to maintain correct operation.

## CIRCUIT DIAGRAM:
![image](https://github.com/user-attachments/assets/2cb084f1-22ea-4d4e-816d-eee72cd2918f)


## Schematic diagram:
<img width="1275" height="672" alt="image" src="https://github.com/user-attachments/assets/696f7c82-dd21-43fe-9b0d-39a39e21b99d" />


## Layout diagram:
 <img width="1280" height="686" alt="image" src="https://github.com/user-attachments/assets/a30df839-c6e7-4a7c-954b-9c9fadb2110e" />

## RESULT:
Thus, the schematic and PCB layout for the LED sequencer circuit has been successfully designed using Altium software.
