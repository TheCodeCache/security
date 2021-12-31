# Self-Signed X.509 Certificate — 

We can use `OpenSSL` to generate a `self-signed X.509 certificate` with a 1024-bit RSA private key.  

The sample code is as follows —  

```shell
$ openssl req -x509 -newkey rsa:1024 -keyout privateKey.pem -out certificateChain.pem -days 365 -nodes -subj '/C=US/ST=Washington/L=Seattle/O=MyOrg/OU=MyDept/CN=*.us-west-2.compute.internal'
$ cp certificateChain.pem trustedCertificates.pem
$ zip -r -X my-certs.zip certificateChain.pem privateKey.pem trustedCertificates.pem
```

**Reference:**  
1. https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-encryption-enable.html  

