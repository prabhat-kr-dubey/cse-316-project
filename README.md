Student Name: Prabhat Kumar Dubey
Student ID: 11802786
Email Address: prabhatpuspendra@gmail.com
GitHub link:

Problem:
20.There are 3 student processes and 1 teacher process. Students are supposed to do their assignments and they need 3 things for that pen, paper and question paper. The teacher has an infinite supply of all the three things. One students has pen,an other has paper and another has question paper. The teacher places two things on a shared table and the student having the third complementary thing makes the assignment and tells the teacher on completion. The teacher then places another two things out of the three and again the student having the third thing makes the assignment and tells the teacher on completion. This cycle continues. WAP to synchronize the teacher and the students. 
Explanation:
1.	In the given solution I have taken all the student processes and resources in 2D array and initialized then to 0.
2.	I have made 3 student processes in three different functions which will be executed by single s_thread and one t_thread for execution of teacher process.
3.	User will get a menu to select any two out of three resources that are to be placed on shared table.
4.	If one process is completed there will be a message printed on the screen saying process is completed.
5.	When one process is executing no other student or teacher process will execute and for achieving this I have used Mutex lock.
6.	When a process starts to execute it acquires the lock and when it completes the execution releases the lock.
7.	After completion of all the three processes the program will end.
Code Snippet:
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
#include<stdbool.h>
int student[3][4]={0};
void *teacher();
void *student1();
void *student2();
void *student3();
pthread_mutex_t lck;
int ch1,ch2;
int r1,r2;

int main()
{	
printf("\t\t\t---Welcome---\n");
	pthread_mutex_init(&lck,NULL);\
student[1][1]=1;
	student[2][2]=2;student[3][3]=1;
	pthread_t t_thread;
	pthread_t s_thread;
printf("Resources Menu: \n\t\tPress '1' for pen\n\t\tPress '2' for paper \n\t\tPress '3' for   question_paper \n"); 	
	while(1)
{
if(student[1][4]==1 && student[2][4]==1 && student[3][4]==1){break;}
pthread_create(&t_thread, NULL, teacher, NULL);
pthread_join(t_thread,NULL);
	    
if((ch1==1 && ch2==2 || ch2==1 && ch1==2 ) && student[3][4]==0)
{
	pthread_create(&s_thread, NULL, student3, NULL);
	pthread_join(s_thread,NULL);
}
else if((ch1==1 && ch2==3 || ch2==1 && ch1==3 ) && student[2][4]==0)
{
pthread_create(&s_thread, NULL, student2, NULL);
	pthread_join(s_thread,NULL);
}
else if((ch1==2 && ch2==3 || ch2==2 && ch1==3 ) && student[1][4]==0)
{
	pthread_create(&s_thread, NULL, student1, NULL);
pthread_join(s_thread,NULL);
}
else
{
	printf("\n\tError (007): try again.. with different choices.\n");
}
}
printf("\n\t----Done---\n");
}


void *teacher()
{
pthread_mutex_lock(&lck);
	printf("\nFirst Resource on shared tabel:-\t");
	scanf("%d",&ch1);
	printf("Second Resource on shared tabel:-\t");
	scanf("%d",&ch2);
	pthread_mutex_unlock(&lck);
}

void *student2()
{	
	pthread_mutex_lock(&lck);
	printf("\nChoices Made = 'pen', 'question_paper'\n");
	student[2][4]=1;
	printf("\n\tStudent 2 has Completed the assignment. \n");
	pthread_mutex_unlock(&lck);
}

void *student3()
{	
	pthread_mutex_lock(&lck);
	printf("\nChoices Made = 'pen', 'paper'\n");
	student[3][4]=1;
	printf("\n\tStudent 3 has Completed the assignment.\n");
	pthread_mutex_unlock(&lck);
}

void *student1()
{	
	pthread_mutex_lock(&lck);
	printf("\nChoices Made = 'paper', 'question_paper'\n");
	student[1][4]=1;
	printf("\n\tStudent 1 has Completed the assignment.\n");	
	pthread_mutex_unlock(&lck);
}












Problem:
7. Researchers designed one system that classified interactive and noninteractive processes automatically by looking at the amount of terminal I/O. If a process did not input or output to the terminal in a 1-second interval, the process was classified as noninteractive and was moved to a lower-priority queue. In response to this policy, one programmer modified his programs to write an arbitrary character to the terminal at regular intervals of less than 1 second. The system gave his programs a high priority, even though the terminal output was completely meaningless.
Explanation: 
Code Snippet:
#include<stdio.h>
	int main()
	{
		int i, type[20],n;
		int resptime[20];
		printf("Number of process: ");
		scanf("%d",&n);
		printf("Enter the data\n");
		for(i=0;i<n;i++)
		{
			printf("Response time of P%d (in milliseconds): ",i);
			scanf("%d",&resptime[i]);
			if(resptime[i]<1000)
			{
				type[i]=1;
			}
			else
			{
				type[i]=0;
			}
		}
		printf("Process Number\tResponse Time\tType\t\tPriority");
		for(i=0;i<n;i++)
		{
			printf("\nP%d\t\t%dms\t\t",i,resptime[i]);
			if(type[i]==1)
			{
				printf("Interactive\tHigh");
			}
			else
			{
				printf("Non-Interactive\tLow");
			}
		}
	}

