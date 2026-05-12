# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:
## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

## 2.1-OS-Linux-Process API - fork() , getpid() , getppid()  
Program:  

#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>  

int main() {  
    int pid = fork();  
 
    if (pid == 0) {   
        printf("I am child, my PID is %d\n", getpid());   
        printf("My parent PID is: %d\n", getppid());   
        sleep(2);  // Keep child alive for verification  
    } else {   
        printf("I am parent, my PID is %d\n", getpid());   
        wait(NULL);   
    }  
}  

## output
<img width="809" height="629" alt="exp2" src="https://github.com/user-attachments/assets/da157840-6a97-405b-8b0a-1474c6875060" />  


## 2.2-OS-Linux-Process API -exec(), exit() , wait()   
Program:   
  
#include <stdio.h>  
#include <stdlib.h>  
#include <sys/types.h>  
#include <sys/wait.h>  
#include <unistd.h>  
  
int main() {   
    int status;   
      
    printf("Running ps with execl\n");  
    if (fork() == 0) {  
        execl("ps", "ps", "-f", NULL);  
        perror("execl failed");  
        exit(1);  
    }  
    wait(&status);   
       
    if (WIFEXITED(status)) {   
        printf("Child exited with status: %d\n", WEXITSTATUS(status));   
    } else {   
        printf("Child did not exit successfully\n");   
    }  
    
    printf("Running ps with execlp (without full path)\n");   
    if (fork() == 0) {   
        execlp("ps", "ps", "-f", NULL);   
        perror("execlp failed");   
        exit(1);   
    }   
    wait(&status);  
       
    if (WIFEXITED(status)) {  
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));  
    } else {  
        printf("Child did not exit successfully\n");  
    }  
    
    printf("Done.\n");  
    return 0;  
}  

## OUTPUT   
<img width="828" height="593" alt="OS" src="https://github.com/user-attachments/assets/df9bf69a-f877-43e1-8c8f-d2cd0ffbfb1a" />  




# RESULT:
The programs are executed successfully.
