# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking


### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 

    include <sys/stat.h>
    #include <fcntl.h>
    #include <stdlib.h>
    int main()
    {
    char block[1024];
    int in, out;
    int nread;
    in = open("filecopy.c", O_RDONLY);
    out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);
    while((nread = read(in,block,sizeof(block))) > 0)
    write(out,block,nread);
    exit(0);}





## 2.To Write a C program that illustrates files locking

    #include <fcntl.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <sys/file.h>
    int main (int argc, char* argv[])
    { char* file = argv[1];
     int fd;
     struct flock lock;
     printf ("opening %s\n", file);
     /* Open a file descriptor to the file. */
     fd = open (file, O_WRONLY);
    // acquire shared lock
    if (flock(fd, LOCK_SH) == -1) {
        printf("error");
    }else
    {printf("Acquiring shared lock using flock");
    }
    getchar();
    // non-atomically upgrade to exclusive lock
    // do it in non-blocking mode, i.e. fail if can't upgrade immediately
    if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
        printf("error");
    }else
    {printf("Acquiring exclusive lock using flock");}
    getchar();
    // release lock
    // lock is also released automatically when close() is called or process exits
    if (flock(fd, LOCK_UN) == -1) {
        printf("error");
    }else{
    printf("unlocking");
    }
    getchar();
    close (fd);
    return 0;
    }



## OUTPUT

<img width="715" height="380" alt="324231378-3f458eaa-76b8-4625-b729-629030fcff4a" src="https://github.com/user-attachments/assets/eb1b54f2-75ed-44fc-9814-c9f5686f2b4d" />


<img width="852" height="957" alt="324231383-16848c5e-ad93-40d8-8f7c-7a03e66d238b" src="https://github.com/user-attachments/assets/85e2bd1a-212e-4ef3-9109-d22c3e68be1f" />






# RESULT:
The programs are executed successfully.
