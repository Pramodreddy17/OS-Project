//Ques. 10. Design a scheduler with multilevel queue having two queues which will schedule the processes on the basis of  pre-emptive shortest remaining processing time first algorithm (SROT) followed by a scheduling in which each process will get 2 units of time to execute. Also note that queue 1 has higher priority than queue 2.  Consider the following set of processes (for reference)with their arrival times and the CPU burst times in milliseconds.
-------------------------------------
Process  Arrival-Time   Burst-Time
-------------------------------------
P1             0      	       5
P2             1             	       3
P3             2                       3
P4             4                       1                  //


#include<string.h> 
#include<stdio.h> 
#include<pthread.h> 
#include<unistd.h> 
#include<stdlib.h> 
int main() 
{ 
int at[10],bt[10],rt[10],endTime,i,smallest; 
int remain=0,n,time,sum_wait=0,sum_turnaround=0; 
printf(" Welcome To The Operating System Project \n"); 

printf("Enter Number of Processes : "); 
scanf("%d",&n); 
for(i=0;i<n;i++) 
{ 
printf("Enter Arrival-time for Process P%d : ",i+1); 
scanf("%d",&at[i]); 
printf("Enter Burst-time for Process P%d : ",i+1); 
scanf("%d",&bt[i]); 
rt[i]=bt[i]; 
} 
printf("\n\nProcess\t|Turnaround Time| Waiting Time\n\n"); 
rt[9]=9999; 
for(time=0;remain!=n;time++) 
{ 
smallest=9; 
for(i=0;i<n;i++) 
{ 
if(at[i]<=time && rt[i]<rt[smallest] && rt[i]>0) 
{ 
smallest=i; 
}} 
rt[smallest]--; 
if(rt[smallest]==0) 
{ 
remain++; 
endTime=time+1; 
printf("\nP[%d]\t|\t%d\t|\t%d",smallest+1,endTime-at[smallest],endTime-bt[smallest]-at[smallest]); 
sum_wait+=endTime-bt[smallest]-at[smallest]; 
sum_turnaround+=endTime-at[smallest]; 
} 
} 
printf("\n\nAverage waiting time = %f\n",sum_wait*1.0/n); 
printf("Average Turnaround time = %f",sum_turnaround*1.0/5); 
return 0; 
}






