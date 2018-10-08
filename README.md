# DevOps Interview Questions

## Table of Contents

##### 1. Linux Administration
##### 2. AWS Questions


### General Questions

#### What is DNS?

  DNS is a domain system which resolves host/domain names into IP adresses.
  
#### How does DNS work?

  https://dyn.com/blog/dns-why-its-important-how-it-works/
  
#### Difference between Telnet and SSH

 They are network protocols used to connect to remote servers. The difference is SSH is more secure where SSH encrypts the data and uses     the public key for authentication and Telnet sends the data as a plain text.

#### What happens when you type URL?

   a. Browser checks cache; if requested object is in cache and is fresh, skip to #9

   b. Browser asks OS for server's IP address.

   c. OS makes a DNS lookup and replies the IP address to the browser.

   d. Browser opens a TCP connection to server (this step is much more complex with HTTPS)

   e. The browser sends the HTTP request through TCP connection.

   f. The browser receives HTTP response and may close the TCP connection, or reuse it for another request

   g. Browser checks if the response is a redirect or a conditional response (3xx result status codes) authorization request (401), error (4xx and 5xx), etc.; 
      these are handled differently from normal responses (2xx)

   h. If cacheable, response is stored in cache

   i. Browser decodes response (e.g. if it's gzipped)

   j. The browser determines what to do with response (e.g. is it a HTML page, is it an image, is it a sound clip?)

   h. the browser renders response, or offers a download dialog for unrecognized types.

#### What is Zombie Process?

   When a process dies, the parent is notified with SIGCHILD signal. The parent is supposed to execute wait() call. If it doesn't,
   the process will stick around in the memory as zombie process.
   
#### Explain the three load averages and what do they indicate?

  Load Average is the value which represents the average load on your system for a specific period of time.
   Three numbers represent load averages in 1min, 5mins and 15 mins It an be seen by "top" or "uptme" cmd.
   
#### Difference between TCP and UDP:

  TCP                                                                             TCP
  
  a. Connection-oriented protocol                                                 a.Connectionless protocol 
  b. Stream oriented                                                              b.Message oriented
  c. TCP is suited for applications that require high reliability,                c.UDP is suitable for applications that need fast, efficient transmission, such as games. 
  and transmission time is relatively less critical.
  d. TCP header size is 20 bytes                                                  d.  UDP Header size is 8 bytes.
  e. The speed for TCP is slower than UDP.                                        e. UDP is faster because error recovery is not      attempted. It is a "best effort" protocol.
