# Experiment 8: Functional Verification of Asynchronous FIFO

---

## Aim  
To perform **functional verification** of an **Asynchronous FIFO (First-In-First-Out)** design using **SystemVerilog**, ensuring reliable data transfer between two clock domains.

---

## Apparatus Required  
- Computer with **Windows OS**  
- **ModelSim 2020.1** (or later) or **EDA Playground**  
- **SystemVerilog source code editor**

---

## Description  
An **Asynchronous FIFO** allows data to be safely transferred between two independent clock domains — typically used in systems where producer and consumer operate at different clock frequencies.  

Functional verification ensures that:
- The FIFO **correctly stores and retrieves data**.  
- **Full** and **Empty** flags operate correctly.  
- No **data corruption** occurs despite differing clock speeds.  

This experiment verifies FIFO behavior through **random stimulus generation** and **testbench-driven verification** in SystemVerilog.

---

## Features  
- Asynchronous FIFO design with independent read/write clocks  
- Verification using **SystemVerilog testbench**  
- Includes **randomized data generation**  
- Compatible with **ModelSim** or **EDA Playground**

---

## Procedure  

1. **Open EDA Playground or ModelSim**  
   - Create a new SystemVerilog project named `Async_FIFO_Verification`.

2. **Add the Following Files:**  
   - `async_fifo.sv` → FIFO Design  
   - `fifo_tb.sv` → Testbench for functional verification  

3. **Compile Design and Testbench**  
   - Check for syntax and semantic correctness.

4. **Run Simulation**  
   - In EDA Playground: Click **Run**  
   
5. **Observe Waveform and Console Output**  
   - Check data flow between write and read sides.  
   - Verify correct behavior of **full** and **empty** flags.

6. **Record Observations**  
   - Save simulation results for documentation.

---

## SystemVerilog Code

### Asynchronous FIFO Design (`async_fifo.sv`)
```
module async_fifo #(
    parameter DATA_WIDTH = 8,
    parameter DEPTH = 8
) (
    input  logic                  wr_clk,
    input  logic                  rd_clk,
    input  logic                  rst,
    input  logic                  wr_en,
    input  logic                  rd_en,
    input  logic [DATA_WIDTH-1:0] din,
    output logic [DATA_WIDTH-1:0] dout,
    output logic                  full,
    output logic                  empty
);

    logic [DATA_WIDTH-1:0] mem [0:DEPTH-1];
    logic [$clog2(DEPTH):0] wr_ptr, rd_ptr;

    // Write logic
    always_ff @(posedge wr_clk or posedge rst) begin
        if (rst)
            wr_ptr <= 0;
        else if (wr_en && !full) begin
            mem[wr_ptr[$clog2(DEPTH)-1:0]] <= din;
            wr_ptr <= wr_ptr + 1;
        end
    end

    // Read logic
    always_ff @(posedge rd_clk or posedge rst) begin
        if (rst)
            rd_ptr <= 0;
        else if (rd_en && !empty) begin
            dout <= mem[rd_ptr[$clog2(DEPTH)-1:0]];
            rd_ptr <= rd_ptr + 1;
        end
    end

    // Status flags
    assign full  = ( (wr_ptr[$clog2(DEPTH)]    != rd_ptr[$clog2(DEPTH)]) &&
                     (wr_ptr[$clog2(DEPTH)-1:0] == rd_ptr[$clog2(DEPTH)-1:0]) );
    assign empty = (wr_ptr == rd_ptr);

endmodule
      
```
### Testbench
```systemverilog
module fifo_tb;
    parameter DATA_WIDTH = 8;
    parameter DEPTH = 8;

    logic wr_clk, rd_clk, rst;
    logic wr_en, rd_en;
    logic [DATA_WIDTH-1:0] din;
    logic [DATA_WIDTH-1:0] dout;
    logic full, empty;

    // Instantiate DUT
    async_fifo #(DATA_WIDTH, DEPTH) uut (
        .wr_clk(wr_clk),
        .rd_clk(rd_clk),
        .rst(rst),
        .wr_en(wr_en),
        .rd_en(rd_en),
        .din(din),
        .dout(dout),
        .full(full),
        .empty(empty)
    );

    // Clock generation (different frequencies)
    initial begin
        wr_clk = 0;
        forever #4 wr_clk = ~wr_clk; // 125 MHz
    end

    initial begin
        rd_clk = 0;
        forever #7 rd_clk = ~rd_clk; // ~71 MHz
    end

    // Reset sequence
    initial begin
        rst = 1;
        #15 rst = 0;
    end

    // Write process
    initial begin
        wr_en = 0;
        din = 0;
        wait(!rst);
        repeat (15) begin
            @(posedge wr_clk);
            if (!full) begin
                wr_en = 1;
                din = $urandom_range(0, 255);
                $display("WRITE @%0t: Data = %0d", $time, din);
            end else begin
                wr_en = 0;
            end
        end
        wr_en = 0;
    end

    // Read process
    initial begin
        rd_en = 0;
        wait(!rst);
        repeat (20) begin
            @(posedge rd_clk);
            if (!empty) begin
                rd_en = 1;
                $display("READ  @%0t: Data = %0d", $time, dout);
            end else begin
                rd_en = 0;
            end
        end
        rd_en = 0;
        #50;
        $display("Simulation Completed");
        $finish;
    end
endmodule
```
### Simulation Output
<img width="1913" height="955" alt="Screenshot 2025-11-11 112645" src="https://github.com/user-attachments/assets/c42817a3-3a11-4771-86d0-b03c6aef4df2" />
<img width="1913" height="941" alt="Screenshot 2025-11-11 112704" src="https://github.com/user-attachments/assets/ba0fba51-bb25-4a37-9279-f20fc6fb06e8" />


### Result

The Functional Verification of Asynchronous FIFO was successfully carried out using SystemVerilog.The FIFO was verified for correct data transfer across two asynchronous clock domains, ensuring proper write/read synchronization, flag operation, and data integrity.
