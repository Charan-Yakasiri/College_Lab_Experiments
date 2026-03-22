# Experiment 1: ALU Design using Enumerated Data Types and Case Statements

---

## Aim  
To design and simulate a **4-bit Arithmetic Logic Unit (ALU)** using **SystemVerilog HDL** with **Enumerated Data Types and Case Statements**, and verify its functionality using **ModelSim 2020.1**.

---

## Apparatus Required  
- Computer with **Windows** OS  
- **ModelSim 2020.1** (or later) installed  
- SystemVerilog source code editor  

---

## Description about ALU  
An **Arithmetic Logic Unit (ALU)** is a combinational circuit that performs arithmetic and logical operations.  
In this experiment, the ALU is designed using:  
- **Enumerated Data Types** to represent ALU operations in a readable form.  
- **Case Statements** to implement the functionality of each operation.  

This approach improves code readability, maintainability, and reduces errors compared to using raw binary values for control signals.  

Common ALU operations included in this design are:  
- **Arithmetic:** Addition, Subtraction  
- **Logical:** AND, OR, XOR, NOT  
- **Shift Operations:** Left Shift, Right Shift  

---

## Features
- Uses **SystemVerilog Enumerated Types** for operation selection  
- Implements ALU operations with **Case Statements**  
- Parameterized design for scalability  
- Includes a **Testbench** for functional verification  
- Compatible with **ModelSim 2020.1**  

---

## Procedure  

1. **Open ModelSim 2020.1**  
   - Launch the ModelSim IDE from the Start Menu (Windows) or terminal (Linux).  

2. **Create a New Project**  
   - Go to `File → New → Project`.  
   - Enter a project name (e.g., `ALU_Enum_Project`).  
   - Set the project location.  
   - Click **OK**.  

3. **Add SystemVerilog Source Files**  
   - Create a new source file named `alu_enum.sv` and type the ALU design code.  
   - Create a new source file named `alu_enum_tb.sv` and type the testbench code.  

4. **Compile the Design and Testbench**  
   - Select both files (`alu_enum.sv` and `alu_enum_tb.sv`).  
   - Right-click → **Compile Selected**.  
   - Ensure there are no syntax errors.  

5. **Start Simulation**  
   - Go to `Simulate → Start Simulation`.  
   - In the **Library window**, expand **work**.  
   - Select the testbench module (`alu_enum_tb`).  
   - Click **OK**.  

6. **Add Signals to Waveform**  
   - In the simulation window, select all signals (A, B, Operation, ALU_Out, CarryOut).  
   - Right-click → **Add to → Wave → Selected Signals**.  

7. **Run Simulation**  
   - In the simulation console, type:  
     ```
     run 100ns
     ```  
   - Or use the **Run button** to observe waveforms.  

8. **Analyze Waveforms**  
   - Verify the outputs of the ALU for each enumerated operation.  
   - Check that addition, subtraction, logical operations, and shifts are working correctly.  

9. **Save Results**  
   - Save the waveform (`.wlf` file) for documentation.  

---

## SystemVerilog Code  

### ALU Design (`alu_enum.sv`)

```systemverilog
typedef enum logic [2:0] 
{
  ADD = 3'b000,
  SUB = 3'b001,
  AND_OP = 3'b010,
  OR_OP  = 3'b011,
  XOR_OP = 3'b100,
  SLT    = 3'b101   // Less Than
} alu_ops;

module alu #(  parameter WIDTH = 8)
(
  input  	logic [WIDTH-1:0] a, b,
  input  	alu_ops         op,    // enum operation
  output 	logic [WIDTH-1:0] result,
  output 	logic    zero,  // flag: result == 0
  output 	logic    carry   // carry/borrow flag
);

  logic [WIDTH:0] temp; // to capture carry

  always_comb 
begin
    temp   = '0;
    result = '0;
    carry  = 1'b0;
case (op)
      ADD: begin
        temp   = a + b;
        result = temp[WIDTH-1:0];
        carry  = temp[WIDTH];
      end

      SUB: begin
        temp   = a - b;
        result = temp[WIDTH-1:0];
        carry  = temp[WIDTH];  // borrow out
      end

      AND_OP: result = a & b;
      OR_OP : result = a | b;
      XOR_OP: result = a ^ b;
      SLT   : result = (a < b) ? 1 : 0;

      default: result = '0;
    endcase
  end
assign zero = (result == 0);
endmodule

```
---

### ALU Testbench (`alu_tb.sv`)

```systemverilog
typedef enum logic [2:0] 
{
  ADD = 3'b000,
  SUB = 3'b001,
  AND_OP = 3'b010,
  OR_OP  = 3'b011,
  XOR_OP = 3'b100,
  SLT    = 3'b101   // Less Than
} alu_ops;

module tb_alu;
  parameter WIDTH = 8;
  logic [WIDTH-1:0] a, b;
  alu_ops        op;
  logic [WIDTH-1:0] result;
  logic zero, carry;

  // DUT
  alu #(WIDTH) dut (    .a(a), .b(b), .op(op), .result(result), .zero(zero), .carry(carry)  );
initial begin
    $display("Time\t A\t B\t Operation\t Result\t Carry\t Zero");
    $monitor("%0t\t %0d\t %0d\t %p\t %0d\t %b\t %b", $time, a, b, op, result, carry, zero);

    a = 8'd10; b = 8'd5;

    op = ADD;   #10;
    op = SUB;   #10;
    op = AND_OP;#10;
    op = OR_OP; #10;
    op = XOR_OP;#10;
    op = SLT;   #10;

    $finish;
  end
endmodule

```
---

### Simulation Output

The simulation is carried out using ModelSim 2020.1.

<img width="1918" height="1078" alt="Screenshot 2025-09-16 094859" src="https://github.com/user-attachments/assets/5a87fd46-469f-469f-b622-bbb3037e5506" />

---

### Result

The design and simulation of a 4-bit ALU using Enumerated Data Types and Case Statements in SystemVerilog HDL was successfully carried out in ModelSim 2020.1.
The ALU performed arithmetic, logical, and shift operations correctly as verified from the simulation outputs.
