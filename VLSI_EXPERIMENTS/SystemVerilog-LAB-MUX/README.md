# Experiment 2: Design and Functional Verification of 8:1 Multiplexer using SystemVerilog

---

## Aim  
To design and functionally verify an 8:1 Multiplexer using SystemVerilog HDL and simulate it using ModelSim 2020.1.

---

## Apparatus Required  
- Computer with Windows OS  
- ModelSim 2020.1 (or later) installed  
- SystemVerilog source code editor  

---

## Description about 8:1 Multiplexer  
A Multiplexer (MUX) is a combinational logic circuit that selects one of several input signals and forwards the selected input to a single output line.  
- An 8:1 MUX has 8 input lines, **3 select lines, and **1 output line.  
- The output depends on the binary value of the select inputs.  

Truth Table Overview:  

| Select Lines (S2 S1 S0) | Output (Y) |  
|--------------------------|------------|  
| 000                      | I0         |  
| 001                      | I1         |  
| 010                      | I2         |  
| 011                      | I3         |  
| 100                      | I4         |  
| 101                      | I5         |  
| 110                      | I6         |  
| 111                      | I7         |  

---

## Features  
- Designed in SystemVerilog for clarity and modularity  
- Supports 8 data inputs and 3-bit selection  
- Testbench for functional verification  
- Compatible with ModelSim 2020.1  

---

## Procedure  

1. Open ModelSim 2020.1  
   - Launch the ModelSim IDE from the Start Menu.  

2. Create a New Project  
   - Go to File → New → Project.  
   - Enter a project name (e.g., MUX8to1_Project).  
   - Set the project location.  
   - Click OK.  

3. Add SystemVerilog Source Files  
   - Create a new source file named mux8to1.sv for the multiplexer design.  
   - Create a new source file named mux8to1_tb.sv for the testbench.  

4. Compile the Design and Testbench  
   - Select both files (mux8to1.sv and mux8to1_tb.sv).  
   - Right-click → Compile Selected.  
   - Ensure there are no syntax errors.  

5. Start Simulation  
   - Go to Simulate → Start Simulation.  
   - Expand work in the Library window.  
   - Select the testbench module (mux8to1_tb).  
   - Click OK.  

6. Add Signals to Waveform  
   - Select inputs, select lines, and output.  
   - Right-click → Add to → Wave → Selected Signals.  

7. Run Simulation  
   - In the simulation console, type:  
     
     run 100ns
       
   - Or use the Run button.  

8. Analyze Waveforms  
   - Check that the output matches the corresponding input for different select line values.  

9. Save Results  
   - Save the waveform (.wlf file) for documentation.  

---

## SystemVerilog Code  

### Multiplexer Design (mux8to1.sv)
~~~
systemverilog
// 8:1 Multiplexer using case statement 
module mux8to1_case (
  input  logic [7:0] d,   // 8 data inputs
  input  logic [2:0] sel, // 3-bit select line
  output logic       y    // single output
);

  // RTL description using case
  always_comb begin
    case (sel)
      3'b000: y = d[0];
      3'b001: y = d[1];
      3'b010: y = d[2];
      3'b011: y = d[3];
      3'b100: y = d[4];
      3'b101: y = d[5];
      3'b110: y = d[6];
      3'b111: y = d[7];
      default: y = 1'b0;   // safe default assignment
    endcase
  end

endmodule

~~~
### Testbench code (mux8to1_tb.sv)
~~~
systemverilog
module tb_mux8to1_case;

  logic [7:0] d;
  logic [2:0] sel;
  logic y;

  // Instantiate DUT
  mux8to1_case uut (d, sel, y);

  initial begin
    // Apply test patterns
    d = 8'b10101010; // alternate 1s and 0s

    $display("Time | Sel | Output");
    for (int i = 0; i < 8; i++) begin
      sel = i;
      #10;
      $display("%0t   | %0d   | %0b", $time, sel, y);
    end

    $finish;
  end
endmodule
~~~


---

### Simulation Output

The simulation is carried out using ModelSim 2020.1.

Waveforms will display the selected input line being passed to the output according to the select signals.

<img width="1918" height="1078" alt="Screenshot 2025-09-16 092944" src="https://github.com/user-attachments/assets/fb943a53-f22c-4178-b629-5bfc77f1c8db" />

---

### Result

The design and functional verification of an 8:1 Multiplexer using SystemVerilog HDL was successfully carried out in ModelSim 2020.1.
The multiplexer correctly selected one of the eight inputs based on the 3-bit select signal.
