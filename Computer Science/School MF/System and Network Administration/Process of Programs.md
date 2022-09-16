# Processes
In a computer, or multitasking computer, ==all work in a computer program are abstracted, and these abstraction are called Processes==

This could also defined as the instance of running a program. When we run a program, we create an instance or a process of the same name as the program. When 2 user run the same program, we have <u>synonymous processes</u> which is just having 1 program on disk but 2 process in memory, it works like [[OOP]] ins't it?

The management of processes are handled by the [[Kernel]] which dictates the priorities of processes so that they could share the same [[Processor|cpu]] resources. 

Every process have attributes and these attributes are also handled by the [[Kernel]] but in a separate memory called [[Process Tables]]

This handles the resources such as :
- File handles
- [[Memory address]] or allocated memory
- [[Programs]] code
- CPU Registers
In a running program at least