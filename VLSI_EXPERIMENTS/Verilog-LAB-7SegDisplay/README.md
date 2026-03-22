**Seven-segment display using Verilog HDL**

Aim
To design and simulate a seven-segment display driver using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. The objective is to implement the logic that converts a 4-bit binary input into the corresponding 7-segment display output for the digits 0 to 9.

Apparatus Required
Vivado 2023.1
Computer system with a suitable operating system.

Procedure

Launch Vivado 2023.1:

Open Vivado and create a new project.
Design the Verilog Code:

Write the Verilog code for the seven-segment display, defining the logic that maps a 4-bit binary input to the corresponding segments (a to g) of the display.
Create the Testbench:

Write a testbench to simulate the seven-segment display behavior. The testbench should apply various 4-bit input values and monitor the corresponding output on the seven-segment display.
Add the Verilog Files:

Add both the design module and the testbench in the Vivado project.
Run Simulation:

Run the behavioral simulation to verify the output. Ensure the seven-segment display behaves correctly for binary inputs 0000 to 1001 (decimal 0 to 9).
Observe the Waveforms:

Analyze the output waveforms in the simulation window, and verify that the correct segments light up for each digit.
Save and Document Results:

Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

Diagram
![image](https://github.com/user-attachments/assets/d7ecb419-906e-4e3b-9b82-f86ced4f364a)


Verilog Code for Seven-Segment Display

// seven_segment_display.v
module seven_segment_display (

    input wire [3:0] binary_input,
    
    output reg [6:0] seg_output

    );
    always @(*) begin
    
        case (binary_input)
        
            4'b0000: seg_output = 7'b0111111; // 0
            
            4'b0001: seg_output = 7'b0000110; // 1
            
            4'b0010: seg_output = 7'b1011011; // 2
            
            4'b0013: seg_output = 7'b1001111; // 3
            
            4'b0100: seg_output = 7'b1100110; // 4
            
            4'b0101: seg_output = 7'b1101101; // 5
            
            4'b0110: seg_output = 7'b1111101; // 6
            
            4'b0111: seg_output = 7'b0000111; // 7
            
            4'b1000: seg_output = 7'b1111111; // 8
            
            4'b1001: seg_output = 7'b1101111; // 9
            
            default: seg_output = 7'b0000000; // blank or error
        
        endcase
    end
    endmodule

![WhatsApp Image 2024-10-17 at 19 25 26_2739b2ea](https://github.com/user-attachments/assets/c20d9620-6c35-4609-899a-e69fe52152b9)


Testbench for Seven-Segment Display:

// seven_segment_display_tb.v
`timescale 1ns / 1ps

module seven_segment_display_tb;
    // Inputs
    reg [3:0] binary_input;

    // Outputs
    wire [6:0] seg_output;

    // Instantiate the Unit Under Test (UUT)
    seven_segment_display uut (
        .binary_input(binary_input),
        .seg_output(seg_output)
    );

    // Test procedure
    initial begin
        // Initialize inputs
        binary_input = 4'b0000;

        // Apply test cases
        #10 binary_input = 4'b0000; // Display 0
        #10 binary_input = 4'b0001; // Display 1
        #10 binary_input = 4'b0010; // Display 2
        #10 binary_input = 4'b0011; // Display 3
        #10 binary_input = 4'b0100; // Display 4
        #10 binary_input = 4'b0101; // Display 5
        #10 binary_input = 4'b0110; // Display 6
        #10 binary_input = 4'b0111; // Display 7
        #10 binary_input = 4'b1000; // Display 8
        #10 binary_input = 4'b1001; // Display 9
        #10 $stop;
    end

    // Monitor outputs
    initial begin
        $monitor("Time=%0t | binary_input=%b | seg_output=%b", $time, binary_input, seg_output);
    end
endmodule

![WhatsApp Image 2024-10-17 at 19 27 10_f7036226](https://github.com/user-attachments/assets/3446b8ed-fd7b-4a20-b0ec-7637d2d03c41)


Conclusion
In this experiment, a seven-segment display driver was successfully designed and simulated using Verilog HDL. The simulation results confirmed that the display correctly represented the digits 0 to 9 based on the 4-bit binary input. The testbench effectively verified the functionality of the seven-segment display by applying various input combinations and observing the corresponding segment outputs. This experiment highlights how Verilog HDL can be used to control hardware components like a seven-segment display in digital systems.
