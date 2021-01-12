# 										processes

Session Moderator : [Mohamed Abdallah](https://github.com/mohamedabdallah20)

any program that is running in the system is a process.

## types of processes

* **FOREGROUND** \(interactive process\)
* **BACKGROUND** \(un-interactive process\)

### Status of a process

During execution, a process changes from one state to another depending on its environment/circumstances. In Linux, a process has the following possible states :

* **Running** it's either running or it's ready to run
* **Waiting** in this state, a process is waiting for an event to occur
  * interruptible -> can be interrupted by signals
  * uninterruptible -> are waiting directly on hardware conditions and cannot be interrupted by any event/signal.
* **Stopped** in this state, a process has been stopped, usually by receiving a signal.
* **Zombie** here, a process is dead, it has been halted but it’s still has an entry in the process table.

# ps command

it's abbreviation to *process status* <br>

* *PID*-> process id.
* *TTY* -> the typeof terminal that the user is logged in to.
* *Time* -> time in minutes and seconds that the process has been running.
* *CMD* -> The command that launched the process.<br>
you can see man page to see the \[options\]

# _top_ command

it's like *PS* CMD put it's dynamic real-time view of the running processes	

* PID -> process id.
* PR -> priority of the task.
* SHR -> the amount of shared memory used by a task.
* VIRT -> Total virtual memory used by the task.
* USER -> User name of owner of task.
* %CPU -> the CPU usage.
* TIME+ -> CPU Time, the same as ‘TIME’, but reflecting more granularity through hundredths of a second.
* SHR -> Shared Memory size \(kb\) used by a task.
* NI -> a Nice Value of task. A Negative nice value implies higher priority, and positive Nice value means lower priority.
* %MEM: Shows the Memory usage of task.<br>
you can press H or ? to show the show Help for Interactive Commands <br>
you can see man page to see the \[options\]

# _HTOP_ command

it's like *top* command, but offers many improvements. 

```bash sudo apt install htop ```

* it's supports mouse operation
* uses color in its output
* gives vital indications about processor, memory and swap usage
* prints full command lines for processes
* has no man page
you can press H,? to show the show Help for Interactive Commands 

# SIGNALS 

The fundamental way of controlling processes in Linux is by sending signals to them.
there are many signal that you can sed to process , run **_kill -l_** to list all signals
use **use _kill_ to send signals** 
*kill \[signal_number\] PID* 

# helpful Command lines

* **pgrep** grep the pid with specific criteria
* **pkill** kill the specific process by it's name
* **killall** kill the specific process by it's name


