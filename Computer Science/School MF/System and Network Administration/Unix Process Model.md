# Unix Process Model
Like any other  [[Process of Programs]], a process in a [[UNIX]] model is just an intance of running a program

It is divided by 2 process state
- [[User Running State]]
- [[Kernel Running State]]

## Unix Running State
We also have 8 different Process State
- New State - process being created
- Ready State - [[Process of Programs|process]] waiting to be assigned to a [[Processor]]
- Blocked State - [[Process of Programs|process]] on main memory and waiting for an event
- Blocked Suspended - process in secondary memory and waiting for an event
- Suspend/ Ready - process in secondary memory and ready for execution when it finally goes to main memory
- Exited State - process where parent does not wait when process die for cleaning purpose, it does not have an entry in te [[Process Tables]]
- Zombie - parent wait for completion when process die, it has an entry to the [[Process Tables]]
- Preemted State - special case of blocked state, (kernel mode to user mode), (immediately blocked and put on ready process que i dont understand what the fuck)

![[Pasted image 20220901111755.png]]

