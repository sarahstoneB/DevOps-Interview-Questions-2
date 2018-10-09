# Networking Questions

### What is DNS?

  DNS is a domain system which resolves host/domain names into IP adresses.
  
### How does DNS work?

  https://dyn.com/blog/dns-why-its-important-how-it-works/
  
### Difference between Telnet and SSH

 They are network protocols used to connect to remote servers. The difference is SSH is more secure where SSH encrypts the data and uses     the public key for authentication and Telnet sends the data as a plain text.

### What happens when you type URL?

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

### Difference between TCP and UDP:

- TCP is Connection-oriented protocol and UDP is Connectionless protocol   
  
- TCP is Stream oriented and UDP is Message oriented protocol
  
- TCP is suited for applications that require high reliability and UDP is suitable for applications that need fast, efficient  transmission, such as games.  and transmission time is relatively less critical.
  
- TCP header size is 20 bytes and UDP Header size is 8 bytes.
  
- The speed for TCP is slower than UDP and UDP is faster because error recovery is not attempted. It is a "best effort" protocol.
