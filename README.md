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

7. There are various structural types in OS (list at least 3)
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
   a mailbox to communicate with each other.

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
                              $$\tau_{n+1} = \alpha t_n + (1-\alpha)\tau_n$$ \
   Where $\tau_{n+1}$ is the next burst time predicted, $t_n$ is the previous actual burst time, and $\tau_n$ is the previous predicted burst 
   time. The parameter $\alpha$ control the weight of $t_n$ and $\tau_n$. \
   <br>
   As it depends on the actual burst time if the sequence of the burst time varies too much, the exponential average algorithm will lose its 
   precision.

2. What is the purpose of CPU scheduling? \
   To maximize the CPU utility, keep the CPU busy.

3. When and Why does the OS perform CPU scheduling? \
   when: 
      1. Switch from the running state to the waiting or ready state. 
      2. Switch from the waiting state to the ready state. 
      3. Process termination.
   <br> 
   Why: To allocate the limited resources to different processes efficiently, ensure fairness, and optimize.

4. Describe about the Priority Scheduling. \
   Priority scheduling allocates the CPU time to the process with the highest priority to make sure the important task is executed first.

5. What is the Dispatch Latency? \
   The time it takes for the dispatcher to stop one process and start another.

6. What are the Scheduling Criteria?
   1. CPU utilization: Ranging from 0% to 100%, we want to keep the CPU as busy as possible.
   2. Throughput: The number of processes that are completed in a time unit.
   3. Turnaround time: The amount of time to complete a process.
   4. Waiting time: The amount of time that a process spends waiting in the ready queue.
   5. Response time: The time between the first response and request.

7. What is starvation in scheduling? What is the solution? \
   Starvation refers to a lower-priority process that keeps getting preempted by higher-priority processes, so the lower-priority process 
   might never be executed. The solution is to **aging** the lower-priority process, which gradually increases the process' priority as time      goes by.

8. For Round-Robin scheduling, what problems can arise if the time quantum is too small or too large? If the context switch time is less than 10 $\mu$ sec, what is a good time quantum range? \
   If the time quantum goes too large, it acts like FCFS. If too small, it will cause heavy overhead of the context switch. Usually, while        the context switch is in 10 $\mu$ sec, the time quantum would fall in the range: \
                  $$10ms \leq q \leq 100ms$$  
   
## Chapter 5-2
1. What is the difference between AMP and SMP? \
   Asymmetric Multiprocessing (AMP): Only one processor does the scheduling, and the other processors execute the code, like master-slave. \
   Symmetric Multiprocessing (SMP): Each processor has its scheduling method and may share a common ready queue or have its own ready queue.

2. Why is a simulator more accurate than deterministic modeling in algorithm evaluation? 
   1. Simulators can emulate the dynamic behavior of a real system.
   2. Simulators consider the influence of multiple factors.
   3. Simulators precisely capture the system's state at different time.
      
3. Distinguish PCS and SCS scheduling. \
   Process-Contention Scope (PCS): Scheduling for user-thread to LWPs. \
   System-Contention Scope (SCS): Scheduling for kernel thread to CPU. 

4. Which parameters define the multilevel feedback queue scheduler? 
   1. Number of queues.
   2. Scheduling algorithm of each queue.
   3. Method to decide when to move a process to a higher level.
   4. Method to decide when to move a process to a lower level.
   5. Method to decide in which queue the process should put when first entering the system.

5. What is NUMA in the system? \
   NUMA refers to Non-Uniform Memory Access. In such kind of architecture, different CPUs will have different memory access times due to different physical distance between memories and CPUs (If a CPU wants to access another CPU's memory).

6. What are the advantages of NUMA? (list at least 3)
   1. Improve the memory access time by placing the memory physically close to the specific core.
   2. Improve the multi-tasking performance since the CPU usually has to access the memory closet to it.
   3. NUMA system can be easily scaled to more CPU cores and memories.

7. What is the difference between Linux and Windows scheduling algorithms? \
   Linux implements CFS by red-black tree, while Windows implements multi-class priority scheduling by multi-level feedback queue.

## Chapter 6-1
1. What is the Producer and Consumer problem? \
   Producer is a process, which can produce data/items to a queue for the consumer to fetch. \
   Consumer is a process that can fetch data/items from the Producer through a queue.
    
2. Explain the concept of Race Condition. \
   A situation where several processes access and manipulate the same data concurrently and the outcome of the execution depends on the order in which the access takes place.
   
3. Describe Semaphore implementation, and what are the two operations used in Semaphore implementation with no Busy Waiting. \
   Semaphore uses wait() and signal() to check for an available semaphore. wait() is to acquire the semaphore and signal() is to release the semaphore. \
   For the mechanism with no Busy Waiting, the block() operation puts the process into the waiting queue while there is no semaphore to acquire. The wakeup() operation moves the process from the waiting queue to the ready queue while there is 
   an available semaphore.
   
4. How to solve the critical section problem? \
   We can solve the critical section problem by satisfying the three requirements.
      1. *Mutual Exclusion* : only one process can be executed in the critical section.
      2. *Progress* : only those processes that are not in the remainder section can decide which process can enter the critical section.
      3. *Bounded Waiting* : a process must not suffer starvation from waiting to enter the critical section. 

5. What is Synchronization Hardware, and what is its role in a multi-processor system? \
   Synchronization Hardware is hardware that can perform atomic instruction, where atomic means it can not be interrupted even in a multi-processor system. So if there is another process in another process that tries to execute atomic instruction, it will be blocked by the hardware.
   
6. In Semaphore, Why using the while loop in wait() is not a good method? \
   It may incur Busy Waiting that wastes the CPU cycles.
   
7. Explain how the test_and_set() function works in the context of process synchronization. \
   It reads and sets a shared variable, such as LOCK, that cannot be interrupted. If a process wants to enter the critical section, it executes test_and_set() to acquire the lock and prevent other processes from entering the critical section by
   holding the lock.

## Chapter 6-2
1. What is Priority Inversion? and explain the priority-inheritance protocol how to solve it. \
   A lower-priority process holds the resource that is also required by a higher-priority process and thus, the higher-priority must wait for the lower-priority process to finish. If the lower-priority process can be preempted by other lower-priority processes, the higher-priority process needs to wait longer. To solve this problem, the priority-inheritance protocol lets the lower-priority process inherit the higher-priority until it finishes, and then revert. In this way, the     inherited process can not be preempted in the case mentioned before.
    
2. What is the Bounded-Buffer Problem, and how is it addressed using semaphores? \
   In the problem, the produces and consumers share the following data structures:
      1. *int n* : declare there are n buffers.
      2. *semaphore mutex = 1* : make sure only one producer or consumer can access the buffer.
      3. *semaphore empty = n* : update the empty buffer size by protection of semaphore.
      4. *semaphore full = 0* : update the full buffer size by protection semaphore.

4. What problem can occur if semaphores are used incorrectly? Please list three problems. 
   1. *Deadlock* : if two processes are both waiting for the resources that are held by each other respectively, the situation will go into deadlock.
   2. *Starvation* : it could lead to starvation for a process that keeps waiting infinitely, such as LIFO.
   3. *Race Condition* : if the correct order of wait() and signal() is not maintained, the processes might go into a race condition.

5. What's the difference between the First and Second Readers-Writers Problems? Which character will suffer from starvation in the two problems? 
   1. *First Problem* : readers don't need to wait for each other, readers wait only when a writer is writing.
   2. *Seconde Problem* : Once a writer is waiting, no new readers can start reading. \
   Therefore, the writers would starve in the first problem; readers would starve in the second problem.

6.  What is a monitor? \
   It is a high-level code structure includes shared data and procedure that use condition variables to keep only one process using shared data at the same time.

7. Describe the 3 solutions for the Dining-Philosophers Problem.
   1. Allow at most n-1 philosophers to be sitting simultaneously at the table.
   2. Allow a philosopher to pick chopsticks only if both chopsticks are available.
   3. Make odd-number philosophers pick the left chopstick first and then pick the right chopstick, while even-number philosophers pick the chopsticks in the reversed order.
      
## Chapter 7
1. Please list the four conditions that must be satisfied to form a deadlock.
   1. *Mutual Exclusion* : only one process at a time can use a resource.
   2. *Hold and Wait* : a process that holds at least one resource, is waiting for additional resources that are held by other processes.
   3. *No Preemption* : a resource can't be preempted, that is the resource can be released only voluntarily by the process.
   4. *Circular Wait* : the waiting process must form a loop, which means all processes are waiting for each other.

2. What are the methods for handling Deadlocks? 
   1. *Deadlock Prevention* : break one of the four criteria of Deadlock.
   2. *Deadlock Avoidance* : RAG, banker's algorithm.
   3. *Deadlock Detection* : RAG, banker's algoritm.
   4. *Recovery from Deadlock* : select a victim(process) to release the resources and rollback(return to safe state).
      
3. Explain at least one advantage and one disadvantage of the Banker's Algorithm.
   * *Advantage* : avoid deadlock in resource allocation by ensuring a safe sequence of resource requests.
   * *Disadvantage* : only works with a fixed number of resources and processes.

4. We have Deadlock Avoidance methods to help the system avoid deadlock, such as a Resource Allocation Graph and Banker's Algorithm. Why do our computers still suffer from deadlock? \
   Two methods rely on a fixed number of resources and processes. If processes become more and more, resources are still the same. The new processes may break the balance while requesting the resources. 

5. 
