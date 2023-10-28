# OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS
# FIRST COME FIRST SERVE
AIM:
To write a program for the first come first serve method of disc scheduling.

ALGORITHM:
```
1: Initialize an array RQ to store disk requests and variables n, TotalHeadMoment, and initial.
2: Prompt the user to input the number of requests (n) and the request sequence (RQ).
3: Prompt the user to input the initial head position (initial).
4: Calculate TotalHeadMoment by iterating through the requests, adding the absolute difference between each request and the current head position to TotalHeadMoment, and updating the head position.
5: Print the TotalHeadMoment as the result of the FCFS disk scheduling.
```
PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int RQ[100],i,n,TotalHeadMoment=0,initial,count=0;
    printf("Enter the number of Requests\n");
    scanf("%d",&n);
    printf("Enter the Requests sequence\n");
    for(i=0;i<n;i++)
     scanf("%d",&RQ[i]);
    printf("Enter initial head position\n");
    scanf("%d",&initial);
    // logic for sstf disk scheduling
        /* loop will execute until all process is completed*/
    while(count!=n)
    {
        int min=1000,d,index;
        for(i=0;i<n;i++)
        {
           d=abs(RQ[i]-initial);
           if(min>d)
           {
               min=d;
               index=i;
           }
        }
        TotalHeadMoment=TotalHeadMoment+min;
        initial=RQ[index];
        // 1000 is for max
        // you can use any number
        RQ[index]=1000;
        count++;
    }
    printf("Total head movement is %d",TotalHeadMoment);
    return 0;
}
```
OUTPUT:
file:///home/sec/Pictures/Screenshots/Screenshot%20from%202023-10-21%2017-17-03.png![image](https://github.com/aparnabalasubrmanian/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/123351172/bcc19eac-e0e1-4074-bc52-480282af0c10)

RESULT:
Thus the implementation of FCFS (First come first serve) Disk scheduling algorithm in C programming is done successfully.

#SHORTEST SEEK TIME FIRST

AIM:
To implement SSTF (Short seek time first ) Disk scheduling algorithm in C programming.

ALGORITHM:
```
1: Initialize variables and arrays for requests, total head movement, initial head position, and a counter.
2: Input the number of requests, the request sequence, and the initial head position from the user.
3: Find the nearest request by looping through the requests, calculating the absolute difference from the current head position, and updating the head position based on the closest request.
4: Repeat this process until all requests are processed, marking completed requests with a large number.
5: Print the total head movement as the result of the SSTF disk scheduling.
```
PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int RQ[100],i,n,TotalHeadMoment=0,initial,count=0;
    printf("Enter the number of Requests\n");
    scanf("%d",&n);
    printf("Enter the Requests sequence\n");
    for(i=0;i<n;i++)
     scanf("%d",&RQ[i]);
    printf("Enter initial head position\n");
    scanf("%d",&initial); 
    // logic for sstf disk scheduling 
        /* loop will execute until all process is completed*/
    while(count!=n)
    {
        int min=1000,d,index;
        for(i=0;i<n;i++)
        {
           d=abs(RQ[i]-initial);
           if(min>d)
           {
               min=d;
               index=i;
           } 
        }
        TotalHeadMoment=TotalHeadMoment+min;
        initial=RQ[index];
        // 1000 is for max
        // you can use any number
        RQ[index]=1000;
        count++;
    } 
    printf("Total head movement is %d",TotalHeadMoment);
    return 0;
}
```
OUTPUT:
file:///home/sec/Pictures/Screenshots/Screenshot%20from%202023-10-21%2017-20-24.png![image](https://github.com/aparnabalasubrmanian/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/123351172/e0ffead2-1f6b-48f0-838d-3f816f22853e)

RESULT:
Thus the implementation of SSTF (Short seek time first ) Disk scheduling algorithm in C programming is done successfully




# Scan Or Elevator
AIM:

To implement Scan Or Elevator Disk scheduling algorithm in C programming.

ALGORITHM:
```
Step 1: Initialize variables and arrays for requests, total head movement, initial head position, disk size, and the head movement direction.

Step 2: Input the number of requests, the request sequence, initial head position, total disk size, and the head movement direction from the user.

Step 3: Sort the request array in ascending order to facilitate the SCAN algorithm.

Step 4: Find the index where the initial head position lies in the sorted request array and calculate head movements in the chosen direction (high or low) while iterating through the requests.

Step 5: Calculate the total head movement by summing the absolute differences in head positions and print the result as the total head movement for the SCAN disk scheduling algorithm.
```

PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int RQ[100],i,j,n,TotalHeadMoment=0,initial,size,move;
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
    // logic for Scan disk scheduling
        /*logic for sort the request array */
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
    // if movement is towards high value
    if(move==1)
    {
        for(i=index;i<n;i++)
        {
            TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
            initial=RQ[i];
        }
        //  last movement for max size 
        TotalHeadMoment=TotalHeadMoment+abs(size-RQ[i-1]-1);
        initial = size-1;
        for(i=index-1;i>=0;i--)
        {
             TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
             initial=RQ[i]; 
        }
    }
    // if movement is towards low value
    else
    {
        for(i=index-1;i>=0;i--)
        {
            TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
            initial=RQ[i];
        }
        //  last movement for min size 
        TotalHeadMoment=TotalHeadMoment+abs(RQ[i+1]-0);
        initial =0;
        for(i=index;i<n;i++)
        {
             TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
             initial=RQ[i]; 
        }
    }
    
    printf("Total head movement is %d",TotalHeadMoment);
    return 0;
}
```

OUTPUT:
file:///home/sec/Pictures/Screenshots/Screenshot%20from%202023-10-21%2017-23-36.png![image](https://github.com/aparnabalasubrmanian/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/123351172/34cf267b-11a4-4139-be63-eecc6dda79ee)


RESULT:
Thus the implementation of Scan Or Elevator Disk scheduling algorithm in C programming is done successfully.

# LOOK

AIM:
To implement look Disk scheduling algorithm in C programming.

ALOGRITHM:
```
Step 1: Initialize variables and arrays for requests, total head movement, initial head position, disk size, and the head movement direction.

Step 2: Input the number of requests, the request sequence, initial head position, total disk size, and the head movement direction from the user.

Step 3: Sort the request array in ascending order to facilitate the LOOK algorithm.

Step 4: Find the index where the initial head position lies in the sorted request array and calculate head movements in the chosen direction (high or low) while iterating through the requests.

Step 5: Calculate the total head movement by summing the absolute differences in head positions and print the result as the total head movement for the LOOK disk scheduling algorithm.
```

PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int RQ[100],i,j,n,TotalHeadMoment=0,initial,size,move;
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
    // logic for look disk scheduling 
        /*logic for sort the request array */
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
    // if movement is towards high value
    if(move==1)
    {
        for(i=index;i<n;i++)
        {
            TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
            initial=RQ[i];
        } 
        for(i=index-1;i>=0;i--)
        {
             TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
             initial=RQ[i];
        }
    }
    // if movement is towards low value
    else
    {
        for(i=index-1;i>=0;i--)
        {
            TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
            initial=RQ[i];
        }
        
        for(i=index;i<n;i++)
        {
             TotalHThus the implementation of look Disk scheduling algorithm in C programming is done successfully.eadMoment=TotalHeadMoment+abs(RQ[i]-initial);
             initial=RQ[i]; 
        }
    }
    printf("Total head movement is %d",TotalHeadMoment);
    return 0;
}
```
OUTPUT:
file:///home/sec/Pictures/Screenshots/Screenshot%20from%202023-10-21%2017-26-28.png![image](https://github.com/aparnabalasubrmanian/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/123351172/fee71a22-f77d-4020-980b-ffae4e0dc4dc)

RESULT:
Thus the implementation of look Disk scheduling algorithm in C programming is done successfully.


