# Day 4 - Processes and Services

## General Summary

---
## Processes
A process is a program that's currently being executed. For example, having an instance of a browser, a video game, or even the terminal open makes it a process. In any given system, dozens if not hundreds of processes are running at once, some used by the system to maintain itself, others by users to do tasks. 

When working with a system's security, it's good have a general idea of what processes are running on it at any given time. This is because one way attackers can get into a system is through false processes, pretending to be something important while your data is secretly compromised. As such, we use the following command to check what processes are running in a system:\
### ```$ps aux```\
or
### ```$ps -ef```