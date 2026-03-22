# EXPT.NO-7-IMPLEMENTATION-OF-GO-BACK-N-PROTOCOL-SLIDING-WINDOW
# AIM
To write and execute a program for Go-Back-N protocol.
# EQUIPMENTS REQUIRED
Personal Computer Turbo C Compiler
# PROCEDURE
1.	Connect two computers in Wired/Wireless LAN.
2.	Make sure that two computers are in one network and could able to ping each other.
3.	In the codeblocker open new c file and type the program.
4.	In the menu choose->Project->Properties->Project Build options->Linker settings->Add netproto and pthread.
5.	Execute the program in both server and client.
6.	Enter the IP address of the remote machine, port address of both local & remote machine and error rate.
7.	Choose the file and verify the go back protocol operation.

# PROGRAM
```
#include <stdio.h>
/* Assume 7 frames of data are to sent using GO BACK N ARQW*/ #define window_size 4
void main()
{
int i,window_start = 1,ack; int n;
printf("SLIDIDNG WINDOW PROTOCOL\n");
char frame[n+1][10]; scanf("%d",&n);
printf("GO BACK N ARQ\n"); printf("Enter the no of frames:%d\n",n); for(i=1;i<=n;i++)
{
printf("Content for frame %d :",i); scanf("%s",frame[i]);
}
while(window_start<=n)
{
printf("\nSending frames:\n"); scanf("%d",&ack);
printf("Enter frame number with no acks :%d",ack); if(ack == 0)
{
printf("Enter frame number with no ACK forward\n"); window_start += window_size;
 
}
else
{
printf("No Acknowlegement for frame %d... \n",ack); printf("Resending frames starting from frame %d\n",ack); window_start = ack;
}
}
printf("\n All frames sent successfully.\n");
}
```
# OUTPUT
<img width="1920" height="1080" alt="212222060192_SW" src="https://github.com/user-attachments/assets/ae997499-a752-4cba-bbbd-cd90aa30671e" />


 




# RESULT: 
Thus the Go-Back-N protocol-Sliding Window was implemented and the output is verified successfully.
