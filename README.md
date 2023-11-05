## Chapter 1
1. What is an Operating System \
   A program acts as an intermediary between the user and computer hardware, also a resource allocator to handle the resources that the user might use, such as memory, CPU time ...

2. What are the two important things after an interrupt occurred 
   1. Execute the Interrupt Service Routine(ISR) 
   2. Save the return address of the swapped process 

3. What's the difference between asymmetric and symmetric multiprocessing \
   In asymmetric multiprocessing, each processor has its own specific job, and there is one hot-standby **boss** processor to control the system, if a processor fails, the **boss**
   processor would replace it. In symmetric multiprocessing, each processor performs all tasks in the system and shares the data in memory. 

4. Why is Dual-Mode operation required, and what is the example \
   To avoid user process compromise the kernel resource. For example, if a user process can access the kernel resource, it might take another process's memory space. 

5. What is the difference between a hardware interrupt and a software interrupt \
   A hardware interrupt is triggered by external hardware, like a mouse, keyboard... While a software interrupt is triggered by programs, like exceptions. 

## Chapter 2
1. What is a core dump and a crash dump \
   A core dump is a binary file that captures a snapshot of the program's memory when it crashes. It includes program data, stack, and registers. \
   A crash dump is a collection of files that record the status of the entire system when it experiences a system crash. It includes the info about the kernel, running programs,
   system memory, and hardware status...

2. What are the types of system calls (list at least 3) 
   1. File Management
   2. Device Management
   3. Communication

3. What are the three general methods to pass parameters to OS 
   1. Passed directly through the CPU registers.
   2. Push to the stack, and pop by the OS.
   3. Store in a memory block(a data structure), access through the pointer.

4. What are the advantages and disadvantages of two-step boots \
   Advantage: Allows multiple OS to exist, more flexible. \
   Disadvantage: It's more complex and the boot-up time is slower.

5. What are the advantages and disadvantages of Micro-Kernel \
   Micro-kernel moves most kernel function to user space to minimize the kernel, therefore \
      Advantage: More flexible, secure, and easy to extend. \
      Disadvantage: More communication between kernel and user space.
   
