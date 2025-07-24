### PROCESS MANAGEMENT:

```c
1. Write a C program to demonstrate the use of fork() system call.
                              (or)
3. Write a program in C to create a child process using fork() and print its PID.
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
int main()
{
        pid_t pid;
        pid=fork();//create a child process
        if(pid<0)//fork() failed
        {
                perror("fork failed");
                return 1;
        }
        else if(pid==0)//child process
        {
                printf("this is the child process.\n");
                printf("child pid:%d\n",getpid());
                printf("parent pid:%d\n",getppid());
        }
        else
        {
                printf("this is the parent process.\n");//parent process
                printf("parent pid :%d\n",getpid());
                printf("child pid: %d\n",pid);
        }
        return 0;
}

Explanation:
    pid_t pid; — Defines a variable to store the process ID.
    fork(); — Creates a new process.
    pid == 0 — Means the current process is the child.
    pid > 0 — Means the current process is the parent, and pid contains the child’s PID.
    pid < 0 — Means the fork() call failed.

     program explaination:
These header files are required:
    <stdio.h> is for standard input/output like printf().
    <unistd.h> gives access to system calls like fork(), getpid(), and getppid().
    <sys/types.h> defines data types like pid_t (used to hold process IDs).
  * pid_t is a data type for process IDs.
  * pid will store the return value of fork().
  * getpid() returns the process ID of the current process (child).
  * getppid() returns the parent’s PID (the process that created this one).
  * getpid() returns the parent’s PID.
  * pid holds the child’s PID, returned by fork().
/**********************************************************************************************************************/
2. Write a C program to illustrate the use of the execvp() function?
#include<stdio.h>
#include<unistd.h>
int main()
{
        char *args[]={"ls","-l",NULL};//command and arguments
        printf("before execvp()\n");
        if(execvp("ls",args)==-1)//replace current process with "ls -l"
        {
                perror("execvp failed");
        }
        printf("after execvp()\n");//this line only runs if execvp fails
        return 0;
}

What is execvp()?
 *  execvp() is one of the exec family functions.
 *  It replaces the current process image with a new program.
 *  The v means it takes arguments as an array (vector).
 *  The p means it searches the PATH to find the command.
/****************************************************************************************************************************/
4. Write a C program to create multiple child processes using fork() and display their
PIDs?
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
int main()
{
        int n=3;//number of child processes to create
        pid_t pid;
        for(int i=0;i<n;i++)
        {
                pid=fork();
                if(pid<0)
                {
                        perror("fork failed");
                        return 1;
                }
                if(pid==0)//child process
                {
                        printf("child %d:pid=%d,parent pid=%d\n",i+1,getpid(),getppid());
                        return 0;
                }
        }
        for(int i=0;i<n;i++)
        {
                wait(NULL);
        }
        printf("parent process :pid=%d\n",getpid());
        return 0;
}
/*************************************************************************************************************************/
5. Write a program in C to create a zombie process and explain how to avoid it?
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    }

    if (pid == 0) {
        // Child process
        printf("Child process: PID = %d\n", getpid());
        exit(0);  // Child exits immediately
    } else {
        // Parent process
        printf("Parent process: PID = %d\n", getpid());
        printf("Child PID = %d has terminated but not waited for — it becomes a zombie.\n", pid);
        
        sleep(20);  // Give time to observe zombie with `ps` or `top`
        
        // No wait() is called, so child becomes zombie temporarily
    }

    return 0;
}
/**************************************************************************************************************************/
6.Write a C program to demonstrate the use of the waitpid() function for process
synchronization?
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    pid_t child1, child2;
    int status;

    // Create first child
    child1 = fork();

    if (child1 == 0) {
        // First child process
        printf("Child 1 (PID: %d) is running.\n", getpid());
        sleep(2); // Simulate some work
        printf("Child 1 (PID: %d) is exiting.\n", getpid());
        exit(1);
    }

    // Create second child
    child2 = fork();

    if (child2 == 0) {
        // Second child process
        printf("Child 2 (PID: %d) is running.\n", getpid());
        sleep(4); // Simulate longer work
        printf("Child 2 (PID: %d) is exiting.\n", getpid());
        exit(2);
    }

    // Parent process
    printf("Parent is waiting for Child 1 (PID: %d)...\n", child1);
    waitpid(child1, &status, 0);
    printf("Child 1 exited with status %d\n", WEXITSTATUS(status));

    printf("Parent is waiting for Child 2 (PID: %d)...\n", child2);
    waitpid(child2, &status, 0);
    printf("Child 2 exited with status %d\n", WEXITSTATUS(status));

    printf("Parent process done.\n");

    return 0;
}
/***************************************************************************************************************************/
7. Write a program in C to create a daemon process?
 #include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<fcntl.h>
#include<sys/stat.h>
#include<sys/types.h>
#include<syslog.h>
#include<string.h>
void create_daemon()
{
        pid_t pid;//fork the process
        pid =fork();
        if(pid<0)
        {
                perror("fork failed");
                exit(EXIT_FAILURE);
        }
        if(pid>0)//exit the parent process
        {
                printf("daemon pid:%d\n",pid);
                exit(EXIT_SUCCESS);
        }
        if(setsid()<0)//create a new session
        {
                perror("setsid failed");
                exit(EXIT_FAILURE);
        }
        pid=fork();
               if(pid<0)
                {
                        perror("second fork failed");
                        exit(EXIT_FAILURE);
                }
                if(pid>0)
                {
                        exit(EXIT_SUCCESS);
     }
                umask(0);
                if(chdir("/")<0)
                {
                        perror("chdir failed");
                                {
                                        exit(EXIT_FAILURE);
                                }
                                close(STDIN_FILENO);
                                close(STDIN_FILENO);
                                close(STDIN_FILENO);
                                open("/dev/null",O_RDONLY);
                                open("/dev/null",O_WRONLY);
                                open("/dev/null",O_RDWR);
                                openlog("mydeamon",LOG_PID,LOG_DAEMON);
                                while(1)
                                {
                                        syslog(LOG_INFO,"daemon is running...");
                                        sleep(30);
                                }
                                closelog();
                }
}
                int main()
                {
                        create_daemon();
                        return 0;
                }
/****************************************************************************************************************************************/
8. Write a C program to demonstrate the use of the system() function for executing shell
commands?                                                                                                                      
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int status;
        printf("listing files in the current directory using 'ls -l':\n");
        status = system("ls -l");
        if(status==-1)
        {
                perror("system");
        }
        printf("\ncreating directory named 'demo_dir':\n");
        status=system("mkdir demo_dir");
        if(status==-1)
        {
                perror("system");
        }
        printf("\ndisplaying current date and time:\n");
        status=system("date");
        if(status ==-1)
        {
                perror("system");
        }
        return 0;
}
/***********************************************************************************************************************************/
9. Write a C program to create a process using fork() and pass arguments to the child?
process.
#include<stdio.h>
#include<stdlib.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<unistd.h>

int main()
{
        pid_t pid;
        pid=fork();
        if(pid<0)
        {
                perror("fork");
                exit(EXIT_FAILURE);
        }
        else if(pid==0)
        {
                printf("child process(pid:%d)\n",getpid());
                printf("executing 'ls -l /' using execlp...\n");
                execlp("ls","ls","-l","/",NULL);
                perror("execlp failed");
                exit(EXIT_FAILURE);
        }
        else
        {
                printf("parent process(pid:%d),created child (pid:%d)\n",getpid(),pid);
                wait(NULL);
                printf("child process completed.\n");
        }
        return 0;
}
/******************************************************************************************************************************/
  9. Write a program in C to demonstrate process synchronization using semaphores.          
#include<stdio.h>
#include<pthread.h>
#include<semaphore.h>
#include<unistd.h>
#define BUFFER_SIZE 5
int buffer[BUFFER_SIZE];
int in=0,out=0;
sem_t empty,full,mutex;
void* producer(void*arg)
{
        int item;
        for(int i=0;i<10;i++)
        {
                item=i+1;
                sem_wait(&empty);
                sem_wait(&mutex);
                buffer[in]=item;
                printf("producer produced:%d\n",item);
                in =(in+1)%BUFFER_SIZE;
                sem_post(&mutex);
                sem_post(&full);
                sleep(1);
        }
        return NULL;
}
void* consumer(void* args)
{
        int item;
        for(int i=0;i<10;i++)
        {
                sem_wait(&full);
                sem_wait(&mutex);
                item=buffer[out];
                printf("consumer consumed:%d\n",item);
                out=(out+1)%BUFFER_SIZE;
                sem_post(&mutex); sleep(2);
        }
        return NULL;
}
int main()
{
        pthread_t prod,cons;
        sem_init(&empty,0,BUFFER_SIZE);
        sem_init(&full,0,0);
        sem_init(&mutex,0,1);
        pthread_create(&prod, NULL, producer, NULL);
    pthread_create(&cons, NULL, consumer, NULL);

    pthread_join(prod, NULL);
    pthread_join(cons, NULL);

    sem_destroy(&empty);
    sem_destroy(&full);
    sem_destroy(&mutex);

    return 0;
}
/**************************************************************************************************************/
10. Write a C program to demonstrate the use of the execvpe() function?
#define _GNU_SOURCE
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
int main()
{
        printf("this is example of execvpe\n");
        char *args[]={"ls","-l",NULL};
        char *envp[]={"MYVAR=helloworld","PATH=/bin:/usr/bin",NULL};
        printf("running ls with custom environment using execvpe()..\n");
        if(execvpe("ls",args,envp)==-1)
        {
                perror("execvpe failed");
        }
        return 0;
}
                                        (or)
#define _GNU_SOURCE
#include <stdio.h>
#include <unistd.h>

int main() {
    char *args[] = {"ls", "-l", NULL};
    char *envp[] = {"MYVAR=helloworld", "PATH=/bin:/usr/bin", NULL};

    execvpe("ls", args, envp);

    perror("execvpe failed");
    return 1;
}
syntax:
int execvpe(const char *file, char *const argv[], char *const envp[]);
             ls commamds      arguments              path
 /***********************************************************************************************************************/
11. Write a C program to create a process group and change its process group ID (PGID).                                    
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
int main()
{
        pid_t pid=fork();
        if(pid==0)
        {
                printf("child pid:%d\n",getpid());
                printf("child pgid:%d\n",getpgrp());
                setpgid(0,0);
                printf("child pgid after:%d\n",getpgrp());
        }
        else if(pid>0)
        {
                sleep(1);
                printf("parent pid:%d\n",getpid());
                printf("parent pgid:%d\n",getpgrp());
        }
        else
        {
                perror("fork failed");
        }
        return 0;
}
/****************************************************************************************************************************/
12. Write a program in C to demonstrate inter-process communication (IPC) using shared
memory.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/ipc.h>
#include<sys/shm.h>
#include<sys/wait.h>
int main()
{
        key_t key = ftok("shmfile",65);
        int shmid=shmget(key,1024,0666|IPC_CREAT);
        char *str=(char*)shmat(shmid,NULL,0);
        pid_t pid=fork();
        if(pid==0)
        {
                sleep(1);
                printf("child reads:%s\n",str);
                shmdt(str);
                }
        else
        {
                strcpy(str,"hello from parent!");
                printf("parent wrote:%s\n",str);
                wait(NULL);
                shmdt(str);
                shmctl(shmid,IPC_RMID,NULL);
        }
        return 0;
}
syntax:
key_t ftok(const char *pathname, int proj_id);
/***************************************************************************************************************/
13. Write a C program to create a child process using vfork() and demonstrate its usage?
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        int x=10;
        pid_t pid=vfork();
        if(pid<0)
        {
                perror("vfork failed");
                exit(1);
        }
        else if(pid==0)
        {
                printf("child process:pid=%d\n",getpid());
                printf("child: x=%d\n",x);
                x=20;
                printf("child changed x=%d\n",x);
                exit(0);
        }
        else
        {
                printf("parent process:pid=%d\n",getpid());
                printf("parent:x=%d\n",x);
        }
        return 0;
}
                                (or)
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main() {
    pid_t pid = vfork();

    if (pid < 0) {
        perror("vfork failed");
        exit(1);
    } else if (pid == 0) {
        // Child process
        printf("In child, PID: %d\n", getpid());
        _exit(0);  // Use _exit, not exit
    } else {
        // Parent process
        printf("In parent, PID: %d\n", getpid());
    }

    return 0;
}

syntax:
pid_t vfork(void);
   |           \
return type    arguments
  (or)
data type
pid<0 - vfork failed (or) error creating process
pid==0 - create child process (or) returned to the child
pid>0 - create parent process (or) returned to the parent, contains child's pid 
/********************************************************************************************************/
13. Write a C program to create a pipeline between two processes using the pipe() system
call?
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
int main()
{
        int fd[2];
        pid_t pid;
        char write_msg[]="hello from parent";
        char read_msg[100];
        if(pipe(fd)==-1)
        {
                perror("pipe failed");
                return 1;
        }
        pid=fork();
        if(pid<0)
        {
                perror("fork failed");
                return 1;
        }
        else if(pid==0)
        {
                close(fd[1]);
                read(fd[0],read_msg,sizeof(read_msg));
                printf("child received:%s\n",read_msg);
                close(fd[0]);
        }
        else
        {
                close(fd[0]);
                write(fd[1],write_msg,strlen(write_msg)+1);
                close(fd[1]);
        }
        return 0;
}

These headers provide:
    stdio.h → For printf()
    unistd.h → For pipe(), fork(), read(), write(), close()
    stdlib.h → For exit()
    string.h → For strlen()
pipe(fd)  -	Creates a unidirectional communication channel
fd[0] -	 Read end of the pipe
fd[1] -	Write end of the pipe
fork() - Creates child process
read() / write()   -	System calls for pipe communication
close() - Always close unused ends of the pipe
/********************************************************************************************************************************/
14. Write a program in C to demonstrate the use of the nice() system call for adjusting
process priority.
#include <stdio.h>
#include <unistd.h>
#include <errno.h>

int main() {
    int result;

    printf("Trying to increase process priority (set nice value to -5)...\n");

    errno = 0;  // Clear errno
    result = nice(-5);  // Increase priority (requires root)

    if (result == -1 && errno != 0) {
        perror("nice failed");
    } else {
        printf("New nice value: %d\n", result);
    }

    return 0;
}
/****************************************************************************************************************************/
15.write a program in c to demonstrate the use of the nice() system call for adjusting lower priority?
#include <stdio.h>
#include <unistd.h>
int main() {
    int new_nice = nice(5); // Increase niceness (lower priority)
    printf("New nice value: %d\n", new_nice);
    return 0;
}
explation:
header file:
#include<sys/resource.h>
nice() is used to change the scheduling priority of the calling process.
It adds increment to the current nice value.
    Nice values range from:
   -20 (highest priority)   
    to +19 (lowest priority)
return value:
new nice value - on success
-1 - on failure(errno is set appropriately)
 getpriority()	Gets current nice value
setpriority()	Sets nice value directly (requires root)
nice()	Adds increment to current nice value.
/*********************************************************************************************/
16.Write a C program to demonstrate the use of the clone() system call to create a thread.
#define _GNU_SOURCE
#include<sched.h>
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<signal.h>
#include<sys/wait.h>
#define stacksize 1024*1024
int shared_var=0;
int child_func(void *arg)
{
        printf("child:modifying shared_var..\n");
        shared_var+=10;
        printf("child:shared_var=%d\n",shared_var);
        return 0;
}
int main()
{
        char *stack=malloc(stacksize);
        if(!stack)
        {
                perror("malloc");
                        exit(EXIT_FAILURE);
        }
        char *stack_top=stack+stacksize;
        pid_t child_pid=clone(child_func,stack_top,CLONE_VM|CLONE_FS|CLONE_FILES|CLONE_SIGHAND|SIGCHLD,NULL);
        if(child_pid==-1)
        {
                perror("clone");
                free(stack);
                exit(EXIT_FAILURE);
        }
        waitpid(child_pid,NULL,0);
        printf("parent:shared_var=%d\n",shared_var);
        free(stack);
        return 0;
}
/******************************************************************************************************/
15.Write a C program to create a child process using fork() and communicate between
parent and child using pipes. 
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#define buffersize 100
int main()
{
        int pipe1[2];
        int pipe2[2];
        pid_t pid;
        char parent_msg[]="hello from parent!";
        char child_msg[]="hello from child!";
        char buffer[buffersize];
        if(pipe(pipe1)==-1||pipe(pipe2)==-1)
        {
                perror("pipe");
                exit(EXIT_FAILURE);
        }
        pid=fork();
        if(pid<0)
        {
                perror("fork");
                exit(EXIT_FAILURE);
        }
        else if(pid==0)
        {
                close(pipe1[1]);
                close(pipe2[0]);
                read(pipe1[0],buffer,buffersize);
                printf("child received:%s\n",buffer);
                write(pipe2[1],child_msg,strlen(child_msg)+1);
                close(pipe1[0]);
                close(pipe2[1]);
        }
        else
        {
        close(pipe1[0]);
                close(pipe2[1]);
                write(pipe1[1],parent_msg,strlen(parent_msg)+1);
                read(pipe2[0],buffer,buffersize);
                close(pipe1[1]);
                close(pipe2[0]);
        }
        return 0;
}
/**************************************************************************************************/
17.Write a C program to demonstrate process synchronization using the fork() and wait()
system calls.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/wait.h>
int main()
{
        pid_t pid;
        pid=fork();
        if(pid<0)
        {
                perror("for failed");
                exit(EXIT_FAILURE);
        }
        else if(pid==0)
        {
                printf("child:starting task..\n");
                sleep(2);
                printf("child:finished task.\n");
                exit(0);
        }
        else
        {
                printf("parent :waiting for child to finish...\n");
                wait(NULL);
                printf("parent:child finished. continuing parent tas.\n");
        }
        return 0;
}
/********************************************************************************************/
18.Write a C program to create a process using fork() and change its scheduling policy
using sched_setscheduler().
#define _GNU_SOURCE
#include<stdio.h>
#include<stdlib.h>
#include<sys/wait.h>
#include<sched.h>
#include<errno.h>
#include<string.h>
int main()
{
        pid_t pid;
        struct sched_param schedparam1;
        schedparam1.sched_priority=50;
        pid=fork();
      if(pid<0)
      {

        perror("fork failed");
        exit(EXIT_FAILURE);
      }
else if(pid==0)
{
        printf("child:pid=%d\n",getpid());
        if(sched_setscheduler(0,SCHED_FIFO,&schedparam1)==-1)
        {
                perror("sched_setschedular failed");
                printf("child:are you running as root?some policies require root privileges.\n");
        }
        else
        {
                        printf("child:scheduling policy changed to schedfifo with priority %d\n",schedparam1.sched_priority);
                }
                for(int i=0;i<5;i++)
                {
                        printf("child:working %d...\n",i+1);
                        sleep(1);
                }
                      exit(EXIT_SUCCESS);
        }
        else
        {
                wait(NULL);
                printf("parent :child process has finished.\n");
        }
        return 0;
}
/*****************************************************************************************************************************/

```

