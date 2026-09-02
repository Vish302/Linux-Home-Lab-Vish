# Day 4 - Processes and Services

## General Summary

---
## Processes
A process is a program that's currently being executed. For example, having an instance of a browser, a video game, or even the terminal open makes it a process. In any given system, dozens if not hundreds of processes are running at once, some used by the system to maintain itself, others by users to do tasks.

Processes are uniquely identified by their PID (i.e. 1, 2, 3). These IDs are used universally in the system to represent the process, and are used when we run commands on the process, such as kill.

When working with a system's security, it's good have a general idea of what processes are running on it at any given time. This is because one way attackers can get into a system is through false processes, pretending to be something important while your data is secretly compromised. As such, we use the following command to check what processes are running in a system:\
```$ps aux```\
or\
```$ps -ef```

A natural question that might arise might be why there are two commands for this task. Well, that's because despite both showing a list of processes, they both tell us different things about the process.

If you want to know how much a process is using in terms of resources, aux is the tool to use. It lists all the processes running, their CPU usage, as well as their memory usage.

If instead you want to know what process spawned the current process (that is, its parent processes), -ef is better. These are just flags, the e flag standing for "every" and the f flag for "full".

When using ps, if you want to sort the processes list by a certain factor, you can use the sort flag:\
```$ps aux --sort=[label] (i.e. %cpu)```\
or, if you're sorting by multiple values:\
```$ps aux --sort=[label],[label]```\
NOTE: some flags have -- due to being longer than one letter.

---
## Working with Processes
