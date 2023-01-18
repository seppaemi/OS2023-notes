# 2 Introduction to operating systems
[link to chapter 2](https://pages.cs.wisc.edu/~remzi/OSTEP/intro.pdf)

A running program does one very simple thing: it executes instructions. The processor fetches an instruction from memory, decodes it 
and executes it. After its done with this instruction, it moves on to the next one, and so on until the program finally completes. 

There is a body of a software that is making it easy to run programs, allows them to share memory and ables them to interact with
devices. The body of the software is called the operating system. It is in charge of making sure the system operates correctly. 
The OS goes through this via visualization. That is, the OS takes a physical resource, such as processor, memory, ect, an ransforms it to an easy-to-use virtual form of itself.

In order for users to tell the OS what to do, the OS also provides some interfaces (APIs) that can be called. We can say that the OS provides a standard library to applications. Since virtualization allows sharing the CPU, the memory and disks, the OS is sometimes known as a resource manager. Each of the CPU, memory and disks are known as a resorce in the system and the OS's role is to manage them. 

The OS, with help of the hardware, is in charge of running multiple programs at the same time. Virtualizisin the CPU is turning a single CPU into seemingly infinite number of CPUs. This allows multiple programs to run at the same time. 

To run and stop programs, APIs are needed to communicate the desires to the OS. The Os is also a resource manager using policies to manage the resources. 

The model of physical memory 
