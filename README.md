# ShellLab
A simple Unix shell program that supports job control. The tsh.cc file contains all functions written to create the shell program. The 
others contain the files needed to build the shell program and were not written by me. This was made as part of the "Computer Systems" 
class at CU Boulder in fall of 2018. The command "make testX" (Where X is a number from 1-16)

Background of how a shell operates: 
A shell is an interactive command-line interpreter that runs programs on behalf of the user. A shell repeatedly prints a prompt, waits for a command line on stdin, and then carries out some action, as directed by
the contents of the command line.
The command line is a sequence of ASCII text words delimited by whitespace. The first word in the
command line is either the name of a built-in command or the pathname of an executable file. The remaining
words are command-line arguments. If the first word is a built-in command, the shell immediately executes
the command in the current process. Otherwise, the word is assumed to be the pathname of an executable
program. In this case, the shell forks a child process, then loads and runs the program in the context of the
child. The child processes created as a result of interpreting a single command line are known collectively
as a job. In general, a job can consist of multiple child processes connected by Unix pipes.
If the command line ends with an ampersand ”&”, then the job runs in the background, which means that
the shell does not wait for the job to terminate before printing the prompt and awaiting the next command
line. Otherwise, the job runs in the foreground, which means that the shell waits for the job to terminate
before awaiting the next command line. Thus, at any point in time, at most one job can be running in the
foreground. However, an arbitrary number of jobs can run in the background.

Specifications: 

• The prompt should be the string “tsh> ”.
• The command line typed by the user should consist of a name and zero or more arguments, all separated by one or more spaces. If name is a built-in command, then tsh should handle it immediately
and wait for the next command line. Otherwise, tsh should assume that name is the path of an
executable file, which it loads and runs in the context of an initial child process (In this context, the
term job refers to this initial child process)
•Typing ctrl-c (ctrl-z) should cause a SIGINT (SIGTSTP) signal to be sent to the current foreground job, as well as any descendents of that job (e.g., any child processes that it forked). If there is
no foreground job, then the signal should have no effect.
• If the command line ends with an ampersand &, then tsh should run the job in the background.
Otherwise, it should run the job in the foreground.
• Each job can be identified by either a process ID (PID) or a job ID (JID), which is a positive integer
assigned by tsh. Job ID’s are used because some scripts need to manipulate certain jobs, and the
process ID’s change across runs. JIDs should be denoted on the command line by the prefix ’%’. For
example, “%5” denotes JID 5, and “5” denotes PID 5. (We have provided you with all of the routines
you need for manipulating the job list.)
• tsh should support the following built-in commands:
  – The quit command terminates the shell.
  – The jobs command lists all background jobs.
  – The bg <job> command restarts <job> by sending it a SIGCONT signal, and then runs it in
  the background. The <job> argument can be either a PID or a JID.
  – The fg <job> command restarts <job> by sending it a SIGCONT signal, and then runs it in
  the foreground. The <job> argument can be either a PID or a JID.
• tsh should reap all of its zombie children. If any job terminates because it receives a signal that
it didn’t catch, then tsh should recognize this event and print a message with the job’s PID and a
description of the offending signal.
