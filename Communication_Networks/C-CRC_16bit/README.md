# EXPT.NO.09-IMPLEMENTATION-OF-ERROR-DETECTION-USING-CRC-CCITT-16-BIT-TECHNIQUE
# AIM:
To write a program for error Detection using Cyclic Redundancy Check (CRC-16 bit) technique.

# EQUIPMENTS REQUIRED:
1.	Personal Computer
2.	C++ compiler

# ALGORITHM:
```
1] Open code blocks application and create a new file. 2] After creating the file type the codes.
3] After typing the codes save the file using the .c extension in the desired location. 4] Run the program using build and run.
5] Give polynomial values and the generated polynomial is obtained, and by other means arraive	at the desired output which uses the error detection technique. 6] Thus the output polynomial is obtained through this technique.
```
# PROGRAM:
```
#include<stdio.h> #include<string.h> #define Nstrlen(g) char t[128],cs[128],g[]="111";
int a,e,c; voidxor()
{
for(c=1;c<N;c++) cs[c]=((cs[c]==g[c])?'0':'1');
}
void crc()
{
for(e=0;e<N;e++) cs[e]=t[e];
do
{
if(cs[0]=='1')
xor();
for(c=0;c<N-1;c++) cs[c]=cs[c+1];
 
cs[c]=t[e++];
}
while(e<=a+N-1);
}
void main()
{
printf("\n Enter poly:"); scanf("%s",t);
printf("\nGen poly is : %s",g); a=strlen(t);
for(e=a;e<a+N-1;e++) t[e]='0';
printf("\nModfied t[u] :%s",t); crc();
printf("\nChecksum is:%s",cs); for(e=a;e<a+N-1;e++) t[e]=cs[e-a];
printf("\nFinal code word is:%s",t); printf("\nTest error detection 0(yes) 1(no)?:"); scanf("%d",&e);
if(e==0)
{
printf("Enter position where is to inserted"); scanf("%d",&e);
t[e]=(t[e]=='0')?'1':'0';
printf("erroneous data :%s\n",t);
}
crc();
for(e=0;(e<N-1)&&(cs[e]!='1');e++) if(e<N-1)
printf("Error detected"); else
printf("no error detected");
}
 ```
# OUTPUT:
<img width="1920" height="1080" alt="212222060192_CRC" src="https://github.com/user-attachments/assets/eed36d7d-abc3-4788-853d-a177325d7c5a" />



# RESULT:
Thus the error detection using CRC-CCITT[16 bit] technique is implemented and the output is obtained and verified successfully.
