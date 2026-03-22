# EXPT.NO.10-IMPLEMENTATION-OF-ENCRYPTION-AND-DECRYPTION
# AIM:
To implement encryption and decryption using C program.

# EQUIPMENTS REQUIRED:

PC with Linux operating system

# PROCEDURE:
```
1] Open code blocks and type the program for encryption and decryption. 2] Save the program using extension .c
3]	Run the program using build and run.
4]	Prime number is given as input. If it is not a prime number then wrong input is displayed. 5] Then a message is entered.
6]	The encrypted form of the message is displayed.
7]	The decrypted form is also displayed as final output. 8] Thus the output is obtained.
```
# PROGRAM:
```
#include<stdio.h> #include<stdlib.h> #include<math.h> #include<string.h>
longintp,q,n,t,flag,e[100],d[100],temp[100],j,m[100],en[100],i; char msg[100];
int prime(longint); void ce();
long int cd(longint); void encrypt();
void decrypt(); void main()
{ printf("\nENTERFIRSTPRIMENUMBER\n");
scanf("%d",&p); flag=prime(p); if(flag=0)
{
printf("\nWRONGINPUT\n"); exit(1);
} printf("\nENTERANOTHERPRIMENUMBER\n");
scanf("%d",&q);
 
flag=prime(q); if(flag==0||p==q)
{
printf("\nWRONGINPUT\n"); exit(1);
}
printf("\nENTERMESSAGE\n"); fflush(stdin);
scanf("%s",msg); for(i=0;msg[i]!=NULL;i++)
m[i]=msg[i]; n=p*q; t=(p-1)*(q-1); ce();
printf("\nPOSSIBLEVALUESOFeANDdARE\n"); for(i=0;i<j-1;i++)
printf("\n%ld\t%ld",e[i],d[i]); encrypt(); decrypt(); }
int prime(long int pr)
{
int i; j=sqrt(pr); for(i=2;i<=j;i++)
{
if(pr%i==0) return0;
}
return1;
}
void ce()
{
int k; k=0;
for(i=2;i<t;i++)
{
if(t%i==0) continue; flag=prime(i);
if(flag==1&&i!=p&&i!=q)
{
e[k]=i; flag=cd(e[k]); if(flag>0)
{
d[k]=flag; k++;
}
if(k==99) break;
 
}
}
}
long int cd(long int x)
{
long int k=1; while(1)
{
k=k+t; if(k%x==0) return(k/x);
}

}
void encrypt()
{
longintpt,ct,key=e[0],k,len; i=0;
len=strlen(msg); while(i!=len)
{
pt=m[i]; pt=pt-96; k=1;
for(j=0;j<key;j++)
{
k=k*pt; k=k%n;
}
temp[i]=k; ct=k+96; en[i]=ct; i++;
}
en[i]=-1; printf("\nTHEENCRYPTEDMESSAGEIS\n");
for(i=0;en[i]!=-1;i++)
printf("%c",en[i]);
}
void decrypt()
{
long int pt,ct,key=d[0],k; i=0;
while(en[i]!=-1)
{
 
ct=temp[i]; k=1;
for(j=0;j<key;j++)
{
k=k*ct; k=k%n;
}
pt=k+96;m[i]=pt; i++;
}
m[i]=-1; printf("\nTHEDECRYPTEDMESSAGEIS\n");
for(i=0;m[i]!=-1; i++
)
printf("%c",m[i]);
}
```
# OUTPUT:
<img width="1920" height="1080" alt="212222060192_E D" src="https://github.com/user-attachments/assets/6bc3352a-7356-4dd0-be36-e8a93315f0df" />

# RESULT:
Thus the encryption and decryption is implemented and the output is obtained and verified successfully.
