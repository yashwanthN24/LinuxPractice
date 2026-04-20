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

---

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

---

## Types of files in Linux 

| File Symbol | File Type |
| --- | --- |
| - | Regular File |
| d | directory |
| l | Link |
| c | Device File |
| s | Socket |
| p | FIFO or Named Pipe |
| d | Block Device |

**s socket** 

- Special file to enable communication between two processes 
- find under /run 

**p FIFO or Named-pipe** 

- Sends data from one process to another so that the recieving process reads the data first-in-first-out manner
- can be created using `mkfifo` command

**b block device file** 

- A file that refers to a device.
- Find under /dev/ 
- Ex: /dev/sda1 

`fdisk -l` 
- The command fdisk -l is used in Linux to list all available disk partitions and their details

**c character device file** 

- we can create using `mknod` command. 
- These files are present in /dev folder
- File that reads/writes data in character by character
- Ex: /dev/input/mouse2 ( A mouse device that provides character input )

---

## Nano Editor 

`nano  filename` - To open the file with nano editor 

- Unlike Vim Motion or Vi editor you can start editing directly dont need to press i and all 

```bash 

ctrl + X # To exit 

ctrl + o # To write out to a new file and provide new filename it writes to that file very helpful for backups of current file 

ctrl + r # To Read other files content and paste them in current file in  nano editor and that file which we read also must be in the same directory 

ctrl + w # To search for a word in nano editor 

ctrl + \  
# To replace a word by other 

ctrl + k # To cut a line text 

ctrl + u # To paste a text

Alt + u # To undo 

Alt + e # To redo 

```

---

## Tee command in linux 

- Tee reads standard input and copies to both to stdout and to a file 
- we can see the information going through a pipeline T shaped

`ls | tee files.txt` 

**xargs** 

- It converts the stdinput to command line argument

```bash 

ls | echo # fails because ls provide the output as stdin to echo but echo doesnt take stdin instead it requires only command line arguments 

ls | xargs echo 

# so here the output of ls i.e sent as stdin to xargs that converts it to command line arguments and passes to echo hence it works fine 

ls | xargs echo h1 

```

```bash 

cat filenames.txt | xargs touch 

# or 

echo file{1..2} | xargs touch

echo file{1..5} | xargs rm

# because these commands require command line arguments only they dont take in stdinput and work on it 

```

---

# Understanding Linux Commands: Arguments vs. Standard Input (Stdin)

In Linux, not all commands are created equal. Some process the **content** of a stream (Stdin), while others only act on **filenames or IDs** provided as command-line arguments.

## 🚫 Commands That Require `xargs`

These commands ignore data coming through a pipe `|` because they do not read from Standard Input. They expect you to type the targets directly after the command.

| Category       | Commands          | Why they need `xargs`                  |
|----------------|-------------------|----------------------------------------|
| **File Management** | `rm`, `cp`, `mv`, `mkdir`, `touch` | They act on the **file object**, not the text inside. |
| **Permissions**    | `chmod`, `chown`  | They modify metadata; they don't read stream data. |
| **Process Control**| `kill`            | Requires a PID (number) as an argument. |
| **Output**         | `echo`, `ls`      | They print specific arguments or directory contents. |

## The `xargs` Bridge

When you want to pass the output of one command (like `find`) into a command that doesn't read Stdin (like `rm`), you must use `xargs`:

```bash
# This WILL NOT work (rm ignores the pipe)
find . -name "*.log" | rm

# This WILL work (xargs converts the pipe into arguments)
find . -name "*.log" | xargs rm
```

> **Use code with caution.**

## 🔍 How to Identify Them (The 3-Step Test)

As a beginner, you can use these tests to determine if a command needs `xargs`.

### 1. The "Blinking Cursor" Test
Run the command by itself and hit `Enter`.

- **Waiting for you?** If it sits there with a blinking cursor, it is waiting for Stdin (e.g., `grep`, `cat`, `sort`). You **do not** need `xargs`.
- **Errors out immediately?** If it says "missing operand" or prints a help message, it likely requires Arguments (e.g., `rm`, `cp`). You **do** need `xargs`.

### 2. The Logic: "Content vs. Container"
- **Content**: Does it look **inside** a file to search, sort, or change text? (e.g., `sed`, `awk`). → **Uses Stdin**.
- **Container**: Does it move, delete, or rename the **file itself**? (e.g., `mv`, `rm`). → **Uses Arguments**.

### 3. The `echo` Test
Pipe a random word to the command:

```bash
echo "test.txt" | ls
```

> **Use code with caution.**

If the command ignores "test.txt" and just does its normal job (like listing the whole folder), it doesn't support Stdin.

## 💡 Quick Summary for GitHub

- Piping (`|`) passes data to a command's **"ears"** (Stdin).
- `xargs` takes that data and puts it in the command's **"hands"** (Arguments).

---

## Grep Command (Global Regular Expression Print)


**Global Regular Expression Print** 
- Grep Command search for a particular string/keyword from a file and print lines matching a pattern 
- It check line by line and print lines matching given pattern 
- we can use grep anywhere like with files, searching for file, directories etc 

```bash 
    grep [Option] Pattern [File]

```

**Case 01** 

- To Ignore the upper and lower case while searching 

```bash 

    grep -i "keyword" file

```

**Case 02**

- To search everything except given pattern/keyword

```bash 

    grep -v "keyword" file

```

**Case 03** 

- To print how many times (count) given keyword present in file 

```bash 

    grep -c "keyword" file

    # Ex: grep -c doctor users.csv 

```

**Case 04** 

- To search for exact match of a given keyword in a file

```bash 

grep -w "keyword" file

```

**Case 05** 

- To print the line number of matches of given keyword in a file 

```bash 

grep -n "keyword" file

``` 

**Case 06** 

- To search a given keyword in multiple files 

```bash 

grep "keyword" file1 file2 

```

- Note: By default result of multiple files shows filename in output 

**Case 07** 

- To suppress file names while search a given keyword in multiple files 

```bash 

grep -h "keyword" file1 file2 


grep -ih merrry user.csv file.txt 

```

   
**Case 08** 

- To search multiple keywords in a file

```bash 

grep -e "keyword1" -e "keyword2" file


# Ex:   grep -ie merry -ie kara users.csv 

# i to ignore case

# or use egrep for searching multiple words in file 

egrep "Kara|merry|karly" users.csv 

```


**Case 09** 

- To search multiple keywords in multiple files 

```bash 

grep -e "keyword1" -e "keyword2" file1 file2 

```


**Case 10** 

- To only print file names which matches given keyword 

```bash 

grep -l "keyword" file1 file2 

# Ex:   grep -l Merry users.csv file.txt 

```

**Case 11** 

- To get the keywords/pattern from a file and match with a another file 

```bash 

grep -f keyword.txt file 

```


**Case 12** 

- To print the matching line which start with given keyword 

```bash 

grep "^keyword" file 


```

**Case 13** 

- To print the matching line which end with given keyword 

```bash 

grep "keyword$" file 

```

**Case 14** 

- Suppose we have 100 files in a directory (dirA) and we need to search a keyword in all the files 


```bash 

grep -R "keyword" dirA/


# Ex: grep -R "Raju" test/ 

# or 

# Ex: grep "Raju" test/* 

# Searches for all files inside test directory for Raju word

```

**Case 15** 

- We can use  egrep command for the multiple keyword search 

```bash 

egrep "key1|key2|key3" file 


```


**Case 16** 

- If you just wanna search but dont want to print on terminal 

```bash 

grep -q "keyword" file

# after this you can check the status (exit status ) of this command via $? if its 0
# successful or else unsuccessful this way you can take decisions in shell scripts  

```

- If you want to suppress error message 

```bash 

grep -s "keyword" file 

```


```bash

ls | grep -i file


```

**egrep** 

- To search multiple files 

```bash 

egrep "kara|karley|kindley" users.csv 

```

**pgrep** 

- To search based on process name and gets its process id 

```bash 

# Before 

ps -ef | grep nginx 


# after

pgrep nginx 

```

**fgrep** 

- To search for a word excluding regex characters like . * in words 

```bash 

fgrep hello.world file1.txt 

# in grep you have to use -w 

grep -w hello.world file2.txt 

```

**zgrep** 

- zgrep is used to search in gz archive files grep wont work on such files 

```bash 

zgrep sara users.csv.gz 

```


**pdfgrep** 

- You can grep and search words in pdf files so we have to use `pdfgrep` to search for words in pdf files 

```bash 

pdfgrep "dummy" dummy.pdf 

```

--- 

## Linux wildcards 

- wildcards are special characters that represent one or more characters in filenames or commands , allowing users to select multiple files at once 


| Symbol | Meaning | Example |
| --- | --- | --- |
| * | Matches any number of characters, including none | *.txt matches all files ending with .txt |
| ? | Matches exactly one character  | file?.txt matches file1.txt , file2.txt etc  |
| [] | Matches any of the enclosed characters  | file[12].txt matches file1.txt and file2.txt only |
| {} | Matches a group of patterns | file{1,2}.txt matches file1.txt and file2.txt |
| ^ | Matches the start of a line  | ^Hello matches any line starting with hello |
| $ | Matches the end of line  | world$ matches any line ending with world  |

```bash 

ls *.xml # matches all files having .xml extension 

ls *.yml 

ls *.jpg

```


**Case 01** 

- How to find all the xml files in a directory

```bash 


ls *.xml 


```


**Case 02** 

- Create 20 files like file1 , file2 ... file20 


```bash 

touch file{1..20}

# here 1..20 (provide number range from 1 to 20)

```

**Case 03** 

- Find all the files whose name is exactly 4 characters ex a123 , test ... 

```bash 


ls ????

```

**Case 04** 

- Find all the files with name _123 (where _ can be any character) 

```bash 

ls ?123 

``` 

**Case 05** 

- Find files whose name start wth a , b or c 

```bash 

ls [abc]*

```


**Case 06** 

- Find files which includes numeric value 

```bash 

ls *[0-9]*


```


**Case 07** 

- Find all files that start with "test" and have exactly 6 character in their name (eg: test01 , test99)

```bash 

ls test??

```

**Case 08** 

- Find all the files that have atleast one underscore in their name 


```bash 

ls *_*

```


**Case 08** 

- List all files that do not contain the letter "e" in their name 

```bash 

ls | grep -v "e" 

# grep -v means except the pattern get all match  

```

**Case 09** 

- Find all files that start with a capital letter [A-Z]

```bash 

ls [A-Z]*

```

**Case 10** 

How would you list all files that start with the letter "a" and end with .sh in the current directory 


```bash 

ls a*.sh

```

**Case 11** 

- What command would you use to move all the files with a .jpg extension to the images directory 


```bash 

mv *.jpg images/ 

# or

mv *.jpg images 

```

**Case 12** 

- How can you delete all the files that have "backup" somewhere in their filename 


```bash 

rm *backup* 

```


```bash 

grep ^R users.csv # find all lines that start with R 

grep .com$ users.csv # find all lines that end with .com 

```

**Case 13** 

- How would you use grep to find lines that start with "Warning" in a log file

```bash 

grep ^Warning userlog.log 

```

**Case 14** 

- What regex pattern would you use with grep to find all lines containing an email address in a text file ?

```bash 

grep .com$ user.txt 

```

**Case 15** 

Write a grep command to find lines that contain a date in the format YYYY-MM_DD in a file 

```bash 

grep -E '\b[0-9]{4}-[0-9]{2}-[0-9]{2}\b' filedates.txt

```

--- 

## Linux Redirection 

- Use casees 

    - Merging multiple files into a single file 

    - Split a big file into a small file with relavent data 


```bash 

cat file1 

cat fil2 

cat file1 file2 


cat file1 file2 > file3 # Combines file1 and file2 and stores its output in flle3 

```

**Type of redirection** 

- Standard Input (Stdin)
- Standard Output (Stdout)
- Standard error (Stderr)

**File Descriptors** 
    
    In Linux , a file descriptor is an integer that represents an open file. There are three standard file descriptors: 

    1.Standard Input (stdin) File Descriptor 0 
    2.Standard Ouput (stdout) File Descriptor 1 
    3.Standard error (stderr) File Descriptor 2 

    These descriptors help the system understand where to send or recieve data 


**Stdout 1** 

- Output of a command is shown in terminal 
- To route output in file using > 

    `hostname > file_name`

- To append output in existing file using >> 

    `pwd >> file_name`

**stderr - 2** 

- if any command gives you error then it is considered as stderr - 2

- we can direct the error to a file 

    `cd /root 2> error_file`

- To redirect both standard output and error to a file 

    `cd /root > error_file 2>&1` 

    or 

    `cd /root &> error_file`

    `ls &>> error.txt`


**Stdin - 0** 

- Input is used when feeding file contents to a file 

- cat < filename 

- cat << EOF 

- cat data.csv (is same as cat < data.csv so its bydefault stdin)

## Linux A-Z 

**A** 

- awk : A powerful programming language used for pattern scanning and processing
- alias , apt (Package manager on Debian/Ubuntu) , at (Automation One time task scheduling) 

**B** 

- bg: Puts a job in background 
- bc : binary calcy (calculator)
- bash : The Bourne Again Shell, a widely used command interpreter

**C** 

- chmod : changes the file permissions 
- chown (change ownership) , chgrp (change group) , cp (copy) , cal (calendar) , curl (For http requests )


**D** 

- df : shows disk space usage 
- du (disk space utilization by a directory) , diff (To see diff between two files) , date 

**E** 

- env : Displays the environment variables 
- echo (To output on terminal) , export 

**F** 

- find : Searches for a file in a directory hierarchy 
- file (Tells the type of file) , fg (Foreground) , free (Memory usage RAM )

**G** 

- grep : Searches files for a specified pattern 
- gzip , groupadd 

**H** 

- history : Shows the command history 
- head (To get specfic number of line from start of file) , hostname (Machine name)

**I** 

- ifconfig : Configures or displays network (used to see ipv4 address of the machine)
- ip , id , iptables 

**J** 

- jobs : Lists the current jobs 

**K** 

- kill : Sends a signal to a process 

**L** 

- ls : lists directory contents and files 
- less , ln (soft link and hard link (shortcuts)) , locate (To find a file faster via db)

**M** 

- mkdir : Create directories 
- mv (move/cut-paste/rename) , more (page view on large files)

**N** 

- netstat : Prints network connections , routing tables , interface statistics , masquerade connections , and multicost memberships 
- nano (Editor) , nice (Running command with specific priority)


**O** 

- openssl : toolkit for the transport layer Security (TLS) and secure sockets layer (SSL) protocols 

**P** 

- ps : Reports a snapshot of the current processes 
- printenv (Print environment variables same as env) , pwd (Print current location path) , passwd (To set password of user)

**Q** 

- quota : Displays the disk usage and limits for a user or a group. 

**

**R** 

- rsync : Fast and versatile file copying tool 
- rm (remove file) , rmdir (remove directory) ,  reboot 

**S** 

- sudo : Allows a permitted user to execute a command as a superuser or another user 
- sed , sort , systemctl 

**T**

- top : Displays all Linux task in real time CPU , memory stats 
- tail , tar , tee , touch , telnet (older now use SSH as credentials are encrypted)

**U** 

- uniq : To get the unique values 
- useradd (add new user) , umask (default permission to files and directories) , usermod (Modify user) , umount , uname (system info os diastro type)


**V** 

- vi or vim: Text Editor

**W** 

- wget : Non-interactive network downloader 
- wc , whoami , which , whatis , who , w

**X** 

- xxd : creates a hex dump of a give file or standard input 
- xargs : To convert stdin to command line arguments used in piping 

**Y** 

- yum : Interactive , rpm-based package manager (Used in Red Hat-based systems RHEL)
- yes 

**Z** 

- zip : Package and compress (archive) files 


--- 

## ps 

To see processes by username

`ps -u username` 

`ps -G groupname`

To see the proces tree 

`ps -ejH`

To see all the running processes 

`ps -e`

`ps -A`

`ps -ef` (For full format)

To see all the processes in BSD (Berkeley Software Distribution) format 
Ideally it gives you more information 

`ps aux`

--- 

## kill 

- `kill` command is used to terminate a proces manually 

    Syntax

    kill [Options] [Pid]

    Options = Signal name or no 
    PID = Process ID 

- To see all the signal names 

    `kill -l`

- Most widely used commands 

    ```bash 

     kill PID 

     kill -1 PID #  (To Restart the process)

     kill -2 PID # (interrupt from keyboard like Ctrl + C)

     kill -3 PID # (forcefully terminate the process)

     kill -15 PID # (kill process gracefully)

     kill -9 PID # To force kill the process

     ```

# Top command 

- The top (table of processes) command shows a real-time view of running processes 
in linux and displays kernal managed tasks 

- The command  also provides a system information summery that shows resource utilization , including CPU and memory usage 

- top then c = Shows the commands absolute path 
- top then k = kill a process by PID 
- top then n = To change the no of task displayed 
- top then d or s = to change interval of refresh 
- top then M = To sort the Linux running process by memory usage 
- top then r = you can change the nice value (priotity) of a PID 
- top then u = To filter task by user 
- top then f = Field management 
- top then h = help 
- top then z or b = Toggle 'z' color/mono , 'b' bold/reverse 
- top then x , y = x sort field , y 'running tasks' 
- top then i = process which some memory usage 


## Log monitoring 

`cat /var/log/data.log/ | more` for a pageable view 

`tail -f /var/log/cron.log | egrep "error|warning"` Shows only error/warning logs in real time 

`cat error.log | grep error | wc - l` (Counts the number of lines having error so those many errors) 


