# Intro
[link to chapter 2](https://pages.cs.wisc.edu/~remzi/OSTEP/intro.pdf)

A running program does one very simple thing: it executes instructions. The processor fetches an instruction from memory, decodes it 
and executes it. After its done with this instruction, it moves on to the next one, and so on until the program finally completes. 

There is a body of a software that is making it easy to run programs, allows them to share memory and ables them to interact with
devices. The body of the software is called the operating system. It is in charge of making sure the system operates correctly. 
The OS goes through this via visualization. That is, the OS takes a physical resource, such as processor, memory, ect, an ransforms it to an easy-to-use virtual form of itself.

In order for users to tell the OS what to do, the OS also provides some interfaces (APIs) that can be called. We can say that the OS provides a standard library to applications. Since virtualization allows sharing the CPU, the memory and disks, the OS is sometimes known as a resource manager. Each of the CPU, memory and disks are known as a resorce in the system and the OS's role is to manage them. 

The OS, with help of the hardware, is in charge of running multiple programs at the same time. Virtualizisin the CPU is turning a single CPU into seemingly infinite number of CPUs. This allows multiple programs to run at the same time. 

To run and stop programs, APIs are needed to communicate the desires to the OS. The Os is also a resource manager using policies to manage the resources. 

The model of physical memory presented by modern macines is just an array of bytes. Memory is accessed all the time when a program is running, as it keeps all of its data structures in memory. 

Concurrency is a host of problems that arise and must be adressed when working wit multiple things at once in the same program. 

In system memory data can be easily lost as values can be stored in a volatile manner. That is when power goes away or the system crashes, all data in memory is lost. Thus, we need hardware and software to be able to store data persistently. The software in the OS that usually manages the disk is called file system. 

what an OS actually does: it takes physical resources, such as a CPU, memory, or disk, and virtualizes them. It handles tough and tricky issues related to concurrency. And it stores files persistently, thus making them safe over the long-term

One goal in designing an os is to provide high performance, provide protection, be energy-efficient, be secure and mobile.

## Chapter 2 quick notes

- Both the CPU and memory are virtualized; like each program has access to its own private copy at a time
- Strange things happen when dealing with concurrency. Load, increment and store back don't happen automatically (all at once)
- Persistence is storing files in the file system. It is messy, as the OS does lot of work and makes thing available through system calls (standard library)
- We have to build abstractions
- We care about time complexity and space complexity (on disk and in memory)
- Protection/isolation
- Reliability
- Energy efficiency
- Security
- Mobility (as in portability)
- System call vs procedure call; system calls elevate permission to the hardware privilege level via a trap or trap handler. 
