## Part1. OS installation

1. Ubuntu version

    ![part1](./screenshots/part1.png)


## Part2. User creation

1. User Creation command

    ![part2_1](./screenshots/part2.png)

2. Adding user `michaleh` to the "adm" group

    `sudo usermod -a -G adm michaleh`

3. The output of cat command shows the new user

    ![part2_2](./screenshots/part2_2.png)

## Part3. OS network setup

1. Setting the machine name as `user-1`

    `hostnamectl set-hostname user-1`

2. Setting the time zone of our location

    1) find out the current time zone
   
        `timedatectl status`
   
    2) looking for a suitable time zone in the list
   
        `timedatectl list-timezones`
   
    3) setting the selected time zone
   
        `timedatectl set-timezone Europe/Moscow`

3. Use the `ip link show` to display network interfaces

    ![part3_1](./screenshots/part3_1.png)

    lo interface is an implementation of a virtual network interface that is not related to hardware in any way, but is
    fully integrated into the network infrastructure of a computer system. Any traffic sent by the program to this 
    interface (loopback) is returned to this interface. Using this interface allows you to establish a connection 
    between a client program and a server program running on the same computer regardless of the configuration of 
    hardware systems (no modem, network card, etc. are needed), this interface is implemented using a pseudo device 
    driver in the operating system kernel

4. Dynamic Host Configuration Protocol (DHCP) - is an application protocol that allows network devices to automatically 
    obtain an IP-address and other parameters necessary to operate on a TCP/IP network

    ![part3_2](./screenshots/part3_2.png)

    This screenshot shows that the current IP address is: 10.0.2.15

5. To get an external IP address, we send a request to the site, which returns the IP address to us

    ![part3_3](./screenshots/part3_3.png)

    To get the internal IP address, execute the command `ip address`

    ![part3_4](./screenshots/part3_4.png)

    Internal IP address: 10.0.2.2

6. To set a static IP address, you need to edit the `/etc/netplan/00-installer-config.yml` file as follows

    ![part3_5](./screenshots/part3_5.png)

    After that, you need to apply the settings

    `sudo netplan apply`

7. We reboot the machine with the `reboot` command

8. Run the `ip address` command to check the static IP address

    ![part3_6](./screenshots/part3_6.png)

    Static address: 10.0.2.16/24, which corresponds to the settings we specified

9. `Ping 1.1.1.1` shows the Internet is working

    ![ping3_7](./screenshots/part3_7.png)

10. `Ping ya.ru` also shows that the network is configured

    ![ping3_8](./screenshots/part3_8.png)

## Part 4. OS update

1. Updates are installed using commands:
    
    `sudo apt update`
    
    `sudo apt upgrade`

    ![part3_9](./screenshots/part3_9.png)

    This screenshot shows that there is nothing more to update

## Part 5. Using the sudo command

1. The sudo command allows you to run commands as an administrator, that is, those that require special permission. This
    is done to protect against accidental "shooting yourself in the foot". These privileges should be handled with care,
    as the security and integrity of the system may depend on them.

2. To allow a user to execute the sudo command, you must add him to the sudo group

    `sudo adduser michaleh sudo`

3. We change the machine name on behalf of the user michaleh (this can be seen when choosing from which user we make 
    changes)

    ![part5_1](./screenshots/part5_1.png)

4. The new machine name is shown in the output of the command

    ![part5_2](./screenshots/part5_2.png)

## Part 6. Installing and configuring the time service

1. Find out the current time in the local time zone.

    ![part6_1](./screenshots/part6_1.png)

2. The output of the `timedatectl show` command indicates that synchronization is set

    ![part6_2](./screenshots/part6_2.png)

## Part 7. Installing and using text editors

1. Since I already have Vim and Nano installed. I also install emacs

    `sudo apt install emacs`

2. To create a file in emacs, open the file with emacs

    `emacs test_emacs.txt` 

3. To exit and save the changes, you must use the keyboard shortcut (control+x) then (control+c), this command will ask
    you to save the file before exiting. When asked whether to save the file - answer yes (y)

    ![part7_1](./screenshots/part7_1.png)

4. Just like in emacs, in Vim, to create a new file, you need to open it with the desired name 

    `vim test_vim.txt`

5.  To exit Vim and save your changes, you must press `ESC` and type `:wq`

    ![part7_2](./screenshots/part7_2.png)

6. To create a file in Nano, you need to do the same as in the editors above

    `nano test_nano.txt`

7. This editor has tips with quick commands, when using the combination (control+x), the editor will ask if we want to 
    save the file. We answer - yes (y). And then we can confirm the file name, or write the changes to a separate file.

    ![part7_3](./screenshots/part7_3.png)

8. To edit a file, you need to open it, we do this the same way as when creating a file

9. To exit Vim without saving, press `ESC` and type `:q!`

    ![part7_4](./screenshots/part7_4.png)
    
10. To exit emacs without saving, we can use the same method as when exiting with saving, but when asked whether to save
     the file, we answer - no(n)

    ![part7_5](./screenshots/part7_5.png)

11. To exit Nano, you also need to repeat the same steps as for exiting with saving but answer the question saving - no

    ![part7_6](./screenshots/part7_6.png)

12. To find a word in Vim, you need to press `ESC`and then enter `:s/<word_we_are_looking_for>`, it will be highlighted

    ![part7_7](./screenshots/part7_7.png)

13. To replace this word, add to the previous command `/word_to_change_to>`

    ![part7_8](./screenshots/part7_8.png)

14. To search a word in emacs, you need to use the shortcut (control+s) and then type the word you are looking for

    ![part7_9](./screenshots/part7_9.png)

15. To replace a word in emacs, you need to use the shortcut (alt+x), and then enter `replace-string`, press `enter`
     enter the word to be replaced, and enter the word we want to replace with

    ![part7_10](./screenshots/part7_10.png)

16. To find a word in Nano, you must use the shortcut (control+W), and enter the word you are looking for

    ![part7_11](./screenshots/part7_11.png)

17. To replace a word in nano, you need to use the shortcut (control+\) and enter the word we want to replace, press 
     `enter` and then enter the word we want to replace with and press `enter`

    ![part7_12](./screenshots/part7_12.png)

## Part 8. Installing and basic configuration of the SSHD service

1.  Install OpenSSH Server

    `sudo apt install openssh-server`

2.  We configure the autostart of the service at the system boot

    `sudo systemctl enable ssh`

3. To change the port, edit the `/etc/ssh/sshd_config` file, adding the line: `Port 2022`

4. To show the presence of the sshd process using the ps command, this command must be used with the `-C` flag and the 
    name of the `sshd` command, this flag implies the output of the process by the name of the command

    ![part8_1](./screenshots/part8_1.png)

5. Reboot the system with the `reboot` command

6. Install netstat

    `sudo apt install net-tools`

7. We run the `netstat -tan` command, where the `-tan` flag implies three flags:
    `-t` - show the current connection in the stage of transferring the load from the processor to the network 
           adapter
    `-a` - show the status of all sockets, as a rule, sockets used by server processes are not shown,
    `-n` - show network addresses as numbers

    ![part8_2](./screenshots/part8_2.png)

    The columns in the output means the following

    `Proto` - Protocol used by the socket

    `Recv-Q` & `Send-Q` - In our case (Listen) demonstrates that the program works correctly with the receiving 
                          and sending side (returns 0).

    `Local Address` - Shows the local address and port, 0.0.0.0 - means that the service can connect to all network 
                      interfaces. It allows you to listen and accept connections from any IP address

    `Foreign Address` - remote address (similar of the local address for the other side)

    `State` - socket status. In our case, the socket is listening for incoming connections. Such connections are not 
              included  in the output without the `-a` flag

## Part 9. Installing and using the top htop utilities

1. I already have top and htop installed

    Based on the output from top

    uptime - 40 min;
    
    number of the authorized users - 1 user;

    total system load - 0,00

    total number of the processes - 95

    cpu load - 0,0(0,3)

    memory load - 2941,4 MiB

    pid of the process taking the most memory - systemd

    pid of the process taking the most CPU time - top

2. htop output sorted by PID

    ![part9_1](./screenshots/part9_1.png)

3. htop output sorted by PERCENT_CPU

    ![part9_2](./screenshots/part9_2.png)

4. htop output sorted by PERCENT_MEM

    ![part9_3](./screenshots/part9_3.png)

5. htop output sorted by TIME

    ![part9_4](./screenshots/part9_4.png)

6. htop output filtered by sshd process

    ![part9_5](./screenshots/part9_5.png)

7. htop output with syslog process found using search

    ![part9_6](./screenshots/part9_6.png)

8. htop output with hostname, clock and uptime output added

    ![part9_7](./screenshots/part9_7.png)

## Part 10. Using te fdisk utility

1. HDD name - /dev/sda

2. HDD size - 10 GiB

3. Number of sectors - 20971520

4. Swap size - 907M

## Part 11. Using the df utility

1. For root partition with df utility

    1) Partition size - 9299276

    2) Used space - 4516216

    3) Free space - 4289084

    4) Usage percent - 52%

2. For root partition with df utility and -Th flag

    1) Partition size - 8,9G

    2) Used space - 4,4G

    3) Free space - 4,1G

    4) Usage percent - 52%

3. File system type ext4

## Part 12. Using du utility

1. du output

    ![part12_1](./screenshots/part12_1.png)

2. du output with flags

    `-b` - fot output in bytes

    `-h` - for output in human-readable form

    `-s` - for summary output by directory

    ![part12_2](./screenshots/part12_2.png)

3. Printing the size of all content in `/var/log` using the command

    `sudo du -b -h /var/log/*`

    ![part12_3](./screenshots/part12_3.png)

## Part 13. Installing and using the ncdu utility

1. Install the ncdu utility

    `sudo apt install ncdu`

2. Print the size of /var/log with the `ncdu /var/log` command

   ![part12_4](./screenshots/part12_4.png)

3. Print the size of /var with the `ncdu /var` command

    ![part12_5](./screenshots/part12_5.png)

4. Print the size of /home with the `ncdu /home`

    ![part12_6](./screenshots/part12_6.png)

## Part 14. Work with system logs

1. Time of the last successful authorization - August 1 12:44:32

2. User name - user

3. Login method (login:session)

4. SSHd restart message

    ![part14](./screenshots/part14.png)

## Part 15. Using the CRON Job Scheduler

1. Run the uptime command every two minutes

    ![part15](./screenshots/part15_1.png)

2. View current CRON jobs

    ![part15_2](./screenshots/part15_2.png)

3. View current tasks after deleting tasks from the scheduler

    ![part15_3](./screenshots/part15_3.png)