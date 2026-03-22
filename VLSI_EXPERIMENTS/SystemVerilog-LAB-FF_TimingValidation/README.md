# Experiment 4: 
# Timing Validation of Flip-Flop Input using Random Data Generator for Setup and Hold Constraints

## Aim  
To validate the *timing of a Flip-Flop input* using *random data generation* in *SystemVerilog* and check *setup and hold constraints* using *ModelSim 2020.1*.

## Apparatus Required  
- Computer with *Windows OS*  
- *ModelSim 2020.1* (or later)  
- SystemVerilog source code editor  

## Description  
Timing validation ensures that a Flip-Flop operates correctly under all input conditions.  
- *Setup time:* Minimum time before the clock edge that the data input must be stable.  
- *Hold time:* Minimum time after the clock edge that the data input must remain stable.  

In this experiment:  
- A *random data generator* is used to drive the Flip-Flop input.  
- *SystemVerilog constructs* like randomize() and class or logic vectors can be used to generate test data.  
- Simulation is used to observe *violations or adherence* to setup and hold constraints.  

## Features  
- Flip-Flop timing validation using *random inputs*  
- Checks for *setup and hold constraints*  
- Includes a *testbench* for verification  
- Compatible with *ModelSim 2020.1*  

## Procedure  

1. *Open ModelSim 2020.1*  
   - Launch the IDE.  

2. *Create a New Project*  
   - File → New → Project  
   - Name it FlipFlop_Timing_Project.  

3. *Add SystemVerilog Files*  
   - Create flipflop.sv → Flip-Flop design  
   - Create flipflop_tb.sv → Testbench with random input generator  

4. *Compile the Design and Testbench*  
   - Select both files, right-click → *Compile Selected*  
   - Resolve any syntax errors  

5. *Start Simulation*  
   - Simulate → Start Simulation  
   - Select testbench module (flipflop_tb)  

6. *Add Signals to Waveform*  
   - Select clock, data, and output signals  
   - Right-click → *Add to → Wave → Selected Signals*  

7. *Run Simulation*  
   - Type in console:  
     
     run 200ns
       
   - Or use *Run button*  

8. *Analyze Waveforms*  
   - Check setup and hold times at the Flip-Flop input  
   - Verify Flip-Flop output stability for all random input patterns  

9. *Save Results*  
   - Save waveform (.wlf) for documentation  



## SystemVerilog Code Skeleton  

### Flip-Flop Design (flipflop.sv)
systemverilog
module dff(D, clk, Q);
  input  logic D;
  input  logic clk;
  output logic Q;

  always_ff @(posedge clk) 
    Q <= D;
endmodule

class RandDelay;
  rand int rand_delay;
  constraint c_range { rand_delay inside {[-3:3]}; }
endclass

### Testbench (flipflop_tb.sv)
systemverilog
module tb_dff;
  logic D, clk, Q;
  RandDelay rg;
  parameter t_setup = 2;
  parameter t_hold  = 1;

  dff uut(.D(D), .clk(clk), .Q(Q));

  initial begin
    $dumpfile("wave.vcd");
    $dumpvars(0, tb_dff);
  end

  initial begin
    clk = 0;
  end

  always #5 clk = ~clk;

  initial begin
    D = 0;
    rg = new();
    repeat (10) begin
      if (!rg.randomize()) begin
        $error("Randomization failed!");
      end

      @(posedge clk);
      #(rg.rand_delay) D = $urandom() % 2;

      if (rg.rand_delay < -t_setup)
        $display("[%0t] SETUP VIOLATION: Data changed %0d ns before clk edge", 
                  $time, rg.rand_delay);

      else if (rg.rand_delay >= 0 && rg.rand_delay < t_hold)
        $display("[%0t] HOLD VIOLATION: Data changed %0d ns after clk edge", 
                  $time, rg.rand_delay);

      else
        $display("[%0t] OK: Data stable within setup/hold window", $time);
    end
    $finish;
  end
endmodule

### Simulation Output

<img width="1857" height="358" alt="Screenshot 2025-09-30 105326" src="https://github.com/user-attachments/assets/d93b865a-0c04-4a73-b195-fc24eebbba17" />




### Result

The timing validation of Flip-Flop input using random data generation was successfully carried out in SystemVerilog HDL with ModelSim 2020.1.
The Flip-Flop maintained correct output behavior, and setup and hold times were verified for all random input cases.
