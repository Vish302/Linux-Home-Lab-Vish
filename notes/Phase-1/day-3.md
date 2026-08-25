# Day 3 - Understanding users and permissions

## General Summary

---
## Adding Users and Groups
When using a certain Linux machine, you may want more than just one user. In these cases, Linux allows you to add just that: more users. So, how do we do it?

It's actually a very simple command:\
```sudo adduser [username]```

This command adds a user to the Linux machine, giving them a unique home directory that only they and the root user can access. Every user will also stay independent of each other and can interact in a multitude of ways.

Now, lets say you wanted to see who all the users are in a specific Linux machine. How would we do this? Well, we make use of /etc/passwd. If we recall back to day 2, we'll remember that etc held config files. One such file, /passwd, holds the data of every user registered on the system, including people as well as system users. To filter for just the people, we run the following command:\
```cat /etc/passwd | grep home```\
This command will return a list of the users listings that have home in them, which is only real people.

To switch between users, we make use of the su command:\
```su [username]```

If there were tons and tons of users, how does Linux manage them? How does it know who is who? Well, Linux makes use of an ID system, assigning each user a corresponding UID.

Another important part of the Linux system is the group system. Users are important when certain people need specific perms that allow them to fulfill their task. Groups are important when this burden lays on a specific role.

Making groups is also a simple, single-line task:\
```sudo groupadd [group name]```

To then add a specific user to a group, you do the following:\
```sudo usermod -aG [group name] [username]```

---
## Files and File Permissions

---
## Sudo