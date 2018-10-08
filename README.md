# DevOps Interview Questions

## Table of Contents

##### 1. Linux Administration
   - 1.1 General Questions
   - 1.2 Linux Commands
##### 2. AWS Questions

#### 1. Linux Administration
### 1.1 General Questions

#### What is DNS?

  DNS is a domain system which resolves host/domain names into IP adresses.
  
#### How does DNS work?

  https://dyn.com/blog/dns-why-its-important-how-it-works/
  
#### Difference between Telnet and SSH

 They are network protocols used to connect to remote servers. The difference is SSH is more secure where SSH encrypts the data and uses     the public key for authentication and Telnet sends the data as a plain text.

#### What happens when you type URL?

- Browser checks cache; if requested object is in cache and is fresh, skip to #9

- Browser asks OS for server's IP address.

- OS makes a DNS lookup and replies the IP address to the browser.

- Browser opens a TCP connection to server (this step is much more complex with HTTPS)

- The browser sends the HTTP request through TCP connection.

- The browser receives HTTP response and may close the TCP connection, or reuse it for another request

- Browser checks if the response is a redirect or a conditional response (3xx result status codes) authorization request (401), error (4xx and 5xx), etc.; 
      these are handled differently from normal responses (2xx)

- If cacheable, response is stored in cache

- Browser decodes response (e.g. if it's gzipped)

- The browser determines what to do with response (e.g. is it a HTML page, is it an image, is it a sound clip?)

- the browser renders response, or offers a download dialog for unrecognized types.

#### What is Zombie Process?

   When a process dies, the parent is notified with SIGCHILD signal. The parent is supposed to execute wait() call. If it doesn't,
   the process will stick around in the memory as zombie process.
   
#### Explain the three load averages and what do they indicate?

  Load Average is the value which represents the average load on your system for a specific period of time.
   Three numbers represent load averages in 1min, 5mins and 15 mins It an be seen by "top" or "uptme" cmd.
   
#### Difference between TCP and UDP:

- TCP is Connection-oriented protocol and UDP is Connectionless protocol   
  
- TCP is Stream oriented and UDP is Message oriented protocol
  
- TCP is suited for applications that require high reliability and UDP is suitable for applications that need fast, efficient  transmission, such as games.  and transmission time is relatively less critical.
  
- TCP header size is 20 bytes and UDP Header size is 8 bytes.
  
- The speed for TCP is slower than UDP and UDP is faster because error recovery is not attempted. It is a "best effort" protocol.
  
 #### What is RAID 0, RAID 1, RAID 5 and RAID 10?

  **RAID 0:** Striped, No redundancy, and good performance. Used for gaming. You stripe if you have two volumes or more. If one disk   fails, the whole RAID array fails(redundancy).

  **RAID 1:** It is mirrored which means you can mirror an exact copy of another disk and redundant.

  **RAID 5:**  3 disks or more. It is good for READS and bad for WRITES. RAID 5 is not recommended to put on EBS. RAID 5 is basically writing the parities(CHECKSUM)

  **RAID 10:** It is the combination of RAID 0 and RAID 1.

 ### 1.2 Linux Commands
 
**id:** to check uid of the the user (root is always = 0)
 
**df -h:** to check the disk space in the file system
 
**du -h:** to check the disk usage of files and directories on a machine

**free:** displays amount of free and used memory in the system.

**top:** displays system tasks

**netstat:** lists all the open ports

**curl:**  It is  a  tool  to transfer data from or to a server.
