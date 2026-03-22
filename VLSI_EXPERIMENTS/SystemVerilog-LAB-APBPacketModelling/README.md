# Experiment 3: Create and Use Classes and Objects to Model APB Packet.

---

## Aim  
To design and verify an **APB (Advanced Peripheral Bus) packet model** using **SystemVerilog object-oriented programming concepts** such as classes and objects, and simulate it using **ModelSim 2020.1**.

---

## Apparatus Required  
- Computer with **Windows OS**  
- **ModelSim 2020.1** (or later)  
- SystemVerilog source code editor  

---

## Description about APB Packet Modeling  
The **Advanced Peripheral Bus (APB)** is part of the AMBA protocol family used for connecting low-bandwidth peripherals.  
In this experiment, we use **SystemVerilog OOP concepts** to model an APB packet.  

- **Classes and Objects** in SystemVerilog allow abstraction and modularity.  
- An APB packet generally contains:  
  - **Address**  
  - **Data**  
  - **Control signals** (Read/Write, Select, Enable, Ready)  
- Using OOP, packets can be **created, initialized, randomized, and reused**, simplifying testbench construction.  

---

## Features  
- Written in **SystemVerilog OOP style**  
- Defines an **APB Packet class** with properties (address, data, control signals)  
- Includes **methods** for packet initialization and display  
- Demonstrates **object creation and manipulation**  
- Simulated using **ModelSim 2020.1**  

---

## Procedure  

1. **Open ModelSim 2020.1**  
   - Launch ModelSim from Start Menu.  

2. **Create a New Project**  
   - `File → New → Project`.  
   - Name it `APB_Packet_Project`.  

3. **Add SystemVerilog Files**  
   - Create a file `apb_packet.sv` → Define the APB Packet class.  
   - Create a file `apb_tb.sv` → Instantiate objects and test the class.  

4. **Compile the Files**  
   - Select both `.sv` files.  
   - Right-click → **Compile Selected**.  
   - Ensure no errors exist.  

5. **Start Simulation**  
   - `Simulate → Start Simulation`.  
   - Select the testbench module (`apb_tb`).  

6. **Add Signals and Run**  
   - Add relevant signals to the waveform.  
   - Run the simulation for required time.  

7. **Analyze Output**  
   - Observe the creation and display of APB packets.  
   - Verify correct modeling of properties and methods.  

---

## SystemVerilog Code   

### APB Packet Class (`apb_packet.sv`)  
```
  class APB_Packet;
    rand bit [31:0] addr;   
    rand bit [31:0] data;   
    rand bit        wr;     
    string resp;            

    function new(bit [31:0] addr = 0, bit [31:0] data = 0, bit wr = 0);
      this.addr = addr;
      this.data = data;
      this.wr   = wr;
      this.resp = "OK";
    endfunction

    function void display();
      $display("APB Packet => Addr: %h, Data: %h, WR: %0b, Resp: %s", 
                addr, data, wr, resp);
    endfunction
  endclass

  
  class APB_WritePacket extends APB_Packet;
    function new(bit [31:0] addr, bit [31:0] data);
      super.new(addr, data, 1); // Write = 1
    endfunction
  endclass



  class APB_ReadPacket extends APB_Packet;
    function new(bit [31:0] addr);
      super.new(addr, 0, 0); // Write = 0
    endfunction
  endclass

```

### APB Packet Class (`apb_tb.sv`) 
```
module apb_packet_demo;

  initial begin
    APB_Packet p; 

    
    p = APB_WritePacket::new(32'h1000, 32'hABCD1234);
    p.display();

    
    p = APB_ReadPacket::new(32'h2000);
    p.display();
  end
endmodule

```
---
### Simulation Output

The simulation is carried out using ModelSim 2020.1.

Output log will show the APB packet details created using class objects.

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/662c6ddc-8a14-432f-b204-c53198c7bd63" />


---

### Result

The design and verification of an APB packet model using SystemVerilog classes and objects was successfully carried out in ModelSim 2020.1.
The experiment demonstrated how OOP concepts simplify modeling and reusability in SystemVerilog testbenches.
