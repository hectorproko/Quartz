# Elective Courses

# Linux Training
## Module 1 - Introduction To Linux
### Basics of Shell
![[Linux Architecture.png]]
Seems like ~~applications commnicate with shell~~, shell talks to kernle, kernel talk to hardware? application talk directly to kernel #question 

Nowadays, We use a lot of GUI-based Linux distributions like CentOS. In these you have a terminal to contact the shell
- Terminals are software's which emulate a CLI Linux system
- A terminal which we see in a GUI server emulates a CLI Linux server
- Terminal emulators are more commonly used now due to GUI Operating Systems like Mac OS or Windows or Ubuntu GUI


### Top Shells in Linux
bash - The Bourne Again Shell is the default shell in a lot Of Linux distributions. It is the most portable shell available. Bash is the default shell of CentOS 8.

zsh - Z shell - It is similar to bash or an extended version of it. It has a lot of useful features like sharing your command history across multiple terminals

fish - Friendly and Interactive shell is again an extended version of the common shell. It has great features like autocompletion of commands

tcsh - Tenex C shell is an extended version Of C shell. The plus Of tcsh is its scripting language, because it will be similar for users with experience in C programming



### Basics Of Kernel
![[Pasted image 20230728095006.png]]

![[Pasted image 20230728095219.png]]
Look into [[System calls]] help execute process but also, used by kill?

### Lecture 4 - CentOS 8 Installation Part-1
### Lecture 5 - CentOS 8 Installation Part-2 And VBox Additions
yum update
dnf update
dnf install tar
dnf intall bzip2
dnf install kernel-devel  
or 
`sudo dnf install kernel-devel-$(uname -r)` 
*This command will install the `kernel-devel` package for the version of the kernel you're currently running.*

dnf install kernel-deaders
dnf install perl
dnf install gcc
dnf install make
dnf install elfutils-libelf-devel
To install the guest additions

### Lecture 6 - Basic Linux Commands
![[Pasted image 20230728110809.png]]
![[Pasted image 20230728110843.png]]

### Lecture 7 – Echo Command
![[Pasted image 20230728112256.png]]

![[Pasted image 20230728112800.png]]

### Lecture 8 – [[Set]] And [[Unset]] Variable
![[Pasted image 20230728113515.png]]

[[set vs export explanation]] maybe not needed?

![[Pasted image 20230728120701.png]]

![[Pasted image 20230728120839.png]]
You can make an existing variable global, with export

set shows you all the variable in the system?

`set` command, when used without any arguments, displays all shell variables (local and exported) and shell functions. This means it shows not just environment variables, but also all internal shell variables and functions.

`+o` and `-o` are options used with the `set` command to control shell behavior. They relate to shell options and provide a more readable method for enabling or disabling these options.

**Example**: To enable the `noclobber` option which prevents redirection from overwriting existing files, you can use:
```bash
set -o noclobber
```


### Lecture 9 – [[Expr]] Command
![[Pasted image 20230728130253.png]]
Found in the **man** page
![[Pasted image 20230728130415.png]]
![[Pasted image 20230728130503.png]]

`expr length $variable`, return the length or number of string in that variable


### Lecture 10 – Header Of A Shell Script
![[Pasted image 20230728131604.png]]


### Module 1 – Hands-On

> [!NOTE]- Basic-Unix-Commands.pdf
> ![[Basic-Unix-Commands.pdf]]

### Module 1 – Assignment #pending



## Module 2 - File Management

### Agenda (File Management)
Everything in linux is a file
### Lecture 1 – Text Editors And Creating A File
Most popular [[vim]] and [[emacs]]
![[Pasted image 20230728144528.png]]

Some vim commands
![[Pasted image 20230728144622.png]]

[vi video you found](https://youtu.be/-_DvfdgR-LA) #pending 


### Lecture 2 – Users, Groups And Processes
![[Pasted image 20230728145432.png]]

![[Pasted image 20230728145746.png]]

![[Pasted image 20230728145937.png]]
The file will not be available once deleted, but it will only fully deleted after process finishes, is in memory 
![[Pasted image 20230728223908.png]]

The 3 types of UID, find out #question 

### Lecture 3 – Root And The Linux File Hierarchy
![[Pasted image 20230728153017.png]]

### Lecture 4 – Understanding File Permissions
![[Pasted image 20230728162223.png]]

![[Pasted image 20230728162625.png]]
Think of Others as, processes, users that are processes
![[Pasted image 20230728162747.png]]

You can tell which user was created by a user because they UID start from 1000 as specify by /etc/login.defs
![[Pasted image 20230728163505.png]]

`gpasswd` used to add users to group? to control configuration in `/etc/group`

### Lecture 5 – Chmod And Chown

![[Pasted image 20230728192036.png]]

![[Pasted image 20230728192142.png]]

![[Pasted image 20230728192339.png]]


![[Pasted image 20230728192500.png]]


### Lecture 6 – Listing Files – The Ls Command
`ls -lh` show size in human readable like 4k 


### Lecture 7 – Metacharacters And Editing A File Using Vim

![[Pasted image 20230728210720.png]]
Here he describes the pipe as way to run multiple command in order, did nto mention how the output of one goes to the other


![[Pasted image 20230728210950.png]]
This work on the command mode

### Lecture 8 – Displaying Contents Of A File
![[Pasted image 20230728213733.png|450]]

These result in the same
```bash
echo "Current user: $(whoami)"

echo "Current user: `whoami`"
```

### Lecture 9 – Copying, Moving And Removing Files


## Module 3 - Files And Processes

### Lecture 1 – Everything Is A File In UNIX
![[Pasted image 20230728225512.png]]

![[Pasted image 20230728225822.png|500]]

![[Pasted image 20230728225920.png|500]]

Executables
![[Pasted image 20230728225956.png|500]]

Processes have process ID and d like directoires
![[Pasted image 20230728230104.png|500]]


### Lecture 2 – Process Control Commands
![[Pasted image 20230729204628.png]]

![[Pasted image 20230729204936.png]]

`ls || pwd &`, using OR one get executed if the first fails

`ls && pwd &` this creates only one Process ID for both commands <mark style="background: #FFF3A3A6;">Could not confirm</mark>

![[Pasted image 20230729210948.png]]

![[Pasted image 20230729211443.png]]

![[Pasted image 20230729211510.png]]

![[Pasted image 20230729212250.png]]

`kill -l` to see all Signals

### Lecture 3 – Other Process Control Tools
![[Pasted image 20230729213035.png]]

![[Pasted image 20230729213131.png]]
two hifens mean the number is negative which increases the priority 
![[Pasted image 20230729213432.png]]
renice
![[Pasted image 20230729213618.png]]

![[Pasted image 20230729214246.png]]



## Module 4 - Introduction To Shell Scripting

### Lecture 1 – What Is Shell Scripting?
![[Pasted image 20230729225006.png]]

![[Pasted image 20230729230523.png]]


### Lecture 2 – Working With A Shell Script
Creating scripts using vi, and making them executable

  
### Lecture 3 – Environment Variables
![[Pasted image 20230729234409.png]]

![[Pasted image 20230729234502.png]]

Environment variable are available even if you boot the system

When you run the `printenv` command without any arguments, it will print the values of all environment variables

When used without any arguments, `env` behaves similarly to `printenv` and displays all environmental variables:

However, the primary use of `env` is to set environmental variables for a specific command. For example, you can run a command with a modified environment without permanently changing the current shell's environment:

Example:
```bash
$ env VAR=value command
```
In this example, `VAR` is set to `value` only for the execution of the `command`, and it won't affect the `VAR` variable in the current shell's environment.

`unset` command remobes variables from environmental variables

### Lecture 4 – User Input In A Shell Script

![[Pasted image 20230730093012.png]]

Learned From quiz:
![[Pasted image 20230730095119.png]]
Option 1 is the correct answer:

> [!NOTE] Explanation
> In Shell scripting, `$*` is used to represent all the parameters (arguments) passed to the script. It expands to a single string containing all the parameters separated by spaces.
> 
> For example, if you run a shell script called `myscript.sh` like this:
> ```css
> ./myscript.sh arg1 arg2 arg3
> ```
> 
> Inside the script, you can use `$*` to refer to all the arguments collectively:
> ```css
> #!/bin/bash  echo "All parameters: $*"
> ```
> 
> The output will be:
> ```css
> All parameters: arg1 arg2 arg3
> ```
> 
> 
> So, `$*` indeed shows all parameter values passed to the shell script as a single space-separated string.



### Module 5 - Part 1 - Conditional And Looping

![[Pasted image 20230730100714.png]]

![[Pasted image 20230730100827.png]]

![[Pasted image 20230730100917.png]]

![[Pasted image 20230730101114.png]]

![[Pasted image 20230730101217.png]]
Notice has keyword **elif**
![[Pasted image 20230730102503.png]]

### Lecture 2 – Hands-On: Conditional Statements


[[1 Live Session]]

  
### Lecture 3 – Looping Statements
![[Pasted image 20230730133532.png]]


![[Pasted image 20230730134917.png]] 
while loop

![[Pasted image 20230730135249.png]]
For loop

![[Pasted image 20230730135428.png]]

![[Pasted image 20230730135615.png]]

![[Pasted image 20230730135708.png]]
Break will stop the execution and take you to the rest of the code
![[Pasted image 20230730135825.png]]
Continue will stop just like break but take it back to the while condition, NOT out of the loop


### Lecture 4 – Hands-On: Looping Statements

while loop
![[Pasted image 20230731205411.png]]

until loop
![[Pasted image 20230731205513.png]]

loop list
![[Pasted image 20230731205635.png]]
break
![[Pasted image 20230731205656.png]]
When it reaches 6 stops and outputs hello

Using **continue**: Skip the iteration
```bash
#!/bin/bash

# Loop from 1 to 5
for i in {1..5}; do
    # Check if the current value of i is 3
    if [ $i -eq 3 ]; then
        # Skip the iteration when i is 3
        continue
    fi
    # Display the current value of i
    echo "Current value: $i"
done
```

### Lecture 5 – Using Case..Esac Statement 
Also called switch statement
![[Pasted image 20230801083823.png]]

![[Pasted image 20230801084102.png]]


## Module 5 - Part 2 - Functions

### Lecture 1 – What Is A Function And Creating A Function
![[Pasted image 20230801093104.png]]

![[Pasted image 20230801093305.png]]
Didnt get the "Can use variables according to scope" #question

function
![[Pasted image 20230801093408.png]]

You can create funciton in the cli
![[Pasted image 20230801093516.png]]
this particual funciton wont wont execute in another shell

another way to create function
![[Pasted image 20230801093644.png]]

![[Pasted image 20230801093710.png]]

![[Pasted image 20230801093744.png]]

### Lecture 2 – Calling Functions
![[Pasted image 20230801094055.png]]
Calling function from another file
![[Pasted image 20230801094556.png]]

  
### Lecture 2 – Calling Functions
`./addsub-func.sh sub`


## Module 6 - Text Processing

### Lecture 1 – GREP Command
![[Pasted image 20230801104925.png]]

Ignore case, casing, the uppwercase lowercase
![[Pasted image 20230801105828.png]]

Another way of doing it, match either capital I or lower i
![[Pasted image 20230801110013.png]]

Search with starting word, not case senstive -i
![[Pasted image 20230801110138.png]]




![[Pasted image 20230801104825.png]]

exclude lines
![[Pasted image 20230801111023.png]]

### Lecture 2 – SED Command
![[Pasted image 20230801113151.png]]

He refered to the s as a flag
![[Pasted image 20230801113338.png]]


![[Pasted image 20230801113648.png]]
If you look there are some numbers with several 0s, but now the first zero has  been replaced with `*` (Otherwise all the zeros would be replaced)

![[Pasted image 20230801113928.png]]
the g flag is what makes the changes in every single line every single occurrence

![[Pasted image 20230801114206.png]]
Keep old file the same

![[Pasted image 20230801120301.png]]

![[Pasted image 20230801130430.png]]

![[Pasted image 20230801152508.png]]

![[Pasted image 20230801155545.png]]

![[Pasted image 20230801155651.png]]

### Lecture 3 – AWK Command
![[Pasted image 20230801162202.png]]

![[Pasted image 20230801162310.png]]

![[Pasted image 20230801162516.png]]
Prints the whole thing. The same if you use action `{print $0}` this explicit as oppose in the above which is implicit 

![[Pasted image 20230801165145.png]]


![[Pasted image 20230801165554.png]]
number the lines ,to the left see the numbers. NR number of rows

![[Pasted image 20230801165749.png]]
all of the rows have 4 columns so as you see to the left all have 4, NF number of fields

ORS Output Record Separator
![[Pasted image 20230801170031.png]]
here we are moving a tab
![[Pasted image 20230801170212.png]]

OFS Output Field Separator, i think they messed up in presentaiton leaving ORS
![[Pasted image 20230801170340.png]]

![[Pasted image 20230801191450.png]]

![[Pasted image 20230801192123.png]]

![[Pasted image 20230801192456.png]]
Need execution permissions


### Lecture 4 – Creating A Shared Folder
Did not follow along #pending

### Lecture 5 – SORT Command And Pipes
![[Pasted image 20230801212024.png]]

![[Pasted image 20230801212211.png]]
lower case sorted before capital,Since number are sorted before letters, we do get mokey3 with lowercase after a capital because it has a higher number


pipes
![[Pasted image 20230801212552.png]]
agains mentions running multiple commands

![[Pasted image 20230801212642.png]]
### Quiz Issue



> [!NOTE] What I should see
> - Which of the following command will print out the numbers of fields in a record from the data.csv file?
>     **Marked Answer :**
>     awk '{print NF}' data.csv
>     **Correct Answer :**
>     awk '{print NF,$0}' data.csv

> [!attention] What is displayed (Obsidian is RENDERING IT OJO)
> 
> 1) Which of the following command will print out the numbers of fields in a record from the data.csv file?
> 	awk &#039;{print NR}&#039; data.csv
> 	awk &#039;{print NR,$0}&#039; data.csv
> 	awk &#039;{print NF}&#039; data.csv
> 	awk &#039;{print NF,$0}&#039; data.csv

## Module 7 - Scheduling Tasks

### Lecture 1 – What Are Daemons?
![[Pasted image 20230801215359.png]]
not all of them end in `d`

![[Pasted image 20230801215730.png]]
![[Pasted image 20230801215742.png]]
start, stop, restart
command service probably replaced by systemctl

### Lecture 2 – Introduction To Task Scheduling

![[Pasted image 20230801222134.png]]

![[Pasted image 20230801222456.png]]
at , cron

### Lecture 3 – Cron And Crontab

![[Pasted image 20230801222821.png]]

![[Pasted image 20230802084556.png]]

![[Pasted image 20230802084755.png]]

`crontab -e`, to create the contrab job?
`crontab -l`, to check the jobs
you can also do it for a particular usr `crontab -u intellipaat -l`

### Lecture 4 – AT Command
![[Pasted image 20230802123226.png]]

![[Pasted image 20230802123349.png]]

`atq` to look at tasks in queue, `at` to schedule the `atrm` to remote task
![[Pasted image 20230802123920.png]]
You can use words midnight, tue for tuesday, in case of tue creates on tuesday executes on Tuesday the same time. If you dont want at the same time you are currently on you can do `at mon + 3 hours`

## Module 8 - Advanced Shell Scripting

### Lecture 1 – Introduction To Process Monitoring

![[Pasted image 20230802130931.png]]
![[Pasted image 20230802131149.png]]
ps an top, othe ryou can install

![[Pasted image 20230802131236.png]]

![[Pasted image 20230802131723.png]]
notice the command underneath

![[Pasted image 20230802131812.png]]

### Lecture 2 – Hands-On: Process Monitoring
top doesn't show all the processes just top ones
went over htop, you can click the collums to sort,
htop ver interactive with the mouse, 

ps is very good if you want to create a list of porcess . `ps -aux`

pgrep
![[Pasted image 20230802134039.png]]

### Lecture 3 – Introduction To File & Folder Monitoring
![[Pasted image 20230802134220.png]]

inotifywait
![[Pasted image 20230802134319.png]]
need ot install `sudo yum install inotify-tools`


![[Pasted image 20230802134536.png]]

![[Pasted image 20230802134642.png]]

![[Pasted image 20230802134728.png]]

### Lecture 4 – Hands-On: Inotifywait

![[Pasted image 20230802141451.png]]
Here he only monitors specifc event MODIFY that only gets trigger once he inserts string to 1.txt


free
![[Pasted image 20230802141608.png]]

### Lecture 5 – Signals

![[Pasted image 20230802174929.png]]
kill 
![[Pasted image 20230802175139.png]]

> [!NOTE]
> 1. **Notification to a Process**: Signals are used to notify a process about various events, such as a termination request (SIGTERM), an interrupt from the keyboard (SIGINT), or a division by zero (SIGFPE), among others.
>     
> 2. **Software Interrupts**: Signals are often described as "software interrupts" because, like hardware interrupts generated by devices, they interrupt the normal execution flow of a program. When a process receives a signal, it temporarily stops its normal execution to handle the signal.
>     
> 3. **Unpredictable Arrival**: The arrival of signals is generally unpredictable from the perspective of the receiving process. A signal can occur at any time during a program's execution, depending on the event triggering it.
>     
> 4. **Source of Signals**: Signals can originate from two main sources:
>     
>     - **Kernel**: The operating system kernel can send signals to processes for various reasons, such as hardware events, termination requests, or resource availability changes.
>     - **Process**: Processes can send signals to other processes using the `kill` system call or command. This allows one process to communicate with or influence another process.
>     - **User**: The user can also send signals to processes using the `kill` command from the shell. This allows a user to interact with processes, request termination, or perform other actions based on the signals they send.

###   Lecture 6 – Trapping Signals


![[Pasted image 20230802212934.png]]
You can prevent a process from beign interrupeted by signals, ignoring signals, you can trap specifc signal like -9 which kills the process 


![[Pasted image 20230802213243.png]]


### Lecture 7 – Hands On On Signals And Trapping Signals

![[Pasted image 20230802214057.png]]
We add  a trap to this script and now you can not interrupt it with `Crt-C`

![[Pasted image 20230802214416.png]]
Here we are re-instating the `Crt-C` interruption with `trap - 2`


![[Pasted image 20230802220019.png]]
trap that deletes file when script exits
`trap "rm -f hello.txt" EXIT`: This line sets up a "trap" command. The `trap` command allows you to define actions to be taken when the script or shell receives specific signals. In this case, the script sets a trap that will execute the command `rm -f hello.txt` when the script exits (i.e., reaches the end or is terminated).

Yes, in the context of the `trap` command, `EXIT` is a signal. However, it's important to clarify that `EXIT` is a special pseudo-signal used to specify that the trap action should be executed when the script or shell exits, rather than in response to a traditional signal (e.g., SIGINT, SIGTERM).

![[Pasted image 20230802222212.png]]
so this is an infinite loop until this 3 controls are done.
So the stop_it function only gets called when you SIGINT or Crt-C, which increases. Meanwhile the code that is running is the while loop. Eventually with enough counts stop_it exits the script
Is a way to warn the issuer they trying to stop an important function
Sample run
![[Pasted image 20230802222501.png]]


![[Pasted image 20230802222916.png]]

## Module 9 - Database Connectivity

### Lecture 1 – Installing And Configuring MySQL

```bash
sudo dnf install @mysql
```
<mark style="background: #FFB8EBA6;">In Centos used `sudo yum install mysql-server`</mark>

Start MySQL and make it automatically start at system boot
```bash
sudo systemctl enable --now mysqld
```

Check whether your MySQL service is running or not
```bash
sudo systemctl status mysqld
```

Runs some security-related operations like configuring a password
```bash
sudo mysql_secure_installation
```

*You will have to configure the "VALIDATE PASSWORD PLUGIN". It will validate your MySQL password to improve security by imposing better passwords*

***SHOW VARIABLES LIKE 'validate_password%';**
Run this query to check your password policy, you can also change it as per your needs. You can change it by running the below query*

So you can check the variables
![[Pasted image 20230803101448.png]]

Then like this you can change them. Notice `validate_password.policy` is a var
```mysql
mysql> SET GLOBAL validate_password.policy=LOW;
Query 0K, 0 rows affected (0.00 sec)
```



### Lecture 2 – Running SQL Queries From Terminal

Accessing MySQL using the client `mysql -u root -p`

- Running queries directly from the shell:
	Check all databases `mysql -u <username> -p -e 'show databases'`
	Query on a DB — `mysql —D <database name> -u <username> -p -e 'query'`
		ex: `mysql -D dev -u root -p -e 'show tables;'`
	Save output in a file — `mysql -u <username> -p -e 'query' > output.txt`

### Lecture 3 – Running SQL Queries From Shell Scripts

Shell script to show databases
```bash
#!/bin/bash
mysql -u root -p << EOF
show databases;
EOF
```

Shell script to create database, create a table and insert data into that
```mysql
#!/bin/bash

# Start the MySQL client and log in as the root user
mysql -u root -p <<EOF
# Within the MySQL client, create a new database named "dbl"
CREATE DATABASE dbl;
# Switch to the "dbl" database
USE dbl; 

# Create a new table named "tablel" with three columns: bookingid, date, and name
CREATE TABLE tablel (
    bookingid INT NOT NULL AUTO_INCREMENT,
    date VARCHAR(50) NOT NULL,
    name VARCHAR(50),
    PRIMARY KEY (bookingid, date, name)
);
# Insert rows into the "tablel" table
INSERT INTO tablel (date, name) VALUES ('2/2/2019', 'kodee');
INSERT INTO tablel (date, name) VALUES ('2/3/2019', 'jake');
INSERT INTO tablel (date, name) VALUES ('2/4/2019', 'holt');
INSERT INTO tablel (date, name) VALUES ('2/5/2019', 'rosa');
# End the MySQL commands
EOF

echo "successful"

```
Then you can just execute the bash script. Remmeber to add execute permission `chmod +x script.sh`
To check 
```bash
mysql -u root -p -e 'use dbl; select * from tablel;
```


## Module 10 - Linux Networking

  
### Lecture 1 – What Is Networking In Linux?
- A group of interconnected computers are called as a Network; Working on networks and handling them would be called as Networking
- A system administrator's routine tasks include configuring, maintaining, troubleshooting, and managing servers and networks within data centers. There are numerous tools and utilities in Linux designed for theadministrative purposes.


  
### Lecture 2 – Networking Commands – (Ifconfig & Ping , Wget & Curl)

Ifconfig — Kernel links up the software side to the hardware side using a network interface; Using this command you can configure them

```css
#example
ifconfig enp0s3 #information
sudo ifdown enp0s3 #disable
sudo ifup enp0s3 #enable
```

ping — A way to check whether a computer can communicate with another computer over the network
```bash
ping -c 6 <IP> #ping 6 times, instead of infinte
```

wget — A command used to retrieve content from web servers. Only http?

```css
#sample
$ wget <URL>
$ wget https://docs.aws.amazon.com/AWSEC2/Iatest/UserGuide/ec2-ug.pdf
```


cURL — A command to transfer data using various protocols

```css
$ curl <URL>
$ curl https://intellipaat.com/blog/what-is-data-science/ > intel.html
```

  
### Lecture 3 – Networking Commands – (Ssh, Scp And Ftp)

ssh — Used for a secure remote login to another computer
```css
#sample
ssh intelli aat@192.168.122.1
```


scp — Secure Copy Protocol for safely transferring files from one computer to other

ftp — Most used protocol for file transfer between computers

```css
#sample
ftp ftp.cesca.es #use anosnymus

scp intel.html ftp.cesca.es #tried copying to test server
ftp ftp.cesca.es #cheching to see if is there
get <filename>
```



### Lecture 4 – Firewall Tools
*Run diff combinations of commands you did not copy*

firewall is a network security program

Iptables — It is an application which can be used to configure firewall security tables

```bash
iptables --version
sudo iptables -L #rules
```

Allowing a port:
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```
Blocking a port:
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j DROP
```

You can have a rule that drops, lets say port 80 but you can can also delete rules


firewalld — A dynamically managed firewall application
	Zones — These are set of rules which decide whether a traffic should be allowed or blocked
```bash
sudo firewall-cmd --get-active-zones
```

Allow port:
```bash
sudo firewall-cmd --permanent —zone—public --add-port=80/tcp
```
Remove port:
```bash
sudo firewall-cmd —zone=public --remove-port=80/tcp
```


### Lecture 5 – DNS And Resolving IP Address

`/etc/hosts` An OS file which translates domain names to IP addresses
![[Pasted image 20230803152301.png]]
Learned you can have multiple  domain names next to the ip like 'hello'

`/etc/hostname` Contains name of the local machine as to run applications locally

`nslookup` Name Server lookup is used to query name servers of mentioned domains to find info about the resource records
uses: find the IP of a domain, or name of domain,

`dig`— Domain information Groper is used to get info about DNS name servers and is more flexible than nslookup
![[Pasted image 20230803153500.png]]

## Linux Quiz And Project

### Project – Installing WordPress On Centos7 #pending
	[[Advanced-Linux_Intellipaat-Capstone-Project.pdf]]
### [[Linux Quiz 1]]


---

# Previous Version

