# Virtualization
[link to chapter 3](https://pages.cs.wisc.edu/~remzi/OSTEP/dialogue-virtualization.pdf)

[link to chapter 4](https://pages.cs.wisc.edu/~remzi/OSTEP/cpu-intro.pdf)

[link to chapter 5](https://pages.cs.wisc.edu/~remzi/OSTEP/cpu-api.pdf)

## Processes

> Each peach-eater can eat their own _virtual_ peach, even though there's only one _physical_ peach.

A _process_ is a runnign program. As users we often want to run multiple processes at the same time. To make this happen, the operating system must provide the illusion that there are manu CPUs, so that each process can run on one.

This is done through _virtualization_; processes are stopped and started (called _context switcing_), sharing the CPU time at the cost of taking longer to run. OS's also have _policies_ that determine exactly how decisions like scheduling are made. 

Because a process is by definition a running program, we can understand what processes are by taking account of everything that happens during execution.

The _machine state_ of a process is everything that the program can read of update while running; all the parts were interested in when thinking about the process. Key components of the machine state are:
- _Memory_, which includes the instructions and all the data the program touches (its _address space_)
- _Registers_, part of the processor that are read from and written to over the course of program execution (including the _program counter, stack pointer,_ and _frame pointer_)
- Various IO devices like persistent storage

#### The Process API

In any implementation, the OS needs to provide a basic interface for interacting with processes, supporting operations:
- Create
- Destroy
- Status
- Wait (which can allow one process to wait for another to terminate)
- Miscellaneous control (including support for _suspending_ and _resuming_ processes)

#### Process Creation

Process creation involves taking bytes on disk that specify instructions and turning them into a running program. First, data is _loaded_ into memory, including all of its static data. On modern OS's, this is done _lazily_. Next, memory is allocated for the _stack_, possibly initialized with values (eg. C's `argc` and `argv`). _Heap_ data might also be allocated and depending on the OS there might be additional initialization tasks (like opening file descriptors). Finally, execution begins from `main`, and control is transferred to the CPU to begin execution.

#### Process States 

Processes have three high-level states:
  - Running; executing instructions
  - Ready; ready to run but not currently being executed
  - Bocked; not ready to run until some other event takes place (eg. waiting for an IO request to resolve)

Transitions between ready and running (_scheduled_ vs _descheduled_) happen at the discretion of the OS based on decisions of the _scheduler_.

#### Data structures

A few key data structures are used to keep track of state in typical OS's. For example, a _process list_ tracks process state. This includes the _register context_ (register components) of each stopped process, process states etc.

#### The Unix Process API

The core of Unix process APi is three functions: `fork()` `exec()`, and `wait()`.

##### Fork

`fork()` can be called by a process to create a clone (exact copy) of the calling process. The function returns twice: with value `0` in the child process ad a non-zero positive process id of the child in the calling parent. This process si _nondeterministic_; the parent might run and terminate before child, or vice-versa.

##### Wait

`wait()` can be used to have the parent block until the child finishes executing.

##### Exec

`exec()` is used to run a program that is different from the calling program (which we kinda want to do always). The call accepts as arguments the name of an executable (like `wc`) and some arguments, and then _transforms_ the currently running process into the specified by the arguments. Thus, succesfull calls to `exec` never return, so code after `exec` isn't run.

##### Motivation

Motivation for the API can be understood by considering how it is more useful than alternatives in practice. For example, having distinct `fork()` and `exec()` calls makes it possible for a shell to modify the process environment before running a program. For example, shell redirection might involve setting up some file descriptions before transferring control to the running process.

##### Others

Beyond the main functions, Unix also provides interfaces for interactiong with processes. For example `kill()` is used to send _signals_ to processes including `SIGINT` (interrupt), which generally terminates process, as well as `SIGSTOP` which typically suspends them. Processes can also "catch" signals with `signal()`, allowing arbitrary code to be run in response to them.

To remain sound alongside core OS goals like security and isolation, signals can't be sent arbitrarily. If this were the case, a rogue process could terminate all others on the system. Instead, the OS maintains a notion of a user, who must log in, and can then send signals to processes they have started, but not those started by others on the machine.

### Quick notes chapter 3

- Virtialization is like switching who has the real peach at any given instant in time.

### Quck notes chapter 4

- A process is a running program
- We use time-sharing to virtualize (space sharing also exists)
    - This is used in networking
- Low-level part; time-sharing mechanism, a context switch
- High level part; a scheduling policy
- The previous two should be separate, because modularity
- What makes a process?
    - Memory
    - Registers
    - Program counter / instructuon pointer
    - Stack pointer and associated frame pointer
    - Persistent storage devices, open files (I/O information)
- Process API 
    - Create
    - Destroy
    - Wait
    - Miscellaneous Control
    - Status
- Loading copies code and static data, initializes heap and stack
- Process states
    - Running
    - Ready
    - Blocked
- Processes can be scheduled and descheduled

### Quick notes chapter 5

- `fork()`is a system call that clones current process and returns both itself (parent) and the copy (child), with different return codes
    - Which one gets returned is _nondeterministic_, so if you want the child done firts, you call 'wait()` in the parent branch, which gives the illusion of determinism

- `exec()` is another system call that spawns a different process in the child
    - This is how we make a shell / a repl
 
- `pipe()` is also a system call
