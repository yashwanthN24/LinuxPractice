# LinuxPractice
This repo contains all useful Linux commands for day to day tasks and some cool linux commands 


## 10 most important Linux Commands 

**top** 

- k - to kill the process id 
- u - to get user specific process details 
- r - reniece to change priority of a process (least the number higher priority starts from -20)
- Shift+o => Then type the fiilter like PID=121 (To get details of process id 121)

`top -p <specific_pid>`

`pgrep <process_name>`



`top -p $(pgrep nginx)` 

or 

`pgrep nginx` 

`top -p $(pgrep dockerd)` 

z to toggle color coding in top output qq

`htop` 

`ps aux`  (to show all running processes) (ps is not real time like top command) used in shell scripts 

`ps aux | grep nginx` 

or if you already know the process name 

`pgrep nginx` 

`pstree -p`  (You can see hierachy of all the processes)

`pstree processname` (like pstree java)

**Network trobleshooting** 

- netstat (To check if a port is available or not )

```bash 
netstat -tuln
 # shows all ports already in use so that you can use a different port or kill those ports and reuse them for your application
```
Lets say you have a situation wherein the client complaints that there is a latency in  the response 
tcpdump lets you analyse network packets and diagnosing the connectivity issues 

use `sudo tcpdump -i enX0 port 80`

ping www.google.com (To test server connectivity and dns resolution and see if we are recieved packets from the server  

traceroute   to check the  latency that can occur in transfer of packets between different hops between your ip to the destination ip 

traceroute www.google.com 

disk utilization 

df -h 

if i have to check the size that a directory is taking 

du -sh directorypath 

du -sh opt

free -h (To check memory utilization) 

journalctl (very important when dealing with services , say you have nginx service and want to check its logs , these services are run by systemd  

journalctl -u nginx (shows the logs of nginx service) 

journalctl -u nginx -f (to show float logs in real time of nginx service) 

journalctl -b  (to check the logs from the boot time onwards) 

lsof -i :port (to find which app is using this port) 

tail -n 10 /var/log/auth.log (To see last 10 lines of this log file) 

head -n 10 /var/log/auth.log (To see first 10 lines of this log file) 

tail -f /var/log/auth.log (To see real time floating logs of this file) 

Shortcuts 

history => To get back all commands executed in past say you dont remember the command but you know its something related to export 

press ctrl + r to search start typing export Keeping pressing ctrl + r till you get the exact match one you found right arrow and enter done 

instead of doing `history | grep export`

then for changing the ui the name that gets displayed change `export PS1="yashwanth $PWD`



apt is the default package manager in debian based systems like Ubuntu OS 

apt list (lists all packages installed already in this system) 

apt update (To update all packages on this system keeping olderversion as well for reverting back to old version) 

apt install python3 (To install python on ubuntu system must have sudo permission or must be a root user to install packages)

ncdu (modern for seeing disk utilization of a directory instead of using du -h directorypath ) 

tldr commandname (to get the most used versions of the command for quick learning instead of man command and --help flag on command)

rg (to quick search for specific words across files) 

fzf - For searching files faster than locate and find 

bat - to read file content with color formatting and numbers instead of traditional cat command 

ranger (To understand any big codebase very easily instead of installing vscode ) from terminal itself better style liek vscode to understand files better 

glances (For system monitoring (advanced version of the top command) )


## Productivity Tips in Linux 

**Case 01** 

#### Tab for Autocompletion 

    Suppose you want to go to directory cd home/paul/tutorials we can use Tab for autocompletion which will speed up the task and reduces chances of errors 

**Case 02** 

#### Switch to the last working directory 

    cd - 

**Case 03** 

#### Running multiple commands in one line using ; 

```bash    
 Command1 ; command2 ; command3
# Here each command run irrespective of it previous command's output regardless of an error

 command1 && command2 
# Here 2nd command will run only if 1 was successful

 command1 || command2 
# Here command2 will run only if command1 fails 
```

**Case 04** 

```bash 

#To Read big files cat is not a good option; better to use less 

less csv  # we can easily search and navigate, go to top and end of the file 

# use arrow keys to navigate 

# / for forward search and ? for backward search 

# p to go to the start of the file

# Shift + g to go to the end of file 

```

**Case 05**

```bash 
# Empty a file without deleting it : 
 `
> filename`  

# This will empty the file without deleting it 
```

**Case 06** 

```bash 

tail -f | grep "error" # for live monitoring file with given text

# or 

sudo tail -f filename  # if your non-root but have sudo access

```

**Case 07**

```bash 

# To Record all the commands executed in a script 

script 

# Then perform all the tasks -> Ctrl + D to stop the script 

# If your trainer , boss , collegue teach you a process then we can record it using this 

script commands.txt

``` 

**Case 08** 

```bash 

# terminal as calculator 

bc -l # quit to exit 


#  w , who these two commands show logged in users list details 

# whoami - shows the current login user (effective username of the current user in the shell.)

# which -To get the path of the binary of a software 

where ls # gets the path of the ls executable useful for PATH configurations and debugging 

whatis ls # short description of the command from the manuel of the command man 

wc filename # word count (Counts lines , words and bytes)

wc -l filename # counts the lines from the filename 


```


**Case 09**

```bash 

Ctrl + a: To move cursor to the start 

ctrl + e: To move cursor to end 

```

```bash 

Ctrl + u: To clear the terminal 

Ctrl + y: To redo commands in the terminal 

```

**Case 10** 

```bash 

Ctrl + r : To reverse search for the commands we used ever 

Ctrl + l : Clear Screen 

``` 

```bash 

ctrl + d : to delete one character at a time from starting (opp of backspace)

cd ~ # To switch the path to home directory 

cd # also takes to the home directory 

cd /  #  takes to the root directory 

``` 

```bash 


history # history command to see all the commands executed frequently 

cp file1 ~ # means copy file1 to home directory 
# instead of saying 

cp file1 /home/paul 

# do 

cp file1 ~ # ~ represents the home directory of a non-root user i.e /home/username i.e /home/paul for example 


```



