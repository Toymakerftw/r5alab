### Fcfs c



#include<stdio.h>
 
 int main()
 
{
    int n,bt[20],wt[20],ta[20],avgwt=0,avgta=0,i,j,twt=0;
    char a;
    printf("enter  no.of processes:");
    scanf("%d",&n);
     
    printf("Enter Process Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("Process[%d]:",i+1);
        scanf("%d",&bt[i]);
    }
 
    wt[0]=0;
    for(i=1;i<n;i++)
    {
      wt[i]=wt[i-1]+bt[i-1];
    }
 
    printf("\nProcess\t\tBurst Time\tWaiting Time\tTurnaround Time:");
 
    for(i=0;i<n;i++)
    {
        ta[i]=bt[i]+wt[i];
        avgwt=avgwt+wt[i];
        avgta=avgta+ta[i];
        printf("\nProcess[%d]\t\t%d\t\t%d\t\t%d",i+1,bt[i],wt[i],ta[i]);
    }
     printf("\n\nGantt Chart\n\n"" ");
     for(i=0;i<n;i++)
    {
        printf("Process[%d]_",i+1);
        
    }
         printf("\n");
    

    for(i=0;i<n;i++)
    {
        twt=twt+bt[i];
        printf("%d__________",wt[i]);
        
    }printf("%d",twt);
    avgwt=avgwt/i;
    avgta=avgta/i;
    printf("\n\nAverage Waiting Time:%d",avgwt);
    printf("\nAverage Turnaround Time:%d\n",avgta);


 
    return 0;
}

#### sjf

#include<stdio.h>
#include<string.h>
void main()
{
int n,i,bt[10],wt=0,tt=0,temp,j,a[10];
float tb=0,tw=0;
char process[10][10],ta[10];
printf("Enter the no of process: ");
scanf("%d",&n);
for(i=0;i<n;i++)
{
printf("enter process name: ");
scanf("%s",process[i]);
printf("Enter the cpu time: ");
scanf("%d",&bt[i]);
}
for(i=0;i<n;i++)
{
for(j=i;j<n-i-1;j++)
{
if(bt[j]>bt[j+1])
{
temp=bt[j];
bt[j]=bt[j+1];
bt[j+1]=temp;
strcpy(ta,process[j]);
strcpy(process[j],process[j+1]);
strcpy(process[j+1],ta);
}
}
}

printf("\nProcess name\tburstTime\twaitingtime\tTurnaroundTime\n");
for(i=0;i<n;i++)
{
wt=tt;
a[i]=wt;
tt=tt+bt[i];
printf("%s\t\t%d\t\t%d\t\t%d\n",process[i],bt[i],wt,tt);
tw=tw+wt;
tb=tb+tt;
}
printf("\n\nGantt Chart\n\n"" ");
     for(i=0;i<n;i++)
    {
        printf(" %s  ",process[i]);
        
    }
         printf("\n");
    

    for(i=0;i<n;i++)
    {
        
        printf("%d   ",a[i]);
        
    }printf("%d",tt);

printf("\naverage waiting time=%f\n",(tw/n));
printf("\nAverage turn around time=%f\n",(tb/n));

}

## Priority

#include<stdio.h>
#include<string.h>
void main()
{
	int n,i,bt[10],wt=0,tt=0,temp,j,a[10],p[10];
	float tb=0,tw=0;
	char process[10][10],ta[10];
	printf("ENTER THE NUMBER OF PROCESS: " );
	scanf("%d",&n);
	for(i=0;i<n;i++)
		{
			printf("ENTER PROCESS NAME: ");
			scanf("%s",process[i]);
			rintf("ENTER THE CPU TIME: " );
			scanf("%d",&bt[i]);
			printf("ENTER THE PRIORITY: " );
			scanf("%d",&p[i]);
		}
			for(i=0;i<n;i++)
		{	
  			for(j=i;j<n;j++)
		{
 			if(p[i]>p[j])
	{
 		temp=p[i];
 		p[i]=p[j];
 		p[j]=temp;
 		strcpy(ta,process[j]);
 		strcpy(process[j],process[i]);
 		strcpy(process[i],ta);
 		temp=bt[i];
 		bt[i]=bt[j];
 		bt[j]=temp;
	}	
		}
		}
printf("\nProcess name\tburst time\t priority\twaitingtime\tTurnaroundtime\n");
for(i=0;i<n;i++)
	{
		wt=tt;
		a[i]=wt;
		tt=tt+bt[i];
		printf("%s\t\t%d\t\t%d\t\t%d\t\t%d\n",process[i],bt[i],p[i],wt,tt);
		tw=tw+wt;
		tb=tb+tt;
	}
printf("\n\nGantt Chart\n\n"" ");
for(i=0;i<n;i++)
	{
 		printf(" %s   ",process[i]);
	}
  printf("\n\n");
  for(i=0;i<n;i++)
	{
   		printf("%d   ",a[i]);
	                                                                                                                                                                                }	
printf("%d",tt);
printf("\naverage waiting time=%f\n",(tw/n));
printf("\nAvERAGE TURN AROUND TIME=%f\n",(tb/n));
}

### Round robin



    Register
    Log in

#include<stdio.h>
int main(){

	int num_pr, i, j, temp, sq = 0, swap_var;
	int quantum_time, count = 0;
	int burst_time[32], wait_time[32], process[32];
	int turn_around_time[32], rem_burst_time[32];
	float avg_wt = 0, avg_tat = 0;
	int g_process[32], g_turn_around_time[32];

	printf("Enter Number of process : ");
	scanf("%d", &num_pr);

	for (i = 0; i < num_pr; ++i){
	
		printf("Burst Time for Process %d : ", i+1);
		scanf("%d", &burst_time[i]);
		printf("\n");
		rem_burst_time[i] = burst_time[i];
		process[i] = i+1;
	}

	printf("Enter Quantum Time : ");
	scanf("%d", &quantum_time);

	while(1 == 1){
	for(i=0, count=0; i<num_pr; i++){
		
			temp = quantum_time;
			if (rem_burst_time[i] == 0){
				count++;
				continue;
			}

			if (rem_burst_time[i] > quantum_time)
				rem_burst_time[i] = rem_burst_time[i] - quantum_time;
			else
				if(rem_burst_time[i] >= 0){
					temp = rem_burst_time[i];
					rem_burst_time[i] = 0;
				}
				sq = sq + temp;
				turn_around_time[i] = sq;
				g_turn_around_time[i] = turn_around_time[i];
				g_process[i] = process[i];
		}

		if (num_pr == count)
			break;
	}

	printf("\nProcess | Burst Time | Waiting Time | Turn Around Time\n"); 


	for(i=0; i<num_pr; i++){
		
		wait_time[i] = turn_around_time[i] - burst_time[i];
		avg_wt += wait_time[i];
		avg_tat += turn_around_time[i];
		printf("\n%d\t\t%d\t\t%d\t\t%d", i+1, burst_time[i], wait_time[i], turn_around_time[i]);

	}


	printf("\n");

	avg_wt /= num_pr;
	avg_tat /= num_pr;

	printf("\nAverage Waiting Time = %0.4f", avg_wt); 
	printf("\n"); 
	printf("Average Turn Around Time = %0.4f \n", avg_tat);


	printf("\nGantt Chart\n");

	for (i = 0; i < num_pr; ++i)
		printf("___P%d___", g_process[i]);
	printf("\n");

	for (i = 0; i < num_pr+1; ++i)
		printf("|\t");

	printf("\n0\t");

	for (i = 0; i < num_pr; ++i)
		printf(" %d \t", g_turn_around_time[i]);

	printf("\n");
	printf("\n");


	return 0;
}


## Disk Fcfs

#include<stdio.h>
void main()
{
	int n,i,j,reqQ[50],sum=0,h;
	printf("Enter the length::");
	scanf("%d",&n);
	printf("Enter the head value::");
	scanf("%d",&h);
	printf("Enter the request queue::");
	for(i=1;i<=n;i++)
	{
	   scanf("%d",&reqQ[i]);
	}
	reqQ[0]=h;
	for(j=0;j<n;j++)
	{
	  if(reqQ[j]>reqQ[j+1])
         	  {
	         	sum=sum+(reqQ[j]-reqQ[j+1]);
	          }
	  else
		  {
			sum=sum+(reqQ[j+1]-reqQ[j]);
		  }
	}
	printf("Total Head Movements are %d\n",sum);
}

## scan

include<stdio.h>
#include<stdlib.h>
int main()
{
    int RQ[100],i,j,n,THM=0,initial,size,move;
    printf("Enter the number of Requests\n");
    scanf("%d",&n);
    printf("Enter the Requests sequence\n");
    for(i=0;i<n;i++)
     scanf("%d",&RQ[i]);
    printf("Enter initial head position\n");
    scanf("%d",&initial);
    printf("Enter total disk size\n");
    scanf("%d",&size);
    printf("Enter the head movement direction for high 1 and for low 0\n");
    scanf("%d",&move);
    
   
    for(i=0;i<n;i++)
    {
        for(j=0;j<n-i-1;j++)
        {
            if(RQ[j]>RQ[j+1])
            {
                int temp;
                temp=RQ[j];
                RQ[j]=RQ[j+1];
                RQ[j+1]=temp;
            }

        }
    }

    int index;
    for(i=0;i<n;i++)
    {
        if(initial<RQ[i])
        {
            index=i;
            break;
        }
    }
   
    
    if(move==1)
    {
        for(i=index;i<n;i++)
        {
            THM=THM+abs(RQ[i]-initial);
            initial=RQ[i];
        }
        
        THM=THM+abs(size-RQ[i-1]-1);
        initial = size-1;
        for(i=index-1;i>=0;i--)
        {
             THM=THM+abs(RQ[i]-initial);
             initial=RQ[i];
            
        }
    }
    
    else
    {
        for(i=index-1;i>=0;i--)
        {
            THM=THM+abs(RQ[i]-initial);
            initial=RQ[i];
        }
        
        THM=THM+abs(RQ[i+1]-0);
        initial =0;
        for(i=index;i<n;i++)
        {
             THM=THM+abs(RQ[i]-initial);
             initial=RQ[i];
            
        }
    }
    
    printf("Total head movement is %d",THM);
    int avg=THM/n;
    printf("\nAverage Total head movement is %d\n\n",avg);
   
}


### C scan

#include<stdio.h>
#include<stdlib.h>
int main()
{
    int RQ[100],i,j,n,THM=0,initial,size,move;
    printf("Enter the number of Requests\n");
    scanf("%d",&n);
    printf("Enter the Requests sequence\n");
    for(i=0;i<n;i++)
     scanf("%d",&RQ[i]);
    printf("Enter initial head position\n");
    scanf("%d",&initial);
    printf("Enter total disk size\n");
    scanf("%d",&size);
    printf("Enter the head movement direction for high 1 and for low 0\n");
    scanf("%d",&move);
    
   
    for(i=0;i<n;i++)
    {
        for( j=0;j<n-i-1;j++)
        {
            if(RQ[j]>RQ[j+1])
            {
                int temp;
                temp=RQ[j];
                RQ[j]=RQ[j+1];
                RQ[j+1]=temp;
            }

        }
    }

    int index;
    for(i=0;i<n;i++)
    {
        if(initial<RQ[i])
        {
            index=i;
            break;
        }
    }
   
    
    if(move==1)
    {
        for(i=index;i<n;i++)
        {
            THM=THM+abs(RQ[i]-initial);
            initial=RQ[i];
        }
       
        THM=THM+abs(size-RQ[i-1]-1);
       
        THM=THM+abs(size-1-0);
        initial=0;
        for( i=0;i<index;i++)
        {
             THM=THM+abs(RQ[i]-initial);
             initial=RQ[i];
            
        }
    }
    
    else
    {
        for(i=index-1;i>=0;i--)
        {
            THM=THM+abs(RQ[i]-initial);
            initial=RQ[i];
        }
       
        THM=THM+abs(RQ[i+1]-0);
        
        

	THM=THM+abs(size-1-0);
        initial =size-1;
        for(i=n-1;i>=index;i--)
        {
             THM=THM+abs(RQ[i]-initial);
             initial=RQ[i];
            
        }
    }
    
    printf("Total head movement is %d",THM);
    int avg=THM/n;
    printf("\nAverage Total head movement is %d\n\n",avg);
}

# Bankers

#include<stdio.h>
#include<conio.h>
int max[100][100];
int alloc[100][100];
int need[100][100];
int avail[100];
int n,r;
void input();
void show();
void cal();
int main()
{
int i,j;
printf("**** Banker's Algo ****\n");
input();
show();
cal();
getch();
return 0;
}
void input()
{
int i,j;
printf("Enter the no of Processes\t");
scanf("%d",&n);
printf("Enter the no of resources instances\t");
scanf("%d",&r);
printf("Enter the Max Matrix\n");
for(i=0;i<n;i++)
{
for(j=0;j<r;j++)
{
scanf("%d",&max[i][j]);
}
}
printf("Enter the Allocation Matrix\n");
for(i=0;i<n;i++)
{
for(j=0;j<r;j++)
{
scanf("%d",&alloc[i][j]);
}
}
printf("Enter the available Resources\n");
for(j=0;j<r;j++)
{
scanf("%d",&avail[j]);
}
}
void show()
{
int i,j;
printf("Process\t Allocation\t Max\t Available\t");
for(i=0;i<n;i++)
{
printf("\nP%d\t ",i+1);
for(j=0;j<r;j++)
{
printf("%d ",alloc[i][j]);
}
printf("\t");
for(j=0;j<r;j++)
{
printf("%d ",max[i][j]);
}
printf("\t");
if(i==0)
{
for(j=0;j<r;j++)
printf("%d ",avail[j]);
}
}
}
void cal()
{
int finish[100],temp,need[100][100],flag=1,k,c1=0;
int safe[100];
int i,j;
for(i=0;i<n;i++)
{
finish[i]=0;
}
//find need matrix
for(i=0;i<n;i++)
{
for(j=0;j<r;j++)
{
need[i][j]=max[i][j]-alloc[i][j];
}
}
printf("\n");
while(flag)
{
flag=0;
for(i=0;i<n;i++)
{
int c=0;
for(j=0;j<r;j++)
{
if((finish[i]==0)&&(need[i][j]<=avail[j]))
{
c++;
if(c==r)
{
for(k=0;k<r;k++)
{
avail[k]+=alloc[i][j];
finish[i]=1;
flag=1;
}
printf("P%d->",i);
if(finish[i]==1)
{
i=n;
}
}
}
}
}
}
for(i=0;i<n;i++)
{
if(finish[i]==1)
{
c1++;
}
else
{
printf("P%d->",i);
}
}
if(c1==n)
{
printf("\n The system is in safe state");
}
else
{
printf("\n Process are in dead lock");
printf("\n System is in unsafe state");
}
}



########### MASM
### Factorial masm


ASSUME DS: DATA, CS: CODE

DATA SEGMENT

F DW 00

DATA ENDS

CODE SEGMENT

START: MOV AH,00

MOV AL, 05

MOV CX, AX

L1:

DEC CX

MUL CL

CMP CX, 01

JNZ L1 MOV F, AX

MOV AH, 4CH

INT 21H

CODE ENDS

END START


### Fibonacci

ASSUME CS:CODE, DS: DATA DATA SEGMENT

F DB 10 DUP (0) COUNT DB 07

DATA ENDS

CODE SEGMENT

START:

MOV AX, DATA

MOV DS, AX LEA BX, F

MOV CL, COUNT

MOV AX, 0001

DEC CL

L1: ADD AL, BYTE PTR [BX]

MOV DL, BYTE PTR [BX] INC BX

MOV BYTE PTR [BX],

MOV

AL, DL

DEC CL

CMP CL, 00

JNZ L1

MOV AH, 4CH

INT

21H

AL

CODE ENDS

END START



## COUNT OF EVEN AND ODD

ASSUME CS:CODE, DS: DATA

DATA SEGMENT

NUM DB 01H, 02H, 03H, 04H, 05H, 06H, 07H, 08H, OAH, OCH

EVN DB 00H

ODD DB 00H

COUNT DB OAH

DATA ENDS

CODE SEGMENT

START:

MOV AX, DATA

MOV DS, AX

XOR CH, CH

MOV CL, COUNT

LEA SI, NUM

MOV BL, 02 MOV AH,00H

MOV AL, [SI]

DIV BL

CMP AH, 00H

JZ TOEVEN

ADD ODD, 01H

JMP NEXT

TOEVEN: ADD EVN, 01H

NEXT: INC SI DEC CX

JNZ NEXT MOV AH, 4CH

INT 21H

CODE ENDS

END START


#### FIND SMALLEST USING AN ARRAY


ASSUME CS: CODE DS: DATA DATA SEGMENT

STRING1 DB 08H, 14H, 05H, OFH, 09H

RES DB ?

DATA ENDS

CODE SEGMENT

START: MOV AX, DATA

MOV DS, AX

MOV CX, 04H MOV BL, 79H

LEA SI, STRING1 : MOV AL, [SI]

UP CMP AL, BL

JGE NXT MOV BL, AL

NXT : INC SI

DEC CX

JNZ UP MOV RES, BL

MOV AH, 4CH INT 21H

CODE ENDS

END START


### character reading


ASSUME CS:CODE, DS: DATA DATA SEGMENT

MSG1 DB ODH, OAH, "ENTER A CHARACTER:$"

MSG2 DB ODH, OAH, "ENTERED CHARACTER IS:$"

DATA ENDS

CODE SEGMENT

MOV AX, DATA

START:

MOV DS, AX

LEA DX, MSG1

MOV AH,09H

INT 21H

MOV AH, 01H

INT 21H

LEA DX, MSG2 MOV AH,09H

INT 21H

MOV DL, AL

MOV AH,02H

INT 21H MOV AH, 4CH

INT 21H

CODE ENDS

END START

### Average of N Number

ASSUME CS:CODE, DS: DATA

DATA SEGMENT A DB 1,2,3, 4, 5, 6, 7, 8, 9, 10

SUM DB OH AVG DW 00H

DATA ENDS

CODE SEGMENT

START:

MOV AX, DATA

MOV DS, AX

LEA BX, A

MOV CL, OAH

MOV AX, 0000 L1:ADD AL, BYTE PTR [BX]

INC BX

DEC CL

CMP CL, 00

JNZ L1

MOV SUM, AL

MOV BL, 10

DIV BL

MOV

AVG, AX MOV AH, 4CH

INT 21H

CODE ENDS 
END START

### String reading and display


ASSUME CS:CODE, DS: DATA DATA SEGMENT

MSG2 DB "ENTER A STRING"

MSG DB 80 DUP ("S") MSG1 DB OAH, '$'

DATA ENDS CODE SEGMENT

MOV AX, DATA

START:

MOV DS, AX

MOV AH,09H

LEA DX, MSG2

INT 21H

LEA DX, MSG

MOV AH, OAН

INT 21H

MOV AH,09H

LEA DX, MSG1

INT 21H

MOV AH,09H

LEA DX, MSG+2 
INT 21H

MOV AH, 4CH

INT 21H 
CODE ENDS

END START

#### Array search
DATA SEGMENT
STRING1 DB 11H,22H,33H,44H,55H
MSG1 DB "FOUND$"
MSG2 DB "NOT FOUND$"
SE DB 33H
DATA ENDS
 
PRINT MACRO MSG
MOV AH, 09H
LEA DX, MSG
INT 21H
INT 3
ENDM
 
CODE SEGMENT
ASSUME CS:CODE, DS:DATA
START:
MOV AX, DATA
MOV DS, AX
MOV AL, SE
LEA SI, STRING1
MOV CX, 04H
 
UP:
MOV BL,[SI]
CMP AL, BL
JZ FO
INC SI
DEC CX
JNZ UP
PRINT MSG2
JMP END1
 
FO:
PRINT MSG1
 
END1:
INT 3
CODE ENDS
END START

# Pass one

#include<stdio.h> 
#include<conio.h>
#include<stdlib.h> 
#include<string.h> 
void main()
{
FILE *f1, *f2, *f3, *f4, *f5; int LOCCTR, SA, o, x, size;
char L[20], OP[20], O[20], OPT[20], SYM[20];
f1=fopen("input.txt", "r");
f5=fopen("symtab.txt", "w");
f3=fopen("intermediate.txt", "w");
fscanf(f1, "%s %s %d", L, OP, &o);
if(strcmp(OP, "START")==0)
{
SA=o;
LOCCTR=SA;
fprintf(f3, "%s %s %d\n", L, OP, o);
}
else LOCCTR=0;
fscanf(f1, "%s%s", L, OP); while(!feof(f1))
{
fscanf(f1, "%s", O);
fprintf(f3, "%d %s %s %s \n", LOCCTR, L, OP, O); if(strcmp(L, "-")!=0 && strcmp(L, "START")!=0)
{
fprintf(f5, "%d %s\n", LOCCTR, L);
}
f2=fopen("optab.txt", "r");
fscanf(f2, "%s %d", OPT, &o); while(!feof(f2))
{
if(strcmp(OP, OPT)==0)
{
LOCCTR+=3;
size=3; break;
}
else if(OP[0]=='+')
{
LOCCTR+=4;
size=4; break;

}
fscanf(f2, "%s %d", OPT, &o);
}
fclose(f2);
if(strcmp(OP, "WORD")==0)
{
LOCCTR+=3;
}
else if(strcmp(OP, "RESW")==0)
{
x=atoi(O);
LOCCTR+=(3*x);
}
else if(strcmp(OP, "RESB")==0)
{
x=atoi(O);
LOCCTR+=x;
}
else if(strcmp(OP, "BYTE")==0)
{
if(O[0]=='X')
{
LOCCTR+=1;
}
else
{
x=strlen(O)-2;
LOCCTR+=x;
}
}
fscanf(f1, "%s %s", L, OP);
}
if(strcmp(OP, "END")==0)
{
f4=fopen("length.txt", "w"); x=LOCCTR-SA;
fprintf(f4, "%d", x);
}
fclose(f1); fclose(f2); fclose(f3); fclose(f4);
}

