# EX.NO: 5 IMPLEMENTATION OF STOP AND WAIT PROTOCOL

# AIM
To implement Stop and Wait protocol using NS2 program.

# EQUIPMENTS REQUIRED
1.	PC with ubuntu operating system
2.	NS2 Software

# ALGORITHM
```
Step 1: Start the program.
Step 2: Declare the global variables ns for creating a new simulator. Step 3: Open the network animator file in the write mode.
Step 4: Open the trace file in the write mode. Step 5: Transfer the packets in network.
Step 6: Create the capable no of nodes.
Step 7: Create the duplex-link between the nodes including the delay time, bandwidth and dropping queue mechanism.
Step 8: Set a tcp connection for source node. Step 9: Set the destination node using tcp sink.
Step 10: Set the window size and the packet size for the tcp. Step 11: Set up the ftp over the tcp connection.
Step 12: Define the plot window and finish procedure.
Step 13: In the definition of the finish procedure declare the global variables. Step 14: Close the trace file and namfile and execute the network animation file. Step 15: At the particular time call the finish procedure.
Step 16: Stop the program.
 ```
# PROGRAM
```
set ns [new Simulator]
set namfile [open out.nam w]
$ns namtrace-all $namfile proc finish {}
{
global ns namfile
$ns flush-trace close $namfile
exec nam out.nam & exit 0
}
set n0 [$ns node] set n1 [$ns node] set n2 [$ns node] set n3 [$ns node]
$ns duplex-link $n0 $n1 2Mb 200ms DropTail
$ns duplex-link $n1 $n2 2Mb 10ms DropTail
$ns duplex-link $n2 $n3 2Mb 10ms DropTail
$ns queue-limit $n0 $n1 15 set tcp [new Agent/TCP]
$tcpset window_ 1
$tcp set maxcwnd_ 1
$ns attach-agent $n0 $tcp
set sink [new Agent/TCPSink] set sink [new Agent/TCPSink]
$ns attach-agent $n1 $sink
$ns connect $tcp $sink
set ftp [new Application/FTP]
$ftp attach-agent $tcp
$ns add-agent-trace $tcp tcp #$ns moniter-agent-trace $tcp
$tcp tracevar cwnd_
$ns at 0.1 "$ftp start"
$ns at 3.0 "$ns detach-agent $n0 $tcp ; $ns detach-agent $n1 $sink"
$ns at 3.5 "finish"
$ns at 0.0 "$ns trace-annotate \"Stop and Wait with normal operation\""
$ns at 0.05 "$ns trace-annotate \"FTP starts at 0.1\""
$ns at 0.11 "$ns trace-annotate \"Send Packet_0\""
$ns at 0.35 "$ns trace-annotate \"Receive Ack_0\""
$ns at 0.56 "$ns trace-annotate \"Send Packet_1\""
$ns at 0.79 "$ns trace-annotate \"Receive Ack_1\""
$ns at 0.99 "$ns trace-annotate \"Send Packet_2\""
$ns at 1.23 "$ns trace-annotate \"Receive Ack_2\""
 
$ns at 1.43 "$ns trace-annotate \"Send Packet_3\""
$ns at 1.67 "$ns trace-annotate \"Receive Ack_3\""
$ns at 1.88 "$ns trace-annotate \"Send Packet_4\""
$ns at 2.11 "$ns trace-annotate \"Receive Ack_4\""
$ns at 2.32 "$ns trace-annotate \"Send Packet_5\""
$ns at 2.55 "$ns trace-annotate \"Receive Ack_5\""
$ns at 2.75 "$ns trace-annotate \"Send Packet_6\""
$ns at 2.99 "$ns trace-annotate \"Receive Ack_6\""
$ns at 3.1 "$ns trace-annotate \"FTP stops\""
$ns at 0.0 "$n0 label Sender"
$ns at 0.0 "$n1 label Receiver"
$ns run
 ```
# OUTPUT
![WhatsApp Image 2025-09-12 at 4 33 09 PM (1)](https://github.com/user-attachments/assets/14347ecd-fe85-4929-ab6e-9d88d39ecf1f)










# RESULT
Thus the Stop and Wait protocol is implemented using NS2 and the output is verified successfully.
