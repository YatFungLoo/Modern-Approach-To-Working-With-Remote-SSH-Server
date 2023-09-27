# A modern approach to working with SSH remote server

- [A modern approach to working with SSH remote server](#a-modern-approach-to-working-with-ssh-remote-server)
  - [Introduction](#introduction)
  - [SSH Protocol](#ssh-protocol)
    - [Using SSH (Password)](#using-ssh-password)
    - [Using SSH (SSH key-pair)](#using-ssh-ssh-key-pair)
  - [Vim vs Emacs](#vim-vs-emacs)
  - [Some life improvement things](#some-life-improvement-things)

## Introduction
My friend is starting her new job that does all the work on a personal remote server that connects via SSH ([Secure Shell](https://phoenixnap.com/kb/what-is-ssh)). Coming from an engineering background that does minimal coding where I started a course on high-performance computing in 2022 I lived in the SSH server for a year, I would like to share things that I have learned from the past year for anyone in a similar situation to get quickly get used to and get familiar with working on one! Very basic computer experience (opening Powershell as admin, installing applications) required.

## SSH Protocol
Working on a thin-and-light laptop while having the power of a supercomputer on it is the reason why you come across SSH protocol, as a TLDR; it allows you to control a server (think of it as a separate computer) to run build and run code. The protocol goes quite in-depth and since it is not the focus of this guide, I recommend Googleing about it and have a read on any website about it.

Available on both Windows (Powershell and CMD) and Linux, you can type the following in your favorite terminal:

```ssh --V```

to check the version (-V stands for version, which is called a flag) of the SSH program, it should come pre-installed in both Windows and Linux but if it is not, please refer to the most updated documentation you can find online to install one.

### Using SSH (Password)
You should be given a username, IP address (or domain name) and password for your server. With this info and the SSH program installed in your system, you are already ready to connect to your server! As an example, my details will be in the following table:

<!-- create a table -->
| Username | IP address | Domain Name | Password |
| -------- | ---------- | -------- | -------- |
| Dexter   | 123.123.123.123 | F00BAR.com | 12345678 |

To connect to your server, you can type the following in your terminal:

```ssh <username>@<IP address>```
as in
```ssh Dexter@123.123.123.123```

or

```ssh <username>@<Domain Name>```
as in
```ssh Dexter@F00BAR.com```

Then it will prompt you to enter a password, once it is entered you will be officially connected to the server! It will most likely be running Linux so learning a few commands to move around (creating a directory, link to the path, .bashrc all that great stuff) will be very helpful.

To change the password of your login, use the following:

```passwd```

which will ask for your current password and the new password you want, which is very handy when the IT department sets your password to 1234.

But having to enter a password every time you want to connect to the server (including reloading Windows VSCode) is a harder task than understanding recursive function, in the following section I will write about how to use ssh key-pair to connect to the server that can eliminate entering password every time.

### Using SSH (SSH key-pair)
SSH key-pair as the name suggests is two files that can be generated via your favorite terminal (providing it has the SSH program installed). But before getting started here, I recommend installing [MobaXterm](https://mobaxterm.mobatek.net/download-home-edition.html). It is a better terminal on Windows with X11 support (it means it can display graphic stuff outside of the terminal) with remote file editing features, and the most important part it is extremely popular (any problem you face you can solve it very quickly and get work done).

Once you installed it you can use it as a normal terminal (you can try to ssh into your server again with a password).

Going back on track, generating an SSH key-pair will create two files under the ```.ssh``` directory (for windows: C:\Users\${user_name}\\.ssh, if you are new to Linux use the ```-la``` to see the directory since the dot indicate it is hidden). By default it will be id_rsa and id_rsa.pub, which we call the the former private key and the latter public key. The idea is basically you will give the server your public key (can think of it functioning as a lock) and when you try to ```ssh``` into said server ```ssh``` itself will look for yor ```.ssh``` directory for the private key to unlock your way into the server.

> Note: SSH key-pair ARE reuseable for multiple server! (i.e. same id-rsa pair for infinite different servers)

To generate a generic SSH key-pair (without email), use:

```ssh-keygen```

> Please refer to the document given to use as different server setup has different procedure, this should work for my friend 

And press enter and yes to everything until it reaches the create password prompt, it is generally a very good idea to have a password for the key pair, but it can be blank if you want to SSH without entering a password.

Then you will need to put this key to the server:

```ssh-copy-id <username>@<IP address>``` as in example ```ssh-copy-id Dexter@123.123.123.123```

or

```ssh-copy-id <username>@<Domain Name>``` as in example ```ssh-copy-id Dexter@F00BAR.com```

Once you enter the password for the server, you will be able to ```ssh``` into the server with the private key, enter "yes" for fingerprint and you are set! You can now enter the server quicker than before (depending on the password you chose). Note that you can actually ```cat``` or ```more``` or ```less``` to see the content of the public key.

Now you are in! But providing you have to read this (no offence haha) weekly team meeting is in two days you are probably not going to develop code in the terminal I will introduce a few different paths that I have taken and tools that I have come across that can save you a lot of time.

## Vim vs Emacs 
Just use vscode!

.

.

.

(It's a joke) but learning the basics of Nano / Vi / Emacs is very good and using one of them along with VSCode is a very good idea (getting good at vi or emacs binding on VSCode is also very helpful when you get good at them!)
The most common setup I have come across are either:

1. Windows: MobaXterm (or quick terminal access / quick edit with Vi) + VSCode (with as many plugins as you can install to it) for actual developement
1. Windows: WSL + VSCode (recommend if you are allowed to install things on your company laptop)
1. Linux: Full Neovim setup or old-school Emacs or VSCode

I would not discuss Vim in detail, however, I would do so for VSCode as it is very popular (easy to fix the problem).

To connect to your server via SSH, providing you created your key-pair already you can install these plugins:

1. Remote - SSH
1. Remote - SSH: Editing Configuration Files
1. Remote Explorer

and the plenty of extensions that are available for your language.

There are plenty of tutorials online to get you started on these, so I will be ending the tutorial here.

## Some life improvement things
This is a do-to list of sorts when you are more familiar with Linux. You should look into it yourself and it will be more fun that way.

1. to customize your bash: edit .bashrc and source it
1. to avoid typing a lot: create a .bash_alias and bash something
2. learn all the bash shortcuts (C-a C-e C-r etc.)
3. something to practice: awk sed grep and makefile
4. to keep your terminal alive forever (and to look cool): use Tmux
to find the file quickly: fzf
1. to manage server files: sshfs and sftp
2. to become a rust developer: Neovim with arch
3. to become an old-school: Emacs
4. and many many more!

Remember to keep trying new things (like vi and emacs) that give you a new perspective on not only software engineering but life in general! Keep exploring and be open-minded, wish you the best on the job and may we see again.
