# Client Certificate  
In cryptography, a `client certificate` can be defined as a `digital certificate`. It authenticates the `identity` of the requester to a remote server.  
  The requester could be email users or website users. A `client certificate` ensures the server that it is communicating with a legitimate user.  

> Client certificates are used to validate the identity of a client (user)`  

The user, in this case, might be a website user or an email user.   
  Simply put, it works as a password, but without any intervention/input from the user.  
  This way, the server makes sure that it’s connecting to the permitted user and that party is safe to communicate with.  

Sometimes passwords are not good enough.  
  We often fall prey to password cracking techniques such as brute-force attacks and keyloggers.  
  That’s why passwords are no longer sufficient when you have some really highly-sensitive information at stake  

So, there might be some documents or files that you want only designated people to access.  
  But as passwords are not secure enough, you’ll have to explore your options.  
  That’s where Client certificates come in.  
  Instead of validating people via passwords, Client certificates authenticate people by the systems they use.   
  If the user doesn’t have the granted permissions, he/she won’t be granted access.  
  To make it even more secure, you can combine the use of client certificates with passwords.  
  In technical terms, this is called `Two-factor Authentication`.   
  It is an absolute must for organizations dealing with sensitive data – both internal as well as external.  

Client certificates also use public key infrastructure (PKI) for authentication, just like Server certificates.  

**Key difference:**  
  > Unlike Server certificates, Client certificates don't encrypt any data; they're installed for validation purposes only.  

**Reference:**  
- https://cheapsslsecurity.com/blog/client-certificate-vs-server-certificate-simplifying-the-difference/

