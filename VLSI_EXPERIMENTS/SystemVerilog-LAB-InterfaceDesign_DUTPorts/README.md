# Experiment 7: Interface Design for DUT Ports and Signal Encapsulation

---

## Aim  
To design a **SystemVerilog interface** for encapsulating signals between a **Design Under Test (DUT)** and its **testbench**, ensuring efficient connectivity and modular design verification.

---

## Apparatus Required  
- Computer with **Windows OS**  
- **ModelSim 2020.1** (or later) or **EDA Playground**  
- **SystemVerilog source code editor**

---

## Description  
In complex designs, connecting multiple signals between the **testbench** and **DUT** can be error-prone.  
SystemVerilog **interfaces** provide a way to **bundle related signals** into a single hierarchical structure, simplifying port connections and improving reusability.

In this experiment:
- An **interface** is created to encapsulate communication signals.  
- The **DUT** and **testbench** both reference this interface, avoiding redundant port declarations.  
- The **modport** construct is used to define signal directionality for master and slave roles.

---

## Features  
- Clean and modular **DUT–testbench** connection  
- Demonstrates **signal encapsulation** using `interface`  
- Implements **modport direction control**  
- Verified using **ModelSim 2020.1** or **EDA Playground**

---

## Procedure  

1. **Open ModelSim or EDA Playground**  
   - Create a new SystemVerilog project named `Interface_Design_Project`.

2. **Add SystemVerilog Files**  
   - `dut.sv` → Design Under Test  
   - `dut_if.sv` → Interface definition  
   - `dut_tb.sv` → Testbench  

3. **Compile Files**  
   - Ensure all `.sv` files compile successfully.

4. **Run Simulation**  
   - In EDA Playground, click **Run**  
   - In ModelSim, type:  run 200ns

5. **View Waveform**  
   - Observe encapsulated signals (`clk`, `rst`, `data_in`, `data_out`).

6. **Verify Results**  
   - Check that interface signals correctly propagate from testbench to DUT.

---

## SystemVerilog Code

### Interface Definition
```
interface dut_if (input logic clk, input logic rst);
    logic [7:0] data_in;
    logic [7:0] data_out;
    logic       valid;

    // Define modports for direction control
    modport DUT_side (input clk, rst, data_in, valid, output data_out);
    modport TB_side  (input clk, rst, data_out, output data_in, valid);
endinterface
```
### Design Under Test
```
module dut (dut_if.DUT_side bus);
    always_ff @(posedge bus.clk or posedge bus.rst) begin
        if (bus.rst)
            bus.data_out <= 8'h00;
        else if (bus.valid)
            bus.data_out <= bus.data_in + 8'h01; // Simple processing
    end
endmodule
```
### Testbench
```
module dut_tb;
    logic clk, rst;

    // Instantiate interface
    dut_if bus(clk, rst);

    // Instantiate DUT
    dut uut (.bus(bus));

    // Clock generation
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    // Reset generation
    initial begin
        rst = 1;
        #10 rst = 0;
    end

    // Test sequence
    initial begin
        bus.valid = 0;
        bus.data_in = 0;
        #20;

        repeat (5) begin
            @(posedge clk);
            bus.valid = 1;
            bus.data_in = $urandom_range(0, 255);
            $display("Input: %0d, Output: %0d", bus.data_in, bus.data_out);
        end

        bus.valid = 0;
        #20;
        $display("Simulation Completed");
        $finish;
    end
endmodule
```
### Simulation Output

<img width="1920" height="1049" alt="512533774-5860a4f4-9b2a-466b-bf2d-30b1ffb29949" src="https://github.com/user-attachments/assets/857bc5cc-6256-4d20-be4a-6cae42acb653" />



### Result

The Interface Design for DUT Ports and Signal Encapsulation was successfully implemented and verified using SystemVerilog. The experiment demonstrated efficient connectivity between the DUT and testbench using an interface with modports, ensuring better readability, reusability, and verification modularity.
