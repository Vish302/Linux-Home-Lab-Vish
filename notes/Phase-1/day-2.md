# Day 2 - Understand the file system and hierarchy

## General Summary
A summary on the file hierarchy system, including what each important directory holds and how the Linux system uses. Not too in depth, but deep enough to have a general idea.

Also, a bit of my insights on package installations, as this is something important to a lot of projects one could do. The package I downloaded was SSH.

Finally, a dive into understanding SSH and tunneling, whether it be public or private. I also looked into how the encryption works on a surface level.

---
## File Hierarchy
/bin -> Binaries, where things like commands are stored (ls, cat, etc). This specific directory holds what regular users use for tasks.

/sbin -> System Binaries, where commands used by the system are stored. Things like stop and start are here.

/usrbin -> User Binaries that are downloaded by the user. For example, git or any other popular library.

/boot -> Information needed by the Boot Loader to load the OS. Things like RAM, CPU, etc.

/dev -> Files for external devices connected to your system, because in Linux, external devices are treated as files.

/etc -> This is where system config files and scripts that you want to run on start up go. For example, /etc/passwd contains a list of all users on the system.

/home -> A user's home directory, where they keep all their personal files, code, and whatever else their heart may desire.

/lib -> Shared libraries go here, things like math.

/mnt -> Mounted drives go here. Don't worry about this too much it's for later.

/tmp -> Temporary files go here, things like cache. These get lost on reboot so they're very much temporary.

/var -> This is where files that change on runtime go. Similar to /tmp, but it's permanent in the sense that it never gets deleted.

/usr -> Where user applications and utilities exist.

---
## Package Installation
When installing packages, the commands you'll mostly use are:

`sudo apt update`\
and
`sudo apt install [package]`\

apt stands for advanced package tool, just as a fun fact.

So, why do we have do sudo apt update every time? Well it's because every time we run update, we get the newest installed packages. And, we don't necessarily have to do it every single time, but it's good practice to run it every few hours.

When doing sudo apt install, we can follow up the full command with a -y flag. This flag just means yes and answers Linux's are you sure you want to install this package question.

The reason why we need sudo for the apt commands is because we're changing more than just any given user's home directory. Usually, when using commands as a user, the only thing we can change is things in our home directory, but since packages go beyond that, superuser is required.

---
## Services
In any given Linux machine, there can be a multitude of services running at any given time. So, knowing how to tell when a service is running can be really helpful.

This is the following command that can tell you whether a service is running:\
`systemctl status [service-name]`

Should the given service you're looking at not in the state you want (started, stopped, etc), there are a few commands you can use to change that:\
`(sudo) systemctl start [service-name]` to start\
`(sudo) systemctl stop [service-name]` to stop\
`(sudo) systemctl restart [service-name]` to restart\

---
## SSH
Standing for Secure Shell, this package is a method used to connect to remote Linux machines. This is done through the use of an encrypted tunnel which connects your local machine to the server through a shell. It allows you to control the server as if you were a user working directly on the machine itself.

You can access the Linux Machine either through a password (unsafe and weaker, can be brute forced) or a private-public key pair (safe and strong, uses advanced mathematical cryptographic techniques). Just use the private-public key pair.

How the key pair system works is that every remote user has a public key saved within the server which they use to request connect. Then, based on the public key, the server sends the client an encryted message that only the corresponding private key can solve as a means to verify the client's identity.

To use ssh, we generate a key-pair on your local computer, which gives you both a public and a private key, which is done with the following command:
`ssh-keygen`

Then, take the public key and share it with whichever server you wish you remotely connect to. The private key must NEVER leave your local computer. Also, you're usually given the option to hide your private key with a passphrase. You should. It's just an extra layer of security. With the public key on your remote server, just add it to the authorized keys file on your machine (create if it doesn't exist).

Once you've manually set this up, you're ready to connect. To connect to the remote server, just run the following command:\
`ssh [serverip]`\
or if you have a different username on the server:\
`ssh username:[serverip]`

Your ssh connection can either be done through a public connection or a private one. With a public connection, you can connect from anywhere, but with a private network, you'd need a VPN or have to be connected to the same network.