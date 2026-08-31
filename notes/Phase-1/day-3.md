# Day 3 - Understanding users and permissions

## General Summary
Today was a study on users, groups, and files. We took at a look at how we can manipulate and inspect users, then moved to files and file permissions. Finally, we took a quick look at Sudo.

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

Now, files and permissions can be given to groups of people rather than specific members. This not only saves a lot of time initially when adding permissions, but it also saves time in the future, when members need to be added or removed from the group.

---
## Files and File Permissions
Files can be made by any user using the touch command. However, when making a file, it has certain permissions on who can read, write, and execute it. To check these permissions, we do the following command:\
```ls -l [file name]```

This will output a line of text that looks something like this:\
```-rwxrw-rw-...```\
These 10 characters are called permission bits, and they show what level of permission a certain category of users have in regards to that file.

The first bit is used to classify the file. For example, - is a regular file, whereas d is a directory, etc. The next 3 bits are the user permission bits. The first of the three is the read bit, denoted by the r. The second is the write bit, denoted by the w. Finally, the last one is the execute bit, denoted by the x.

The second set of three represent the same type of bits, but represent group permissions. The last three represent everyone else's permissions.

For any given file, permissions can be changed using the following command:\
```chmod [permission number] [file name]```\
Where the permission number is a 3 digit number based on the permission bits between 777 and 000. The first digit is the permissions of the owner, the second the group, and finally everyone else.

You can also use another approach with chmod:\
```chmod [u, g, o, a][+, -, =][rwx] [file name]```\
Where the first letter is who you're changing permissions for (u = user/owner, g = group, o = others, a = all), whether you're adding, subtracting, or equating, and what permission.

Depending on what permissions you set, various different users can interact with the file. However, it's important to note that it's not just the file permissions that determines how someone interacts with a file. The permissions of the directory it's in is important too.

Of course, file permissions can only go so far. If necessary, another option is to change the file's ownership using the following command:\
```sudo chown [username] [file name]```\
NOTE: sudo is required here because only the root user can change file ownership

To change a file's group, you use the chown command as well:\
```sudo chown [username]:[groupname] [file name]```\
or\
```sudo chown [username]: [file name]```\
if you wanted to have the file take the group of the user.

To move a file, we use the mv command as follows:\
```mv [file name] [new directory]```

---
## Sudo
The sudo command allows any user to act as the root user. The root user is the most powerful user in a Linux system, and they have complete permissions over all the services on the machine, so being logged in on it the entire time is a security issue. 

Most every day tasks don't require the root user's power, but for those that do, the sudo command make it easy to execute them without being the root user yourself.

Limiting control of the root user, only granting permissions to those who really need it is one of the biggest jobs of a cybersecurity professional.