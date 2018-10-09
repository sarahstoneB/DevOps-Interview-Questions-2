# Linux Administration Questions

##### What is Zombie Process?

   When a process dies, the parent is notified with SIGCHILD signal. The parent is supposed to execute wait() call. If it doesn't,
   the process will stick around in the memory as zombie process.
   
##### Explain the three load averages and what do they indicate?

  Load Average is the value which represents the average load on your system for a specific period of time.
   Three numbers represent load averages in 1min, 5mins and 15 mins It an be seen by "top" or "uptme" cmd.

 ##### What is RAID 0, RAID 1, RAID 5 and RAID 10?

  **RAID 0:** Striped, No redundancy, and good performance. Used for gaming. You stripe if you have two volumes or more. If one disk   fails, the whole RAID array fails(redundancy).

  **RAID 1:** It is mirrored which means you can mirror an exact copy of another disk and redundant.

  **RAID 5:**  3 disks or more. It is good for READS and bad for WRITES. RAID 5 is not recommended to put on EBS. RAID 5 is basically writing the parities(CHECKSUM)

  **RAID 10:** It is the combination of RAID 0 and RAID 1.

 ### Linux Commands
 
**id:** to check uid of the the user (root is always = 0)
 
**df -h:** to check the disk space in the file system
 
**du -h:** to check the disk usage of files and directories on a machine

**free:** displays amount of free and used memory in the system.

**top:** displays system tasks

**netstat:** lists all the open ports

**curl:**  It is  a  tool  to transfer data from or to a server.
