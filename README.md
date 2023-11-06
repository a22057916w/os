## Chapter 1
1. What is an Operating System? \
   A program acts as an intermediary between the user and computer hardware, also a resource allocator to handle the resources that the user might use, such as memory, CPU time ...

2. What are the two important things after an interrupt occurred? 
   1. Execute the Interrupt Service Routine(ISR) 
   2. Save the return address of the swapped process 

3. What's the difference between asymmetric and symmetric multiprocessing? \
   In asymmetric multiprocessing, each processor has its own specific job, and there is one hot-standby **boss** processor to control the system, if a processor fails, the **boss**
   processor would replace it. In symmetric multiprocessing, each processor performs all tasks in the system and shares the data in memory. 

4. Why is Dual-Mode operation required, and what is the example? \
   To avoid user process compromise the kernel resource. For example, if a user process can access the kernel resource, it might take another process's memory space. 

5. What is the difference between a hardware interrupt and a software interrupt? \
   A hardware interrupt is triggered by external hardware, like a mouse, keyboard... While a software interrupt is triggered by programs, like exceptions. 

## Chapter 2
1. What is a core dump and a crash dump? \
   A core dump is a binary file that captures a snapshot of the program's memory when it crashes. It includes program data, stack, and registers. \
   A crash dump is a collection of files that record the status of the entire system when it experiences a system crash. It includes the info about the kernel, running programs,
   system memory, and hardware status...

2. What are the types of system calls? (list at least 3) 
   1. File Management
   2. Device Management
   3. Communication

3. What are the three general methods to pass parameters to OS? 
   1. Passed directly through the CPU registers.
   2. Push to the stack, and pop by the OS.
   3. Store in a memory block(a data structure), access through the pointer.

4. What are the advantages and disadvantages of two-step boots? \
   Advantage: Allows multiple OS to exist, more flexible. \
   Disadvantage: It's more complex and the boot-up time is slower.

5. What are the advantages and disadvantages of Micro-Kernel? \
   Micro-kernel moves most kernel functions to user space to minimize the kernel. Therefore it's more flexible, secure, and easy to extend, but more communication between kernel and user
   space.
   
6. How does a computer boot up and start the OS? \
   One-Step: The power-up button signals the bootstrap program to load the OS to the memory and start up the OS. \
   Two-Step: The power-up button signals the pointer to the bootstrap program, loads the bootstrap program to the memory, the bootstrap program loads the OS to the memory, starts up the OS.

7. There are various structural types an OS (list at least 3)
   1. Layered System: The OS is divided into many layers, the bottom is the hardware, and the highest is the user interface.
   2. MicroKernel: The system moves most of the kernel functions to the user space to minimize the kernel. And involves many message passing between kernel and user space.
   3. Module Kernel: The kernel has a set of core components and links via modules, it's more flexible and doesn't require message passing between modules.
  
## Chapter 3
1. What is a PCB(Process Control block)? (List 5 items that are maintained in a PCB and discuss the purpose of each item) 
   1. Process State: States like running, waiting, ...
   2. Program Counter: Indicate the next instruction of the program.
   3. Process number: Process identifier, similar to Linux pid.
   4. Register: Store the information of registers used.
   5. Memory limit: Information about a process's memory boundary and space.
   
2. (1) What do long-term scheduler and short-term scheduler do? \
   (2) Provide at least two reasons why the medium-term scheduler might choose to swap a process. \
   <br>
   (1) The long-term scheduler selects the process to the ready queue, while the short-term scheduler assigns a process to the CPU from the ready queue. \
   (2) If a process takes too much CPU time, the medium-term would swap out the process to release the CPU and the memory.
   
3. There are several cases of Process Creation's Execution options and explain how to run? \
   Parent processes create children processes, which in turn, form a tree of processes.

4. (1)What is a zombie process? How to avoid zombie process? \
   (2)What is a orphan process? How to avoid orphan process? \
   <br>
   (1) A process is a zombie if it is terminated but whose parent has not yet called wait(). The parent should soon call wait(). \
   (2) A process is an orphan if its parent is terminated and did not call wait(). The Parent should call wait() to wait for the child process terminate. Another approach is to assign a new
   parent to the orphan.

5. What are the key differences(please answer at least 3)between shared memory and message passing as two interprocess communication mechanisms?
   1. Communication Method: Shared memory allows processes to directly access and modify the shared memory regions, while message passing uses a message queue as a communication medium, 
      with processes receiving and sending messages. 
   2. Synchronization: In shared memory, processes can rapidly share information, but it requires appropriate synchronization mechanisms to prevent race conditions. In message passing, 
      communication is typically asynchronous.
   3. Concurrency: Shared memory often requires more complex mechanisms to achieve concurrency due to the race condition, while message-passing is easier to implement.

6. What is the difference between direct communication and indirect communication? \
   For direct communication, processes receive and send messages directly to each other. For indirect communication, processes receive and send messages to an intermediate entity like 
   mailbox, to communicate with each other.

7. What is the difference between RPC and LPC? \
   RPC typically involves communication between processes on remote systems, while LPC is typically used for communication between processes on the local system. RPC uses network protocol(
   such as TCP/IP) to communicate with the remote system, while LPC utilizes local communication mechanisms like local sockets or shared memory.

## Chapter 4
1.	Explain what "Context Switching" means in multi-threaded programming? What is its role in a multi-threaded environment? \
   It means the OS switches the threads, its stack, and registers, not the entire PCB. The role of a multi-threaded is to improve the efficiency of the context switch for reason 
   aforementioned.

2. What are the benefits of multithreading? \
   Responsiveness: It allows the CPU to execute if a part of the process is blocked by switching threads. \
   Resource Sharing: The threads can access the data by shared memory, better than message-passing. \
   Economy: Cheaper than process creation, thread switching also has lower overhead. \
   Scalability: Processes can take advantage of a multiprocess system.

3. What is a thread in OS? \
   The smallest unit that the CPU can execute.

4. What is the thread pool? \
   A number of threads in a pool that wait for the process to assign work.

5. What are the advantages of using thread pools? (list at least 2) 
   1. It's more efficient to assign work to an existing thread in a pool than creating a new thread.
   2. The OS can limit the number of threads that a process can use to prevent a process from taking too many resources.

6. In Windows threads, what are the primary data structures of a thread? Name three of them, specify in which space they reside, and describe their basic functions. \
   ETHREAD (Executive Thread Block): It includes the pointer to a process, and indicates the belonging KTHREAD, which is in kernel space. \
   KTHREAD (Kernel Thread Block): Scheduling and synchronizing info, kernel-mode stack, the pointer to TEB, which is in kernel space. \
   TEB (Thread Environment Block): Thread id, user-mode stack, thread local storage, which is in user space.

7. What is the difference between the user thread and kernel thread? \
   The user thread is managed by user-level library, while the kernel thread is support by the kernel.

8. How to handle the signal in OS? 
   1. Deliver the signal to the appropriate thread.
   2. Deliver the signal to every thread.
   3. Deliver the signal to a certain thread.
   4. Specify a thread to receive all signals.
  
## Chapter 5-1
1. The exponential averaging algorithm can help the scheduler estimate the next CPU burst time. Please explain in what context, the algorithm cannot estimate the next CPU burst time precisely. \
   The exponential averaging algorithm goes: \
                              $$\tau_n+1 = \alpha t_n + (1-\alpha)\tau_n$$ \
   Where $\tau_n+1$ is the next burst time predicted, $t_n$ is the previous actual burst time, and $\tau_n$ is the previous predicted burst 
   time. The parameter $\alpha$ control the weight of $t_n$ and $\tau_n$.

