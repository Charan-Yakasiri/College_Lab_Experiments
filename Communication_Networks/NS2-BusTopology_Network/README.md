# EXPT.NO 4 SIMULATION OF BUS TOPOLOGY NETWORK
# AIM

To create and monitor Bus Topology and effective data transmission using NS2 Software.

# APPARATUS REQUIRED

PC System with Linux OS, NS2 software.

# ALGORITHM
```
STEP 1: Start the program.
STEP 2: Declare the global variables ns for creating a new simulator.
STEP 3: Open the network animator file in the write mode.
STEP 4: Open the trace file in the write mode.
STEP 5: Transfer the packets in network.
STEP 6: Create the capable no of nodes.
STEP 7: Create the duplex-link between the nodes including the delay time, bandwidth and dropping queue mechanism.
STEP 8: Set a tcp connection for source node.
STEP 9: Set the destination node using tcp sink.
STEP 10: Set the window size and the packet size for the tcp.
STEP 11: Set up the ftp over the tcp connection.
STEP 12: Create the traffic generator CBR for the source and destination files.
STEP 13: Define the plot window and finish procedure.
STEP 14: In the definition of the finish procedure declare the global variables. STEP 15: Close the trace file and namefile and execute the network animation file. STEP 16: At the particular time call the finish procedure.
STEP 17: Stop the program.
```
# PROGRAM:
```

#Create a simulator object set ns [new Simulator] #Open the nam trace file set nf [open out.nam w]
$ns namtrace-all $nf #Define a 'finish' procedure proc finish {}
{
global ns nf
$ns flush-trace close $nf
#Execute nam on the trace file exec nam out.nam &
exit 0
}
#Create five nodes set n0 [$ns node] set n1 [$ns node] set n2 [$ns node] set n3 [$ns node] set n4 [$ns node]
#Create Lan between the nodes
set lan0 [$ns newLan "$n0 $n1 $n2 $n3 $n4" 0.5Mb 40ms LL Queue/DropTail MAC/Csma/Cd Channel] #Create a TCP agent and attach it to node n0
set tcp0 [new Agent/TCP]
$tcp0 set class_ 1
$ns attach-agent $n1 $tcp0
#Create a TCP Sink agent (a traffic sink) for TCP and attach it to node n3 set sink0 [new Agent/TCPSink]
$ns attach-agent $n3 $sink0
#Connect the traffic sources with the traffic sink
$ns connect $tcp0 $sink0
# Create a CBR traffic source and attach it to tcp0 set cbr0 [new Application/Traffic/CBR]
$cbr0 set packetSize_ 500
$cbr0 set interval_ 0.01
$cbr0 attach-agent $tcp0
#Schedule events for the CBR agents
$ns at 0.5 "$cbr0 start"
$ns at 4.5 "$cbr0 stop"
#Call the finish procedure after 5 seconds of simulation time
$ns at 5.0 "finish"
$ns run
 ```
# OUTPUT
![WhatsApp Image 2025-09-03 at 12 28 55 PM (1)](https://github.com/user-attachments/assets/98fc6529-9d39-480f-83c1-ee79fdfad75f)



# RESULT

Thus the Bus Topology using NS2 software is created and monitored successfully.
