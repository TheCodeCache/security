# Self-Signed X.509 Certificate — 

We can use `OpenSSL` to generate a `self-signed X.509 certificate` with a 1024-bit RSA private key.  
The key allows access to the issuer's Amazon EMR cluster instances in the us-west-2 (Oregon) region  
as specified by the *.us-west-2.compute.internal domain name as the common name.  

Other optional subject items, such as country (C), state (S), and Locale (L), are specified.  
Because a self-signed certificate is generated,  
the second command in the example copies the certificateChain.pem file to the trustedCertificates.pem file.  
The third command uses zip to create the my-certs.zip file that contains the certificates.  

The sample code is as follows —  

```shell
$ openssl req -x509 -newkey rsa:1024 -keyout privateKey.pem -out certificateChain.pem -days 365 -nodes -subj '/C=US/ST=Washington/L=Seattle/O=MyOrg/OU=MyDept/CN=*.us-west-2.compute.internal'
$ cp certificateChain.pem trustedCertificates.pem
$ zip -r -X my-certs.zip certificateChain.pem privateKey.pem trustedCertificates.pem
```

**Recommendations —**  

Using self-signed certificates is not recommended and presents a potential security risk.  
For production systems, use a trusted certification authority (CA) to issue certificates.

**Reference:**  
1. https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-encryption-enable.html  

