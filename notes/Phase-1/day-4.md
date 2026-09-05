# Day 4 - Processes and Services

## General Summary
A study on processes and how they work. There's a lot of terminology in this one that will be reoccuring, so it's good to know now. There's also a study on process termination and reading.

---
## Concepts to Understand
Process - A program that a machine executes.

PID (Process ID) - An identification number used to identify processes.

Parent/child processes - When a process spawns another process, the spawner is the parent and the spawnee is the child.

Daemon - A process that runs in the background without user input (think system processes).

Service - Basically a Daemon but for Windows OS (Daemon is for Linux)

systemd - The initialization system that manages the system's tasks.

CPU usage - Portion of your CPU's working capacity that's currently being used to run tasks.

Memory usage - How much of your computer's Memory is being used to run tasks.

Signals - Messages used within the computer to communicate actions.

Terminating vs. killing a process - Terminate is a calm, gentle turning off of a process, whereas killing is abrubt and rough.

---
## Processes
A process is a program that's currently being executed. For example, having an instance of a browser, a video game, or even the terminal open makes it a process. In any given system, dozens if not hundreds of processes are running at once, some used by the system to maintain itself, others by users to do tasks.

Processes are uniquely identified by their PID (i.e. 1, 2, 3). These IDs are used universally in the system to represent the process, and are used when we run commands on the process, such as kill.

When working with a system's security, it's good have a general idea of what processes are running on it at any given time. This is because one way attackers can cause a lot of damage to a system through false processes, pretending to be something important while your data is secretly compromised. As such, we use the following command to check what processes are running in a system:\
```$ps aux```\
or\
```$ps -ef```

A natural question that arises might be why there are two commands for this task. Well, that's because despite both showing a list of processes, they both tell us different things about the process.

If you want to know how much a process is using in terms of resources, aux is the tool to use. It lists all the processes running, their CPU usage, as well as their memory usage.

If instead you want to know what process spawned the current process (that is, its parent process), -ef is better. It displays this through the PPID, which is the PID of the parent process.

When using ps, if you want to sort the processes list by a certain factor, you can use the sort flag:\
```$ps aux --sort=[label] (i.e. %cpu)```\
or, if you're sorting by multiple values:\
```$ps aux --sort=[label],[label]```\
NOTE: some flags have -- due to being longer than one letter.

---
## Working with Processes
Okay, so now we know how to get a list of all processes. However, what if we want to get a specific process, like say firefox? To do that, we use basic piping and the grep command:
```$ps aux | grep "firefox"```
This way, we can find the process for firefox using its name.

Now, what if we have a process we don't like? How do we get rid of it? Well, in Linux, there's a very simple command to stop a process:
```$kill [signal (by default it's -15, but if you -9 it'll abruptly stop the process)] [PID]```
Depending on the version of kill you use, you either terminate or kill the process. Since processes are a natural way of attacking a system, knowing how to get rid of a process is very important.