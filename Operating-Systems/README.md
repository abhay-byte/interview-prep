### **Operating Systems**

#### **Processes and Threads**

**1. Q: What is the primary difference between a process and a thread?**
*   **A:** A **process** is an independent program with its own dedicated memory space (heap, data, code). A **thread** is the smallest unit of execution *within* a process. Threads in the same process share memory (like heap and data), which makes them lightweight and enables fast communication.

**2. Q: What memory segments do threads share, and what is private to each thread?**
*   **A:** Threads **share** the process's **Heap**, **Data**, and **Code** segments. Each thread has its own private **Stack** (for local variables and function calls) and its own set of **CPU Registers** (including the Program Counter).

**3. Q: What is a context switch?**
*   **A:** A context switch is the process of saving the state of one process (or thread) and loading the state of another so the CPU can switch tasks. This involves saving CPU register values and memory maps. It is pure overhead, as no useful work is done during the switch.

**4. Q: When would you choose multiprocessing over multithreading?**
*   **A:** You would choose **multiprocessing** for tasks that require **security, isolation, and stability**. If one process crashes, it won't affect others. It's also ideal for leveraging multiple CPU cores for CPU-bound tasks in languages with a Global Interpreter Lock (GIL) like Python.

#### **CPU Scheduling**

**5. Q: Briefly describe FCFS, SJF, and Round Robin scheduling.**
*   **A:**
    *   **First-Come, First-Served (FCFS):** Processes are executed in the order they arrive. It's simple but can lead to long wait times if a long job arrives first (the "convoy effect").
    *   **Shortest Job First (SJF):** The process with the shortest estimated execution time is run next. It's optimal for minimizing average waiting time but risks starving longer jobs.
    *   **Round Robin (RR):** A preemptive algorithm where each process gets a small time slice (quantum). It's fair and good for responsiveness but has higher context-switching overhead.

**6. Q: What is starvation in the context of CPU scheduling?**
*   **A:** **Starvation** is when a ready process is perpetually denied access to the CPU. This can happen in priority-based or SJF scheduling, where a low-priority or long-running process is constantly overtaken by new, higher-priority or shorter jobs.

**7. Q: What is the difference between preemptive and non-preemptive scheduling?**
*   **A:** In **non-preemptive** scheduling, once a process is given the CPU, it runs until it voluntarily releases the CPU (by terminating or waiting for I/O). In **preemptive** scheduling, the OS can forcibly take the CPU away from a process (e.g., when its time slice expires) to give it to another, more critical process.

#### **Memory Management**

**8. Q: What is virtual memory?**
*   **A:** **Virtual memory** is an OS abstraction that gives each process its own private and contiguous address space. This allows a program to be larger than the physical RAM by storing parts of it on disk and loading them into RAM as needed.

**9. Q: What is a page fault?**
*   **A:** A **page fault** is a hardware-triggered trap to the OS that occurs when a program tries to access a memory page that is not currently loaded in physical RAM. The OS must then find the page on the disk, load it into a free frame in RAM, update the page table, and resume the program.

**10. Q: Differentiate between internal and external fragmentation.**
*   **A:**
    *   **Internal Fragmentation:** Wasted space *inside* an allocated block of memory. This occurs in paging because a process may not need the entirety of the last page it is allocated.
    *   **External Fragmentation:** Wasted space *between* allocated blocks of memory. This occurs in segmentation as variable-sized segments are loaded and unloaded, leaving holes that may be too small for new requests.

**11. Q: What is thrashing?**
*   **A:** **Thrashing** is a state of severe performance degradation where the system spends more time swapping pages between RAM and disk than executing instructions. It happens when there isn't enough physical memory to hold the working set of currently running processes, leading to constant page faults.

**12. Q: What is the purpose of a Translation Lookaside Buffer (TLB)?**
*   **A:** The **TLB** is a small, fast hardware cache inside the MMU that stores recent virtual-to-physical address translations. It speeds up memory access by avoiding the need to perform a slow lookup in the main memory page table for every memory reference.

#### **Concurrency and Synchronization**

**13. Q: What is a race condition?**
*   **A:** A **race condition** occurs when the outcome of a computation depends on the unpredictable timing or ordering of concurrent threads or processes accessing shared data. This can lead to corrupted data and inconsistent results.

**14. Q: Explain the difference between a mutex and a binary semaphore.**
*   **A:** A **mutex** has the concept of "ownership"—the same thread that locks it must be the one to unlock it. It is strictly for enforcing mutual exclusion. A **binary semaphore** is a signaling mechanism; one thread can `wait()` (decrement) and a *different* thread can `signal()` (increment). It can be used for both mutual exclusion and signaling between threads.

**15. Q: What is a deadlock?**
*   **A:** A **deadlock** is a state where two or more processes are permanently blocked, each holding a resource and waiting to acquire a resource held by another process in the same set, creating a circular wait.

**16. Q: What are the four necessary conditions for deadlock to occur?**
*   **A:**
    1.  **Mutual Exclusion:** At least one resource must be non-sharable.
    2.  **Hold and Wait:** A process holds a resource while waiting for another.
    3.  **No Preemption:** A resource cannot be forcibly taken from a process.
    4.  **Circular Wait:** A circular chain of processes exists, each waiting for a resource held by the next.

#### **System Internals and File Systems**

**17. Q: What is a system call?**
*   **A:** A **system call** is the mechanism used by a user-level program to request a service from the operating system's kernel, such as file I/O or process creation. It acts as the bridge between user mode and kernel mode.

**18. Q: Why is there a need for both kernel mode and user mode?**
*   **A:** These two modes provide **protection**. **User mode** is a restricted mode where applications run; they cannot directly access hardware or critical memory. **Kernel mode** is a privileged mode for the OS kernel, which has unrestricted access. This prevents user programs from crashing the entire system or interfering with other processes.

**19. Q: What is an inode in a Unix file system?**
*   **A:** An **inode** is a data structure that stores all metadata about a file (permissions, owner, size, timestamps, etc.) *except* for its name. Most importantly, it contains pointers (direct and indirect) to the actual data blocks on the disk, allowing the OS to locate the file's content.

**20. Q: What is an interrupt?**
*   **A:** An **interrupt** is a signal sent to the CPU from either hardware (e.g., a key press, I/O completion) or software (a system call). It causes the CPU to immediately pause its current execution, save its state, and execute a special function called an Interrupt Service Routine (ISR) to handle the event.