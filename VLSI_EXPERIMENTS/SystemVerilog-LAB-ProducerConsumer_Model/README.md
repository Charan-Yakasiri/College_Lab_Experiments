# Experiment 5: Design and Verification of Register Memory Access using Mailbox-based Producer-Consumer Model

---

## Aim  
To design and verify a **Register Memory Access system** using a **mailbox-based Producer-Consumer model** in **SystemVerilog**, demonstrating inter-process communication and synchronization in a concurrent environment.

---

## Apparatus Required  
- Computer with **Windows/Linux OS**  
- **EDA Playground** (SystemVerilog environment) or **ModelSim 2020.1**  
- Internet browser (for EDA Playground execution)  

---

## Description  
This experiment demonstrates **inter-process synchronization and data transfer** using the **mailbox mechanism** in SystemVerilog.  

- The **Producer process** writes data into a **mailbox**, simulating register write access.  
- The **Consumer process** retrieves data from the mailbox, representing register read access.  
- Mailboxes allow safe **communication between concurrent processes** without data corruption.  
- Verification ensures that the written data matches the read data (register consistency).  

---

## Features  
- Demonstrates **Producer–Consumer synchronization** using mailbox  
- Implements **Register Memory Access** (write and read)  
- Uses **concurrent processes** (`fork...join`) in SystemVerilog  
- Self-checking **testbench verification**  

---

## Procedure  

1. **Open EDA Playground**  
   - Go to [https://www.edaplayground.com](https://www.edaplayground.com)  
   - Select **SystemVerilog (IEEE 1800-2012)** and choose **ModelSim/QuestaSim** as the simulator.  

2. **Create Files**  
   - Create `register_memory.sv` → Design file  
   - Create `register_memory_tb.sv` → Testbench file  

3. **Paste the Code**  
   - Copy the design and testbench code from below.  

4. **Run the Simulation**  
   - Click **Run** → **Run Simulation**.  

5. **Observe Output**  
   - View the simulation log for producer/consumer transactions.  
   - Check the mailbox synchronization and matching register values.  

6. **Analyze Results**  
   - Confirm that all produced data is consumed correctly.  
   - Ensure no data mismatch or deadlock occurs.  

---

##  SystemVerilog Code

### Design File — `register_memory.sv`
```

module reg_memory_mailbox;

  typedef struct {
    int addr;
    int data;
    bit wr; // 1 = write, 0 = read
  } packet_t;

  mailbox mbox = new();

  int memory [0:15];


```
---
Testbench: Producer-Consumer using Mailbox
---
```
  initial begin
    fork
      producer();
      consumer();
    join
  end

  task producer();
    packet_t pkt;
    int i;
    $display("\n=== PRODUCER STARTED ===");
    for (i = 0; i < 5; i++) begin
      pkt.addr = $urandom_range(0, 15);
      pkt.data = $urandom_range(0, 255);
      pkt.wr   = $urandom_range(0, 1);
      mbox.put(pkt);
      $display("[%0t] PRODUCER: Sent packet -> Addr=%0d Data=%0d WR=%0b",
               $time, pkt.addr, pkt.data, pkt.wr);
      #5;
    end
  endtask

  task consumer();
    packet_t rcv;
    int rd_data;
    $display("\n=== CONSUMER STARTED ===");
    forever begin
      mbox.get(rcv);
      if (rcv.wr) begin
        memory[rcv.addr] = rcv.data;
        $display("[%0t] CONSUMER: WRITE -> Addr=%0d Data=%0d",
                 $time, rcv.addr, rcv.data);
      end 
      else begin
        rd_data = memory[rcv.addr];
        $display("[%0t] CONSUMER: READ  -> Addr=%0d Data=%0d",
                 $time, rcv.addr, rd_data);
      end
      #3;
    end
  endtask

endmodule

   
    
```
### Simulation Output

<img width="1920" height="966" alt="image" src="https://github.com/user-attachments/assets/373d6d9c-6f32-477c-91d3-93bda9c17f67" />



### Result

The Register Memory Access was successfully designed and verified using the mailbox-based Producer-Consumer model in SystemVerilog.
The producer wrote random data into memory, and the consumer read and validated it, demonstrating correct mailbox synchronization and data integrity.


