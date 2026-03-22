# Sequence-Detector
Aim
To design and simulate a sequence detector using both Moore and Mealy state machine models in Verilog HDL, and verify their functionality through a testbench using the Vivado 2023.1 simulation environment. The objective is to detect a specific sequence of bits (e.g., 1011) and compare the Moore and Mealy designs.

Apparatus Required
Vivado 2023.1 or equivalent Verilog simulation tool.
Computer system with a suitable operating system.
Procedure
Launch Vivado 2023.1:

Open Vivado and create a new project.
Write the Verilog Code for Sequence Detector (Moore and Mealy FSM):

Design two Verilog modules: one for a Moore FSM and another for a Mealy FSM to detect a sequence such as 1011.
Create the Testbench:

Write a testbench to apply input sequences and verify the output of both FSM designs.
Add the Verilog Files:

Add the Verilog code for both FSMs and the testbench to the Vivado project.
Run Simulation:

Run the simulation and observe the output to check if the sequence is detected correctly.
Observe the Waveforms:

Analyze the waveform to ensure both the Moore and Mealy machines detect the sequence as expected.
Save and Document Results:

Capture the waveforms and include the results in the final report.

Verilog Code for Sequence Detector Using Moore FSM
    
    // moore_sequence_detector.v
    module moore_sequence_detector (
        input wire clk,
        input wire reset,
        input wire seq_in,
        output reg detected
    );
    typedef enum reg [2:0] {
        S0, S1, S2, S3, S4  // States for detecting 1011
    } state_t;
    
    state_t current_state, next_state;
    
    // State transition logic
    always @(posedge clk or posedge reset) begin
        if (reset)
            current_state <= S0;
        else
            current_state <= next_state;
    end

    // Next state and output logic
    always @(*) begin
        case (current_state)
            S0: begin
                if (seq_in) next_state = S1;
                else next_state = S0;
                detected = 0;
            end
            S1: begin
                if (seq_in) next_state = S1;
                else next_state = S2;
                detected = 0;
            end
            S2: begin
                if (seq_in) next_state = S3;
                else next_state = S0;
                detected = 0;
            end
            S3: begin
                if (seq_in) next_state = S4;
                else next_state = S2;
                detected = 0;
            end
            S4: begin
                if (seq_in) next_state = S1;
                else next_state = S0;
                detected = 1;  // Sequence 1011 detected
            end
            default: next_state = S0;
        endcase
    end
    endmodule

OUTPUT: 
![1](https://github.com/user-attachments/assets/80f6f359-2584-4ac0-8e03-ce23278cbc9b)

Verilog Code for Sequence Detector Using Mealy FSM

    // mealy_sequence_detector.v
    module mealy_sequence_detector (
        input wire clk,
        input wire reset,
        input wire seq_in,
        output reg detected
    );
    typedef enum reg [2:0] {
        S0, S1, S2, S3  // States for detecting 1011
    } state_t;

    state_t current_state, next_state;

    // State transition logic
    always @(posedge clk or posedge reset) begin
        if (reset)
            current_state <= S0;
        else
            current_state <= next_state;
    end

    // Next state and output logic
    always @(*) begin
        detected = 0;
        case (current_state)
            S0: begin
                if (seq_in) next_state = S1;
                else next_state = S0;
            end
            S1: begin
                if (seq_in) next_state = S1;
                else next_state = S2;
            end
            S2: begin
                if (seq_in) next_state = S3;
                else next_state = S0;
            end
            S3: begin
                if (seq_in) begin
                    next_state = S1;
                    detected = 1;  // Sequence 1011 detected
                end else
                    next_state = S2;
            end
            default: next_state = S0;
        endcase
    end
    endmodule

OUTPUT:
![2](https://github.com/user-attachments/assets/df07055f-bcea-4f39-a6c7-53de20eaa55b)

Testbench for Sequence Detector (Moore and Mealy FSMs)

// sequence_detector_tb.v
`timescale 1ns / 1ps

    module sequence_detector_tb;
        // Inputs
        reg clk;
        reg reset;
        reg seq_in;
        
        // Outputs
        wire moore_detected;
        wire mealy_detected;
        
        // Instantiate the Moore FSM
        moore_sequence_detector moore_fsm (
            .clk(clk),
            .reset(reset),
            .seq_in(seq_in),
            .detected(moore_detected)
        );

    // Instantiate the Mealy FSM
    mealy_sequence_detector mealy_fsm (
        .clk(clk),
        .reset(reset),
        .seq_in(seq_in),
        .detected(mealy_detected)
    );

    // Clock generation
    always #5 clk = ~clk;  // Clock with 10 ns period

    // Test sequence
    initial begin
        // Initialize inputs
        clk = 0;
        reset = 1;
        seq_in = 0;

        // Release reset after 20 ns
        #20 reset = 0;

        // Apply sequence: 1011
        #10 seq_in = 1;
        #10 seq_in = 0;
        #10 seq_in = 1;
        #10 seq_in = 1;

        // Stop the simulation
        #30 $stop;
    end

    // Monitor the outputs
    initial begin
        $monitor("Time=%0t | seq_in=%b | Moore FSM Detected=%b | Mealy FSM Detected=%b",
                 $time, seq_in, moore_detected, mealy_detected);
    end
    endmodule

OUTPUT:
![3](https://github.com/user-attachments/assets/a1fa5e06-d6fa-487e-84d1-93db425f3332)
![4](https://github.com/user-attachments/assets/c0cbae14-c34d-42a7-9af4-c5cf4358232f)

Conclusion
In this experiment, Moore and Mealy FSMs were successfully designed and simulated to detect the sequence 1011. Both designs worked as expected, with the main difference being that the Moore FSM generated the output based on the current state, while the Mealy FSM generated the output based on both the current state and input. The testbench verified the functionality of both FSMs, demonstrating that the Verilog HDL can effectively model both types of state machines for sequence detection tasks.
