# EXPT.NO.8-IMPLEMENTATION-OF-GO-BACK-N-PROTOCOL-SELECTIVE-REPEAT
# AIM:
To write and execute a program for Go-Back-N protocol-Selective Repeat.
# EQUIPMENTS REQUIRED:
Personal Computer Turbo C Compiler
# PROCEDURE:
8.	Connect two computers in Wired/Wireless LAN.
9.	Make sure that two computers are in one network and could able to ping each other.
10.	In the codeblocker open new c file and type the program.
11.	In the menu choose->Project->Properties->Project Build options->Linker settings->Add netproto and pthread.
12.	Execute the program in both server and client.
13.	Enter the IP address of the remote machine, port address of both local & remote machine and error rate.
14.	Choose the file and verify the go back protocol operation.

# PROGRAM:
```
#include<stdio.h> void main()
{

int i,j,n;
printf("GO BACK N ARQ\n");
//printf("Entermessage in format\n"); printf("Enter number of frame : "); scanf("%d",&n);
char frame[n][10];

for(i=1;i<=n;i++)
{
printf("Content for frame %d :",i); scanf("%s",&frame[i]);
}
int s=1;
//while(j<=n){
printf("Enter frame number with no ACK :"); scanf("%d",&j);
for(i=1;i<=n;i++)
{
if(i!=j)
printf("\n Sending frame %d \n FRAME ACKNOWLEDGED.	\n",i);
//else
//printf("\n Frame not Acknowledeged.	\n");
 
}
if(j<=n)
{
printf("No Acknowlegement for frame %d... \n",j); printf("Resending... Content from frame %d :%s\n\n",j,frame[j]);

}
printf("\n Sending frame %d \n FRAME ACKNOWLEDGED.	\n",j);
//}

printf("\n\nALL FRAME RECIEVED SUCCESSFULLY\n\n");
}
```
OUTPUT:
![cn2](https://github.com/user-attachments/assets/8e6dcf6d-4cc2-48d2-9de1-96fbef91dc52)

---
# RESULT:
Thus the Go-Back-N protocol- Selective Repeat was implemented and the output is verified successfully.
