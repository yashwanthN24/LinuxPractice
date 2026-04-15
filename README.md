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
tcp lets you analyse network packets and diagnosing the connectivity issues 

use `sudo tcpdump -i enX0 port 80`

ping www.google.com (To test server connectivity and dns resolution and see if we are recieved packets from the server _ 

traceroute   to check the  latency that can occur in trasfer of packets between different hops between your ip to the destination ip 

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

