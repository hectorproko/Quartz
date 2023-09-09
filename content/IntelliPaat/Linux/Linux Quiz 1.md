Sure, here are all the answers to the questions:

1. Linux Installation media is normally downloaded in .iso format? Answer: TRUE
    
2. Which of the following is not a Package Manager? (Choose Two) Answer: Virtual Box and VM Ware

3. Linux Installation with provides both text mode and graphical mode? (Choose Two) Answer: Server with GUI and Linux Desktop

4. Which partitioning option allows you to set the partitions size according to your wish? Answer: Manual partitioning
    
5. Which of the following is used to pass on commands to the Linux OS? Answer: Shell
    
6. ___________ is the core of the Operating System. Answer: Kernel
    
7. Kernel Parameters are stored at runtime in which file system? Answer: /proc
    
8. Kernel parameters are loaded from which file in Linux? Answer: /etc/sysctl.conf
    
9. After writing to /etc/sysctl.conf which command is used to load the values to the /proc without rebooting the system? Answer: sysctl -p
    
10. Command yum install httpd does the following: Answer: Installs apache
    
11. Rpm command to delete a package foo.rpm Answer: rpm -e foo.rpm
    
12. Rpm command to list the files related to package foo.rpm? Answer: rpm -ql foo
    
13. Yum command to update package lists? Answer: yum update
    
14. The following command will list disk partition information. Answer: df
    
15. Services are stopped using which of the following commands. (Choose two) Answer:
    

- systemctl <servicename> stop
- service <servicename> stop

16. Which command will tell you whether a service is running or not? Answer: systemctl status
    
17. Which command will allow you to not run a service at boot time? (Choose two) Answer:
    

- systemctl disable
- chkconfig off

18. The following command is used for creating groups in Linux. Answer: groupadd
    
19. The details regarding the user’s shell interface are stored in which file. Answer: /etc/passwd
    
20. We can expire the password of a user with the following command: Answer: passwd -e username
    
21. Will the useradd command create the user’s home directory? Answer: It depends. By default, the useradd command does not create the user's home directory. However, you can use the -m option with the useradd command to automatically create the user's home directory.
    
22. You can lock user ‘tom’ using the following command? Answer: passwd -l tom
    
23. Multiple users cannot log in to a Linux system at the same time? Answer: FALSE. Multiple users can log in to a Linux system simultaneously, especially in multi-user environments like servers.
    
24. Which of these directory trees are temporary and created every time the system boots up? Answer: /var is a directory tree that is temporary and created every time the system boots up. It contains variable data files, such as logs, spool files, temporary files, etc.
    
25. Which of the following commands reboots the system? (Choose all that apply) Answer:
    

- shutdown –r now
- init 6
- reboot
- telinit 0

26. Which number after the chmod command will provide all access to the file ‘foo’? Answer: chmod 777 foo
    
27. Which command will make the file foo ‘read-only’ to all users? Answer: chmod 444 foo
    
28. The most common network topology in a LAN is: Answer: Star
    
29. We use the following to check if an IP 192.168.0.10 is alive in the network? Answer: ping 192.168.0.10
    
30. A caching-only DNS server does the following (Choose Multiple) Answer:
    

- Resolve domain name to IP if the entry is present in its cache
- Resolve domain name to IP if the entry is not present in its cache
- Does not consult the primary DNS for every query
