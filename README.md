# Linux-Process-API-fork-wait-exec-
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise
## NAME-SRILAKSHMI.B.H
## REG-212224100057

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

```
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main()
{
    pid_t pid = fork();

    if (pid < 0)
    {
        perror("fork failed");
        return 1;
    }
    else if (pid == 0)
    {
        // Child process
        printf("I am child, my PID is %d\n", getpid());
        printf("My parent PID is: %d\n", getppid());
    }
    else
    {
        // Parent process
        printf("I am parent, my PID is %d\n", getpid());
        sleep(5);  // Shortened sleep to avoid timeout
    }

    return 0;
}
```

##OUTPUT

<img width="368" height="114" alt="Screenshot 2025-09-03 at 1 52 16 PM" src="https://github.com/user-attachments/assets/120cf87c-f65e-4d92-a976-00e3ca71e0ec" />



## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family



```

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main()
{
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0)
    {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)
    {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    }
    else   
    {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0)
    {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status))
    {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    }
    else
    {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}

```

##OUTPUT

<img width="536" height="223" alt="Screenshot 2025-09-03 at 8 26 02 PM" src="https://github.com/user-attachments/assets/a03ccc00-6b81-4484-8dfb-9735ec7db3e4" />




# RESULT:
The programs are executed successfully.
