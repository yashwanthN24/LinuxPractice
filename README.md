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



